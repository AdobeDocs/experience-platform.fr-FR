---
title: Présentation De La Configuration Du Flux De Données Dynamique
description: Découvrez comment  [!DNL Dynamic Datastream Configurations] achemine les événements vers les services Experience Cloud en fonction de règles et en quoi il se compare à d’autres options de routage.
source-git-commit: 738597c837440cb66aa80b24f1f877c9c4cb758b
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---


# Présentation de la configuration des trains de données dynamiques

Par défaut, le [!DNL Adobe Experience Platform Edge Network] envoie chaque événement arrivant sur un [flux de données](/help/datastreams/overview.md) à tous [!DNL Experience Cloud] services que vous avez activés. Utilisez des [!DNL Dynamic Datastream Configurations] pour définir des **règles** qui contrôlent quels services reçoivent quels événements et/ou quels jeux de données stockent ces événements, sans modifier le code SDK côté client.

Avant la [!DNL Dynamic Datastream Configurations], le contrôle du routage des événements nécessitait de gérer plusieurs flux de données ou d’ajouter une logique de remplacement dans votre implémentation SDK côté client. [!DNL Dynamic Datastream Configurations] déplacez cette logique de routage côté serveur dans le flux de données lui-même.

## Ce que [!DNL Dynamic Datastream Configurations] pouvez faire {#can-do}

Le tableau suivant récapitule les actions de routage disponibles.

| Action | Exemple |
|--------|---------|
| Acheminer des événements vers différents jeux de données | Les pages vues accèdent à un jeu de données ne concernant pas les profils ; les achats accèdent à un jeu de données activé pour les profils |
| Désactivation d’un service pour les événements correspondants | Désactiver l’ingestion des [!DNL Adobe Experience Platform] pour le trafic de robots |
| Remplacer les paramètres de service par événement | Envoyer des événements à différentes suites de rapports [!DNL Adobe Analytics] ou jetons de propriété [!DNL Adobe Target] en fonction des conditions d’événement |
| Activation ou désactivation des sous-services Experience Platform | Désactivez [!UICONTROL Segmentation ], [!DNL Adobe Journey Optimizer], [!UICONTROL Gestion des décisions] ou [!UICONTROL Destinations Personalization] pour des types d’événements spécifiques |

## Ce que [!DNL Dynamic Datastream Configurations] ne peut pas faire {#cannot-do}

Les configurations de train de données dynamiques sont conçues pour le routage au niveau de l’événement. Les actions suivantes ne sont pas prises en charge.

| Action | Motif |
| ------ | ------ |
| Envoyer le même événement à plusieurs jeux de données en parallèle | Les règles acheminent un événement vers un seul jeu de données |
| Supprimer des champs des payloads d’événement | Edge Network transfère toujours l’événement complet |
| Évaluer les conditions en fonction des attributs de profil | Les règles évaluent uniquement la payload de l’événement entrant |

## Modèle d’évaluation de règle {#rule-evaluation}

Comprendre comment Edge Network évalue les **règles** vous aide à concevoir des configurations qui se comportent de manière prévisible.

- **Le premier match gagne.** Edge Network évalue les règles dans l’ordre dans lequel vous les définissez. Lorsqu’un événement correspond à une règle, Edge Network applique la configuration de routage de cette règle et arrête l’évaluation des autres règles.
- **Secours par défaut.** Si aucune règle ne correspond à un événement, l’événement suit la [configuration de train de données](/help/datastreams/configure.md#aep) statique par défaut : le jeu de données d’événement principal et tous les services activés.
- **budget d’évaluation de 25 ms.** Toutes les règles d’un flux de données doivent être évaluées dans un délai de 25 ms au total. Si l’évaluation dépasse ce budget, l’événement retourne à la configuration de train de données par défaut. Veillez à ce que les règles restent simples et axées sur des champs fiables tels que les `eventType`.
- **Expressions plates uniquement.** Le système ne prend pas en charge les expressions logiques imbriquées (conteneurs dans des conteneurs). Si votre logique nécessite l’imbrication, divisez-la plutôt en plusieurs règles aplaties.

Pour obtenir la liste complète des types de données, des opérateurs et des mécanismes de sécurisation pris en charge, voir [Créer des configurations de flux de données dynamiques](/help/datastreams/configure-dynamic-datastream.md).

## Taxonomie des valeurs d’événement {#event-taxonomy}

Avant de concevoir des règles, classez tous les types d’événements envoyés par votre implémentation dans l’une des trois catégories. Cette classification détermine directement votre stratégie de jeu de données et la conception de règle.

| Catégorie | Description | Exemples |
|----------|-------------|---------|
| **Consommable** | Événements sans valeur analytique ou exploitable. | Événements générés par des robots, événements opérationnels tels que `decisioning.propositionFetch` et `personalization.request` |
| **Analytique** | Événements nécessaires uniquement pour la création de rapports Analytics. Ces événements ne sont pas nécessaires pour l’enrichissement des profils et ne sont pas exploitables dans la segmentation et l’activation. | Pages vues, profondeur de défilement, comportement de navigation général |
| **Exploitable** | Événements nécessaires à l’enrichissement du profil et exploitables dans la segmentation et l’activation. Ces événements sont également analytiques et disponibles dans les rapports d’analyse. | Achats, ajout au panier, envois de formulaire, événements de conversion clés |

La classification des événements avant de configurer des règles est l’étape de planification la plus importante. Il détermine les jeux de données dont vous avez besoin, les événements qui vont à quels jeux de données et le nombre de règles que vous devez écrire.

## Exclusivité mutuelle avec les remplacements de train de données {#overrides}

>[!IMPORTANT]
>
>Les événements qui comportent un remplacement côté client contournent [!DNL Dynamic Datastream Configuration] règles de manière silencieuse, sans erreur ni avertissement. Si vos règles ne correspondent pas aux événements que vous prévoyez qu’elles correspondent, vérifiez si ces événements comportent une payload `edgeConfigOverrides`.

Les configurations de train de données dynamiques et [ remplacements de configuration de train de données](/help/datastreams/overrides.md) s’excluent mutuellement par événement. Lorsqu’un événement est associé à un remplacement côté client envoyé via Web SDK [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) ou [`configure`](/help/collection/js/commands/configure/overview.md), le remplacement est prioritaire et Edge Network ignore [!DNL Dynamic Datastream Configuration] règles pour cet événement.

Planifiez l’implémentation afin d’utiliser une approche ou l’autre par type d’événement. N’utilisez pas les deux. Dans la mesure du possible, utilisez [!DNL Dynamic Datastream Configurations] plutôt que des remplacements côté client. Ils offrent une meilleure visibilité, traçabilité et contrôle.

## Étapes suivantes

- Consultez les [conditions préalables et liste de contrôle de planification](/help/datastreams/dynamic-configurations/prerequisites.md) avant de configurer vos premières règles.
- Lisez [Modèles de configuration de train de données dynamique](/help/datastreams/dynamic-configurations/configuration-patterns.md) pour choisir la bonne stratégie de jeu de données.
- Suivez les étapes de l’interface utilisateur pour [créer [!DNL Dynamic Datastream Configurations]](/help/datastreams/configure-dynamic-datastream.md).

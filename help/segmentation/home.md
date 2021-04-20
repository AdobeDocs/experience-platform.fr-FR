---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; service de segments ; segment ; Segment ; Segments ; segments
solution: Experience Platform
title: Présentation du service de segmentation
topic: overview
description: Découvrez le service de segmentation Adobe Experience Platform et le rôle qu’il joue dans l’écosystème de plateformes.
translation-type: tm+mt
source-git-commit: eff833f20eba4e51579a43fbb98c1e2333e326ef
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 60%

---


# [!DNL Segmentation Service] présentation

Adobe Experience Platform [!DNL Segmentation Service] fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et maintenus de manière centralisée sur [!DNL Platform] et sont facilement accessibles par toute solution d&#39;Adobe.

Ce document donne un aperçu de [!DNL Segmentation Service] et du rôle qu&#39;il joue dans Adobe Experience Platform.

## Prise en main de [!DNL Segmentation Service]

Il est important de comprendre les termes clés suivants utilisés dans ce document :

- **Segmentation** : division d’un grand groupe d’individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou le comportement clés d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Fonctionnement de la segmentation

La segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat.

Une fois qu’un segment a été défini sur le plan conceptuel, il est créé dans [!DNL Experience Platform]. En règle générale, les segments sont créés par le spécialiste du marketing ou des audiences bien que certaines organisations préfèrent qu’ils soient créés par leur service marketing, en collaboration avec leurs analystes de données. Après avoir examiné les données envoyées à [!DNL Platform], l’analyste de données compose la définition de segment en sélectionnant les champs et les valeurs qui seront utilisés pour créer les règles ou conditions du segment. À cet effet, on utilise l’interface utilisateur ou l’API.

## Création de segments

Qu’ils soient créés à l’aide de l’API ou en utilisant [!DNL Segment Builder], les segments sont en fin de compte définis à l’aide de [!DNL Profile Query Language] (PQL). C’est là que la définition conceptuelle du segment est décrite dans le langage conçu pour récupérer les profils répondant aux critères. Pour plus d’informations, voir la [présentation de PQL](./pql/overview.md).

Pour savoir comment créer et utiliser des segments dans [!DNL Segment Builder] (l&#39;implémentation de l&#39;interface utilisateur de [!DNL Segmentation Service]), consultez le [guide du créateur de segments](./ui/overview.md).

Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, consultez le tutoriel sur la [création de segments ciblés à l’aide de l’API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Dans l’éventualité où un schéma est étendu, tous les chargements ultérieurs doivent mettre à jour les nouveaux champs ajoutés en conséquence. Pour plus d&#39;informations sur la personnalisation de [!DNL Experience Data Model] (XDM), consultez le [Schéma Editor tutorial](../xdm/tutorials/create-schema-ui.md).

## Évaluation de segments

La plate-forme prend actuellement en charge trois méthodes d’évaluation des segments : segmentation en flux continu, segmentation par lots et segmentation par arête.

### Segmentation par flux

La segmentation par flux est un processus continu de sélection des données qui met à jour vos segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données d’entrée [!DNL Real-time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui vous permet de vous assurer que votre ciblage d’audience reste pertinent.

Pour plus d’informations sur la segmentation par flux, consultez la [documentation sur la segmentation par flux](./api/streaming-segmentation.md).

### Segmentation par lots

Au lieu d’un processus en continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin que vous puissiez l’exporter pour l’utiliser.

**Segmentation incrémentielle (bêta)**

Les segments de lot sont évalués toutes les 24 heures. Cependant, pour les segments existants, la segmentation incrémentielle maintient les segments à jour jusqu’à une heure.

La segmentation incrémentielle s’exécute sur les nouvelles données arrivant dans le magasin de profils. Toutefois, les avertissements suivants s’appliquent à la segmentation incrémentielle :

- Pour tous les segments nouveaux ou récemment modifiés, les profils contenant de nouvelles données début être qualifiés au cours de la prochaine exécution incrémentielle. Toutefois, les profils sans modification seront rattrapés dans la prochaine tâche de segmentation par lot complète.
- Les segments à plusieurs entités seront actualisés dans la segmentation incrémentielle. S’il existe des mises à jour d’entité, tous les profils contenant de nouvelles données début de les utiliser au cours de la prochaine exécution incrémentielle. Cependant, les profils sans modification seront rattrapés dans la prochaine tâche de segmentation par lots complète.
- Les événements qui abandonnent la fenêtre de temps d’un segment seront rapprochés dans la tâche de segmentation par lots complète suivante.

Pour savoir comment évaluer les segments, consultez le [tutoriel sur l’évaluation des segments](./tutorials/evaluate-a-segment.md).

### Segmentation Edge

La segmentation Edge permet d’évaluer instantanément les segments dans la plate-forme, ce qui permet d’utiliser les mêmes cas de personnalisation de page et de page suivante.

Pour en savoir plus sur la segmentation des arêtes, consultez la [documentation de l&#39;API](./api/edge-segmentation.md) ou la [documentation de l&#39;interface utilisateur](./ui/edge-segmentation.md).

## Accès aux résultats de la segmentation

Pour savoir comment accéder à un segment exporté, consultez le [tutoriel sur l’évaluation des segments](./tutorials/evaluate-a-segment.md).

## Métadonnées de segment

Les métadonnées de segment facilitent l’indexation dans le cas où l’un de vos segments doit être réutilisé et/ou combiné.

La composition de vos segments (via l&#39;API ou [!DNL Segment Builder]) nécessite de définir un nom de segment et une stratégie de fusion.

### Noms de segment

Lors de la création d’un segment, vous devez fournir un nom de segment. Le nom du segment est utilisé pour identifier un segment particulier dans la collection créée par [!DNL Segmentation Service]. Les noms de segment doivent donc être explicites, concis et uniques.

>[!NOTE]
>
>Lors de la planification d’un segment, n’oubliez pas que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec lui. Lorsque vous sélectionnez un nom, pensez à la possibilité que votre segment contienne des portions réutilisables.

### Stratégies de fusion

Les stratégies de fusion sont des règles utilisées par [!DNL Profile] pour déterminer comment les données seront hiérarchisées et combinées dans une vue unifiée dans certaines conditions.
Si aucune stratégie de fusion n&#39;est définie, la stratégie de fusion [!DNL Platform] par défaut est utilisée. Si vous préférez utiliser une stratégie de fusion spécifique à votre organisation, vous pouvez créer la vôtre et la marquer comme valeur par défaut de votre organisation.

Pour plus d&#39;informations sur les stratégies de fusion, consultez le [guide des stratégies de fusion](../profile/api/merge-policies.md).

>[!NOTE]
>
>L’estimation des tailles de l’audience est basée sur la stratégie de fusion de profil par défaut de l’entreprise.

### Autres métadonnées de segment

Outre le nom du segment et la stratégie de fusion, [!DNL Segment Builder] vous offre un champ de métadonnées &quot;description du segment&quot; supplémentaire dans lequel vous pouvez résumer l’objectif de votre définition de segment.

## Fonctionnalités de segmentation avancées

Les segments peuvent être configurés pour générer en permanence une audience en combinant l’[ingestion de données par flux](../ingestion/streaming-ingestion/overview.md) avec l’une des fonctionnalités de segmentation avancées suivantes :
- [Segmentation séquentielle](#sequential)
- [Segmentation dynamique](#dynamic)
- [Segmentation d’entités multiples](#multi-entity)

Ces fonctionnalités avancées sont décrites plus en détail dans les sections suivantes.

## Segmentation séquentielle {#sequential}

Un parcours utilisateur standard est séquentiel par nature. Adobe Experience Platform vous permet de définir une série ordonnée de segments afin de refléter ce parcours, capturant ainsi des séquences de événements au fur et à mesure de leur apparition. Vous pouvez classer les événements dans l’ordre souhaité en utilisant la chronologie du événement visuel dans le [!DNL Segment Builder].

Un exemple de parcours client qui nécessiterait une segmentation séquentielle serait consultation produit > ajout du produit > passage en caisse > pas d’achat.

## Segmentation dynamique {#dynamic}

La segmentation dynamique résout les problèmes d’évolutivité auxquels sont généralement confrontés les spécialistes du marketing lors de la création de segments pour les campagnes marketing.

Contrairement à la segmentation statique qui requiert de capturer de manière explicite et répétée chaque cas d’utilisation possible, la segmentation dynamique utilise des variables pour construire la logique de règle et exprimer de manière dynamique les relations.

### Cas d’utilisation : recherche de clients qui effectuent des achats en dehors de leur État d’origine

Pour illustrer la valeur de cette fonctionnalité de segmentation avancée, imaginez un architecte de données collaborant avec un spécialiste du marketing afin d’identifier les clients qui ont effectué des achats en dehors de leur État d’origine.

**Le problème**

La segmentation statique nécessite de définir des segments individuels dotés d’un attribut unique pour l’État d’origine, avant de filtrer les événements d’achat dont l’état ne correspond pas à l’État d’origine. Un segment explicite de ce type se lirait « Je cherche des personnes de l’Utah dont l’état de leur achat ne correspond pas à Utah ». Pour créer une audience à l’aide de cette méthode, vous devez définir un segment pour chaque État des États-Unis, c’est-à-dire 50 segments.

En raison des différentes combinaisons de segments qui apparaissent inévitablement à mesure que vous évoluez, le processus manuel requis pour la segmentation statique prend plus de temps, ce qui réduit votre efficacité globale.

**La solution**

En attribuant une variable à l’attribut de l’État d’achat, votre segment dynamique simplifie « la recherche d’un achat pour lequel l’État ne correspond pas à l’État d’origine du client ». Vous pouvez ainsi consolider 50 segments statiques en un seul segment dynamique.

## Segmentation d’entités multiples {#multi-entity}

Grâce à la fonction de segmentation multi-entités avancée, vous pouvez étendre les données [!DNL Real-time Customer Profile] à l&#39;aide de données supplémentaires basées sur des produits, des magasins ou d&#39;autres entités autres que des personnes, également connues sous le nom d&#39;entités de &quot;dimension&quot;. Par conséquent, [!DNL Segmentation Service] peut accéder à d’autres champs pendant la définition de segment comme s’ils étaient natifs de la banque de données [!DNL Profile]. La segmentation multientité offre une certaine souplesse lors de l’identification des audiences en fonction de données pertinentes pour vos besoins commerciaux uniques. Pour plus d&#39;informations, y compris les cas d&#39;utilisation et les workflows, consultez le [guide de segmentation multientité](multi-entity-segmentation.md).

## [!DNL Segmentation Service] types de données

[!DNL Segmentation Service] prend en charge divers types de données primitifs et complexes. Vous trouverez des informations détaillées, y compris une liste des types de données pris en charge, dans le [guide des types de données pris en charge](./data-types.md).

## Étapes suivantes

[!DNL Segmentation Service] fournit un processus consolidé pour créer des segments à partir de  [!DNL Real-time Customer Profile] données. En résumé :

- [!DNL Segmentation]La est le processus de définition d’un sous-ensemble de profils de votre banque de profils, ce qui vous permet de caractériser le comportement ou les attributs d’un groupe commercialisable souhaité. [!DNL Segmentation Service] rend ce processus possible.
- Lors de la planification d’un segment, gardez à l’esprit que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec lui.
- Un segment peut être créé à partir de règles basées sur des données de profil, des données de série temporelle associées ou des deux.
- Les segments peuvent être évalués à la demande ou en continu. Lors de l’évaluation à la demande, toutes les données de profil sont transmises simultanément par le biais des définitions de segment. Lorsqu’elles sont évaluées de manière continue, les données sont diffusées par le biais des définitions de segment lors de leur entrée dans [!DNL Platform].

Pour savoir comment définir des segments dans l’interface utilisateur, consultez le [guide du créateur de segments](./ui/overview.md). Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, voir le tutoriel sur la [création de segments à l’aide de l’API](./tutorials/create-a-segment.md).
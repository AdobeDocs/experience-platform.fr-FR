---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;service de segments;segment;Segment;Segments;segments
solution: Experience Platform
title: Présentation de Segmentation Service
description: Découvrez Adobe Experience Platform Segmentation Service et le rôle qu’il occupe dans l’écosystème de Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 97%

---

# Présentation de [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-Time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Platform] et sont facilement accessibles depuis n’importe quelle solution Adobe.

Ce document offre une présentation de [!DNL Segmentation Service] et de son rôle dans Adobe Experience Platform.

## Prise en main de [!DNL Segmentation Service]

Il est important de comprendre les termes clés suivants utilisés dans ce document :

- **Segmentation** : division d’un grand groupe d’individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou le comportement clés d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Fonctionnement de la segmentation

La segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat.

Une fois qu’un segment a été défini sur le plan conceptuel, il est créé dans [!DNL Experience Platform]. En règle générale, les segments sont créés par le spécialiste du marketing ou des audiences bien que certaines organisations préfèrent qu’ils soient créés par leur service marketing, en collaboration avec leurs analystes de données. Après avoir examiné les données envoyées à [!DNL Platform], l’analyste de données compose la définition de segment en sélectionnant les champs et les valeurs qui seront utilisés pour créer les règles ou conditions du segment. À cet effet, on utilise l’interface utilisateur ou l’API.

## Création de segments

Qu’ils soient créés grâce à une API ou au [!DNL Segment Builder], les segments sont finalement définis à l’aide du [!DNL Profile Query Language] (PQL). C’est là que la définition conceptuelle du segment est décrite dans le langage conçu pour récupérer les profils répondant aux critères. Pour plus d’informations, voir la [présentation de PQL](./pql/overview.md).

Pour savoir comment créer et utiliser des segments dans le [!DNL Segment Builder] (l’implémentation de l’interface utilisateur de [!DNL Segmentation Service]), consultez le [guide du créateur de segments](./ui/overview.md).

Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, consultez le tutoriel sur la [création de segments ciblés à l’aide de l’API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Dans l’éventualité où un schéma est étendu, tous les chargements ultérieurs doivent mettre à jour les nouveaux champs ajoutés en conséquence. Pour plus d’informations sur la personnalisation du [!DNL Experience Data Model] (XDM), consultez le [tutoriel de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).
>
>En outre, si une valeur d’expiration d’événement d’expérience est activée sur le jeu de données, cela peut affecter l’appartenance du segment créé. Veuillez lire le guide sur [Expiration des événements d’expérience](../profile/event-expirations.md) pour plus d’informations sur la manière dont cette fonction peut affecter la segmentation.

## Évaluation de segments {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Méthodes d’évaluation"
>abstract="Platform prend actuellement en charge trois méthodes d’évaluation des segments : segmentation par flux, segmentation par lots et segmentation Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Évaluation par diffusion en continu"
>abstract="La segmentation par diffusion en continu est un processus continu de sélection des données qui met à jour vos segments en réponse à l’activité des utilisateurs."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=fr" text="Évaluer les événements en temps quasi réel grâce à la segmentation par flux"

Platform prend actuellement en charge trois méthodes d’évaluation des segments : segmentation par flux, segmentation par lots et segmentation Edge.

### Segmentation par flux {#streaming}

La segmentation par flux est un processus continu de sélection des données qui met à jour vos segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données d’entrée [!DNL Real-Time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui vous permet de vous assurer que votre ciblage d’audience reste pertinent.

Pour plus d’informations sur la segmentation par flux, consultez la [documentation sur la segmentation par flux](./api/streaming-segmentation.md).

### Segmentation par lots {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Évaluation par lots"
>abstract="Au lieu d’un processus en continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créé, le segment est enregistré et stocké afin que vous puissiez l’exporter pour l’utiliser."

Au lieu d’un processus en continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin que vous puissiez l’exporter pour l’utiliser.

Les segments par lot sont automatiquement évalués toutes les 24 heures. Si vous souhaitez évaluer un segment par lot à la demande, vous pouvez utiliser une tâche de segmentation. Pour en savoir plus sur les tâches de segmentation, consultez la [documentation sur les tâches de segmentation](./api/segment-jobs.md).

### Segmentation Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Évaluation Edge"
>abstract="La segmentation Edge permet d’évaluer les segments dans Platform instantanément sur Experience Edge, en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=fr" text="Guide de l’interface utilisateur de segmentation Edge"

La segmentation Edge permet d’évaluer les segments dans Platform instantanément sur [Experience Edge](../edge/home.md), en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante.

Pour en savoir plus sur la segmentation Edge, consultez la [documentation API](./api/edge-segmentation.md) ou la [documentation de l’interface utilisateur](./ui/edge-segmentation.md).

## Accès aux résultats de la segmentation

Pour savoir comment accéder à un segment exporté, consultez le [tutoriel sur l’évaluation des segments](./tutorials/evaluate-a-segment.md).

## Métadonnées de segment

Les métadonnées de segment facilitent l’indexation dans le cas où l’un de vos segments doit être réutilisé et/ou combiné.

La composition de vos segments (par le biais de l’API ou du [!DNL Segment Builder]) requiert que vous définissiez un nom de segment et une stratégie de fusion.

### Noms de segment

Lors de la création d’un segment, vous devez fournir un nom de segment. Le nom de segment permet d’identifier un segment particulier dans la collection créée par [!DNL Segmentation Service]. Les noms de segment doivent donc être explicites, concis et uniques.

>[!NOTE]
>
>Lors de la planification d’un segment, n’oubliez pas que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec lui. Lorsque vous sélectionnez un nom, pensez à la possibilité que votre segment contienne des portions réutilisables.

### Stratégies de fusion

Les stratégies de fusion sont des règles utilisées par [!DNL Profile] pour déterminer comment les données seront hiérarchisées et combinées dans une vue unifiée sous certaines conditions.
Si aucune stratégie de fusion n’est définie, la stratégie de fusion par défaut de [!DNL Platform] est utilisée. Si vous préférez utiliser une stratégie de fusion spécifique à votre organisation, vous pouvez créer la vôtre et la marquer comme valeur par défaut de votre organisation.

Pour plus d’informations sur les stratégies de fusion, consultez le [guide des stratégies de fusion](../profile/api/merge-policies.md).

>[!NOTE]
>
>L’estimation des tailles de l’audience est basée sur la stratégie de fusion de profil par défaut de l’entreprise.

### Autres métadonnées de segment

Outre le nom du segment et la stratégie de fusion, le [!DNL Segment Builder] vous offre un champ de métadonnées « description du segment » supplémentaire dans lequel vous pouvez résumer l’objectif de votre définition de segment.

## Fonctionnalités de segmentation avancées

Les segments peuvent être configurés pour générer en permanence une audience en combinant l’[ingestion de données par flux](../ingestion/streaming-ingestion/overview.md) avec l’une des fonctionnalités de segmentation avancées suivantes :
- [Segmentation séquentielle](#sequential)
- [Segmentation dynamique](#dynamic)
- [Segmentation d’entités multiples](#multi-entity)

Ces fonctionnalités avancées sont décrites plus en détail dans les sections suivantes.

## Segmentation séquentielle {#sequential}

Un parcours utilisateur standard est séquentiel par nature. Adobe Experience Platform vous permet de définir une série ordonnée de segments afin de refléter ce parcours, capturant ainsi des séquences d’événements au fur et à mesure qu’elles se produisent. Vous pouvez organiser les événements dans l’ordre souhaité en utilisant la chronologie visuelle des événements dans le [!DNL Segment Builder].

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

Grâce à la fonction de segmentation d’entités multiples avancée, vous pouvez élargir les données [!DNL Real-Time Customer Profile] avec des données supplémentaires basées sur des produits, des boutiques ou d’autres personnes non-personnes, également appelées entités « de dimension ». Par conséquent, [!DNL Segmentation Service] peut accéder à d’autres champs pendant la définition de segment comme s’ils étaient natifs de la banque de données de [!DNL Profile]. La segmentation d’entités multiples offre une certaine souplesse dans l’identification des audiences en fonction des données qui correspondent à vos propres besoins commerciaux. Pour plus d’informations, notamment sur les cas d’utilisation et les workflows, consultez le [guide de segmentation d’entités multiples](multi-entity-segmentation.md).

## [!DNL Segmentation Service] types de données

[!DNL Segmentation Service] prend en charge divers types de données primitives et complexes. Vous trouverez des informations détaillées, notamment une liste des types de données pris en charge, dans le [guide des types de données pris en charge](./data-types.md).

## Étapes suivantes

[!DNL Segmentation Service] fournit un workflow consolidé pour créer des segments à partir de données de [!DNL Real-Time Customer Profile]. En résumé :

- La [!DNL Segmentation] est le processus de définition d’un sous-ensemble de profils de votre banque de profils, ce qui vous permet de caractériser le comportement ou les attributs d’un groupe commercialisable souhaité. [!DNL Segmentation Service] rend ce processus possible.
- Lors de la planification d’un segment, gardez à l’esprit que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec lui.
- Un segment peut être créé à partir de règles basées sur des données de profil, des données de série temporelle associées ou des deux.
- Les segments peuvent être évalués à la demande ou en continu. Lors de l’évaluation à la demande, toutes les données de profil sont transmises simultanément par le biais des définitions de segment. Lorsqu’elles sont évaluées de manière continue, les données sont diffusées par le biais des définitions de segment lors de leur entrée dans [!DNL Platform].

Pour savoir comment définir des segments dans l’interface utilisateur, consultez le [guide du créateur de segments](./ui/overview.md). Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, voir le tutoriel sur la [création de segments à l’aide de l’API](./tutorials/create-a-segment.md).

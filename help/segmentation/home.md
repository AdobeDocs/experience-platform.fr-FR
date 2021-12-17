---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;segmentation;service de segments;segment;segment;segments;segments;segments
solution: Experience Platform
title: Présentation de Segmentation Service
topic-legacy: overview
description: Découvrez Adobe Experience Platform Segmentation Service et le rôle qu’il joue dans l’écosystème de Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 3130d9731a53c01fb7bc15265e044191ceae47f6
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 62%

---

# Présentation de [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos [!DNL Real-time Customer Profile] data. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Platform], et sont facilement accessibles par toute solution d’Adobe.

Ce document présente les [!DNL Segmentation Service] et le rôle qu’il joue dans Adobe Experience Platform.

## Prise en main de [!DNL Segmentation Service]

Il est important de comprendre les termes clés suivants utilisés dans ce document :

- **Segmentation** : division d’un grand groupe d’individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou le comportement clés d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Fonctionnement de la segmentation

La segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat.

Une fois qu’un segment a été défini sur le plan conceptuel, il est intégré à [!DNL Experience Platform]. En règle générale, les segments sont créés par le spécialiste du marketing ou des audiences bien que certaines organisations préfèrent qu’ils soient créés par leur service marketing, en collaboration avec leurs analystes de données. Lors de la révision des données envoyées à [!DNL Platform], l’analyste de données compose la définition de segment en sélectionnant les champs et les valeurs qui seront utilisés pour créer les règles ou conditions du segment. À cet effet, on utilise l’interface utilisateur ou l’API.

## Création de segments

Création à l’aide de l’API ou à l’aide de la variable [!DNL Segment Builder], les segments sont définis ultimement à l’aide de [!DNL Profile Query Language] (PQL). C’est là que la définition conceptuelle du segment est décrite dans le langage conçu pour récupérer les profils répondant aux critères. Pour plus d’informations, voir la [présentation de PQL](./pql/overview.md).

Pour savoir comment créer et utiliser des segments dans le [!DNL Segment Builder] (l’implémentation de l’interface utilisateur de [!DNL Segmentation Service]), voir [Guide du créateur de segments](./ui/overview.md).

Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, consultez le tutoriel sur la [création de segments ciblés à l’aide de l’API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Dans l’éventualité où un schéma est étendu, tous les chargements ultérieurs doivent mettre à jour les nouveaux champs ajoutés en conséquence. Pour plus d’informations sur la personnalisation [!DNL Experience Data Model] (XDM), rendez-vous sur la page [Tutoriel de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).
>
>En outre, si la durée de vie (TTL) est activée sur le jeu de données, cela peut affecter l’adhésion au segment créé. Pour plus d’informations sur la durée de vie et son impact sur la segmentation, consultez la section [Guide TTL de Profile Service](../profile/apply-ttl.md).

## Évaluation de segments

Platform prend actuellement en charge trois méthodes d’évaluation des segments : segmentation par flux, segmentation par lots et segmentation par périphérie.

### Segmentation par flux

La segmentation par flux est un processus continu de sélection des données qui met à jour vos segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données d’entrée [!DNL Real-time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui vous permet de vous assurer que votre ciblage d’audience reste pertinent.

Pour plus d’informations sur la segmentation par flux, consultez la [documentation sur la segmentation par flux](./api/streaming-segmentation.md).

### Segmentation par lots

Au lieu d’un processus en continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin que vous puissiez l’exporter pour l’utiliser.

Les segments par lot sont automatiquement évalués toutes les 24 heures. Si vous souhaitez évaluer un segment par lot à la demande, vous pouvez utiliser une tâche de segmentation. Pour en savoir plus sur les tâches de segmentation, veuillez lire le [documentation sur les tâches de segmentation](./api/segment-jobs.md).

### Segmentation Edge

La segmentation Edge permet d’évaluer instantanément les segments dans Platform sur Experience Edge, en activant les cas d’utilisation de la personnalisation de la même page et de la page suivante.

Pour en savoir plus sur la segmentation Edge, veuillez lire l’un des [Documentation des API](./api/edge-segmentation.md) ou le [Documentation de l’interface utilisateur](./ui/edge-segmentation.md).

## Accès aux résultats de la segmentation

Pour savoir comment accéder à un segment exporté, consultez le [tutoriel sur l’évaluation des segments](./tutorials/evaluate-a-segment.md).

## Métadonnées de segment

Les métadonnées de segment facilitent l’indexation dans le cas où l’un de vos segments doit être réutilisé et/ou combiné.

la composition de vos segments (via l’API ou [!DNL Segment Builder]) requiert que vous définissiez un nom de segment et une stratégie de fusion.

### Noms de segment

Lors de la création d’un segment, vous devez fournir un nom de segment. Le nom du segment permet d’identifier un segment particulier dans la collection créée par [!DNL Segmentation Service]. Les noms de segment doivent donc être explicites, concis et uniques.

>[!NOTE]
>
>Lors de la planification d’un segment, n’oubliez pas que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec lui. Lorsque vous sélectionnez un nom, pensez à la possibilité que votre segment contienne des portions réutilisables.

### Stratégies de fusion

Les stratégies de fusion sont des règles utilisées par [!DNL Profile] pour déterminer comment les données seront hiérarchisées et combinées dans une vue unifiée sous certaines conditions.
Si aucune stratégie de fusion n’est définie, la valeur par défaut [!DNL Platform] la stratégie de fusion est utilisée. Si vous préférez utiliser une stratégie de fusion spécifique à votre organisation, vous pouvez créer la vôtre et la marquer comme valeur par défaut de votre organisation.

Vous trouverez plus d’informations sur les stratégies de fusion dans la section [guide des stratégies de fusion](../profile/api/merge-policies.md).

>[!NOTE]
>
>L’estimation des tailles de l’audience est basée sur la stratégie de fusion de profil par défaut de l’entreprise.

### Autres métadonnées de segment

Outre le nom du segment et la stratégie de fusion, [!DNL Segment Builder] offre un champ de métadonnées &quot;description du segment&quot; supplémentaire dans lequel vous pouvez résumer l’objectif de votre définition de segment.

## Fonctionnalités de segmentation avancées

Les segments peuvent être configurés pour générer en permanence une audience en combinant l’[ingestion de données par flux](../ingestion/streaming-ingestion/overview.md) avec l’une des fonctionnalités de segmentation avancées suivantes :
- [Segmentation séquentielle](#sequential)
- [Segmentation dynamique](#dynamic)
- [Segmentation d’entités multiples](#multi-entity)

Ces fonctionnalités avancées sont décrites plus en détail dans les sections suivantes.

## Segmentation séquentielle {#sequential}

Un parcours utilisateur standard est séquentiel par nature. Adobe Experience Platform vous permet de définir une série ordonnée de segments pour refléter ce parcours, capturant ainsi des séquences d’événements au fur et à mesure qu’elles se produisent. Vous pouvez organiser les événements dans l’ordre souhaité à l’aide de la chronologie visuelle des événements dans la [!DNL Segment Builder].

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

Grâce à la fonction de segmentation d’entités multiples avancée, vous pouvez étendre [!DNL Real-time Customer Profile] données avec des données supplémentaires basées sur des produits, des magasins ou d’autres personnes non concernées, également appelées entités &quot;de dimension&quot;. Par conséquent, [!DNL Segmentation Service] peut accéder à des champs supplémentaires lors de la définition de segment comme s’ils étaient natifs de la fonction [!DNL Profile] entrepôt de données. La segmentation d’entités multiples offre une certaine souplesse lors de l’identification des audiences en fonction de données pertinentes pour vos besoins commerciaux uniques. Pour plus d’informations, notamment sur les cas pratiques et les workflows, reportez-vous à la section [guide de segmentation d’entités multiples](multi-entity-segmentation.md).

## [!DNL Segmentation Service] types de données

[!DNL Segmentation Service] prend en charge divers types de données primitifs et complexes. Vous trouverez des informations détaillées, notamment une liste des types de données pris en charge dans la section [guide sur les types de données pris en charge](./data-types.md).

## Étapes suivantes

[!DNL Segmentation Service] fournit un processus consolidé à partir duquel créer des segments [!DNL Real-time Customer Profile] data. En résumé :

- [!DNL Segmentation]La est le processus de définition d’un sous-ensemble de profils de votre banque de profils, ce qui vous permet de caractériser le comportement ou les attributs d’un groupe commercialisable souhaité. [!DNL Segmentation Service] rend ce processus possible.
- Lors de la planification d’un segment, gardez à l’esprit que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec lui.
- Un segment peut être créé à partir de règles basées sur des données de profil, des données de série temporelle associées ou des deux.
- Les segments peuvent être évalués à la demande ou en continu. Lors de l’évaluation à la demande, toutes les données de profil sont transmises simultanément par le biais des définitions de segment. Lorsqu’elles sont évaluées de manière continue, les données sont diffusées par le biais des définitions de segment lors de leur entrée dans [!DNL Platform].

Pour savoir comment définir des segments dans l’interface utilisateur, consultez le [guide du créateur de segments](./ui/overview.md). Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, voir le tutoriel sur la [création de segments à l’aide de l’API](./tutorials/create-a-segment.md).

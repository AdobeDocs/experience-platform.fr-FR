---
solution: Experience Platform
title: Présentation de Segmentation Service
description: Découvrez Adobe Experience Platform Segmentation Service et le rôle qu’il occupe dans l’écosystème de Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 44c92e2163e2b6c0c140c64bba41dfbcc15d5d7f
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 50%

---

# Présentation de [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] fournit une interface utilisateur et une API RESTful qui vous permettent de créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos [!DNL Real-Time Customer Profile] data. Ces audiences sont configurées et gérées de manière centralisée sur [!DNL Platform], et sont facilement accessibles par toute solution d’Adobe.

Ce document offre une présentation de [!DNL Segmentation Service] et de son rôle dans Adobe Experience Platform.

## Prise en main de [!DNL Segmentation Service]

Vous devez comprendre les termes clés suivants utilisés dans ce document :

- **Segmentation** : division d’un grand groupe d’individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.
- **Audience**: un groupe de personnes qui partagent des comportements et/ou des caractéristiques similaires. Cette collection de personnes peut être générée par Adobe Experience Platform à l’aide de définitions de segment (audience générée par Platform) ou à partir de sources externes (audience générée en externe).
- **Définition de segment**: le jeu de règles utilisé par Adobe Experience Platform pour décrire les caractéristiques ou le comportement clés d’une audience cible.

## Fonctionnement de la segmentation

La segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat.

Une fois qu’une audience a été définie sur le plan conceptuel, elle est intégrée à [!DNL Experience Platform]. En règle générale, les audiences sont créées par le spécialiste du marketing ou de l’audience bien que certaines organisations préfèrent qu’elles soient créées par leur service marketing, en collaboration avec leurs analystes de données. Lors de la révision des données envoyées à [!DNL Platform], l’analyste de données peut créer l’audience de deux manières : soit en créant une définition de segment en sélectionnant les champs et les valeurs qui seront utilisés pour créer les règles ou les conditions de l’audience, soit en composant une audience à l’aide de la Composition de l’audience.

## Création d’audiences

Les audiences peuvent être créées de deux manières différentes sur Adobe Experience Platform : soit directement composées en tant qu’audiences, soit par le biais de définitions de segment dérivées de Platform.

### Composition de l’audience

Lorsque vous composez directement une audience sur Platform, vous pouvez utiliser la composition de l’audience. Pour savoir comment utiliser la composition d’audience pour créer une audience, veuillez lire le [Guide sur la composition de l’audience](./ui/audience-composition.md) pour plus d’informations.

### Définitions de segment

Création à l’aide de l’API ou à l’aide de la variable [!DNL Segment Builder], les définitions de segment sont définies au final à l’aide de [!DNL Profile Query Language] (PQL). C’est là que la définition conceptuelle du segment est décrite dans le langage conçu pour récupérer les profils répondant aux critères. Pour plus d’informations, voir la [présentation de PQL](./pql/overview.md).

Pour savoir comment créer et utiliser des segments dans le [!DNL Segment Builder] (l’implémentation de l’interface utilisateur de [!DNL Segmentation Service]), consultez le [guide du créateur de segments](./ui/overview.md).

Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, consultez le tutoriel sur [création de définitions de segment à l’aide de l’API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Dans l’éventualité où un schéma est étendu, tous les chargements ultérieurs doivent mettre à jour les nouveaux champs ajoutés en conséquence. Pour plus d’informations sur la personnalisation du [!DNL Experience Data Model] (XDM), consultez le [tutoriel de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).
>
>En outre, si une valeur d’expiration d’événement d’expérience est activée sur le jeu de données, cela peut affecter l’appartenance à la définition de segment créée. Veuillez lire le guide sur l’[expiration des événements d’expérience](../profile/event-expirations.md) pour plus d’informations sur la manière dont cette fonctionnalité peut affecter la segmentation.

## Évaluation des audiences {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Méthodes d’évaluation"
>abstract="Platform prend actuellement en charge trois méthodes d’évaluation des audiences : segmentation en flux continu, segmentation par lots et segmentation Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Évaluation par diffusion en continu"
>abstract="La segmentation par flux est un processus continu de sélection des données qui met à jour vos audiences en réponse à l’activité des utilisateurs et utilisatrices."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=fr" text="Évaluer les événements en temps quasi réel grâce à la segmentation par flux"

Platform prend actuellement en charge trois méthodes d’évaluation des audiences : segmentation en flux continu, segmentation par lots et segmentation Edge.

### Segmentation en flux continu {#streaming}

La segmentation par flux est un processus continu de sélection des données qui met à jour vos audiences en réponse à l’activité des utilisateurs et utilisatrices. Une fois qu’une audience a été créée et enregistrée, la définition de segment est appliquée aux données entrantes vers [!DNL Real-Time Customer Profile]. Les ajouts et les suppressions à l’audience sont traités régulièrement, ce qui vous permet de vous assurer que l’audience cible reste pertinente.

Pour plus d’informations sur la segmentation par flux, consultez la [documentation sur la segmentation par flux](./api/streaming-segmentation.md).

### Segmentation par lots {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Évaluation par lots"
>abstract="Au lieu d’un processus en continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créée, l’audience est enregistrée et stockée afin que vous puissiez l&#39;exporter pour l’utiliser."

Au lieu d’un processus en continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créée, l&#39;audience obtenue est enregistrée et stockée afin que vous puissiez l&#39;exporter pour l&#39;utiliser.

Les audiences par lots sont automatiquement évaluées toutes les 24 heures. Si vous souhaitez évaluer une audience par lots à la demande, vous pouvez utiliser une tâche de segmentation. Pour en savoir plus sur les tâches de segmentation, consultez la [documentation sur les tâches de segmentation](./api/segment-jobs.md).

### Segmentation Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Évaluation Edge"
>abstract="La segmentation Edge permet d’évaluer les segments dans Platform instantanément sur Experience Edge, en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=fr" text="Guide de l’interface utilisateur de segmentation Edge"

La segmentation Edge permet d’évaluer les segments dans Platform instantanément sur [Experience Edge](../edge/home.md), en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante.

Pour en savoir plus sur la segmentation Edge, consultez la [documentation API](./api/edge-segmentation.md) ou la [documentation de l’interface utilisateur](./ui/edge-segmentation.md).

## Accès aux résultats de la segmentation

Pour savoir comment accéder à une audience exportée, reportez-vous au [tutoriel sur l’évaluation de la définition de segment](./tutorials/evaluate-a-segment.md).

## Métadonnées de définition de segment

Les métadonnées de définition de segment facilitent l’indexation dans le cas où l’une de vos audiences doit être réutilisée et/ou combinée.

Composition d’une définition de segment (via l’API ou [!DNL Segment Builder]) requiert que vous définissiez un nom et une stratégie de fusion.

### Noms de définition de segment

Lors de la création d’une définition de segment, vous devez fournir un nom. Le nom de la définition de segment est utilisé pour identifier une définition de segment spécifique dans la collection créée par [!DNL Segmentation Service]. Les noms des définitions de segment doivent donc être descriptifs, concis et uniques.

>[!NOTE]
>
>Lors de la planification d’une définition de segment, n’oubliez pas que les définitions de segment peuvent être référencées à partir de n’importe quelle autre définition de segment et combinées avec elle. Lorsque vous sélectionnez un nom, envisagez la possibilité que votre définition de segment contienne des portions réutilisables.

### Politiques de fusion

Les politiques de fusion sont des règles utilisées par [!DNL Profile] pour déterminer comment les données seront hiérarchisées et combinées dans une vue unifiée sous certaines conditions.

Si aucune politique de fusion n’est définie, la politique de fusion par défaut de [!DNL Platform] est utilisée. Si vous préférez utiliser une politique de fusion spécifique à votre organisation, vous pouvez créer la vôtre et la marquer comme valeur par défaut de votre organisation.

Pour plus d’informations sur les politiques de fusion, consultez le [guide des politiques de fusion](../profile/api/merge-policies.md).

>[!NOTE]
>
>L’estimation des tailles de l’audience est basée sur la politique de fusion de profil par défaut de l’entreprise.

### Autres métadonnées de définition de segment

En plus de la stratégie de nom et de fusion, [!DNL Segment Builder] offre un champ de métadonnées de description supplémentaire dans lequel vous pouvez résumer l’objectif de votre définition de segment.

## Fonctionnalités de segmentation avancées

Les définitions de segment peuvent être configurées pour générer continuellement une audience en combinant [ingestion de données par flux](../ingestion/streaming-ingestion/overview.md) avec l’une des fonctionnalités de segmentation avancées suivantes :
- [Segmentation séquentielle](#sequential)
- [Segmentation dynamique](#dynamic)
- [Segmentation d’entités multiples](#multi-entity)

Ces fonctionnalités avancées sont décrites plus en détail dans les sections suivantes.

### Segmentation séquentielle {#sequential}

Un parcours utilisateur standard est séquentiel par nature. Adobe Experience Platform vous permet de définir une série ordonnée d’audiences pour refléter ce parcours, capturant ainsi des séquences d’événements au fur et à mesure qu’elles se produisent. Vous pouvez organiser les événements dans l’ordre souhaité en utilisant la chronologie visuelle des événements dans le [!DNL Segment Builder].

Un exemple de parcours client qui nécessiterait une segmentation séquentielle serait consultation produit > ajout du produit > passage en caisse > pas d’achat.

### Segmentation dynamique {#dynamic}

La segmentation dynamique résout les problèmes d’évolutivité auxquels sont généralement confrontés les spécialistes du marketing lors de la création d’audiences pour les campagnes marketing.

Contrairement à la segmentation statique qui requiert de capturer de manière explicite et répétée chaque cas d’utilisation possible, la segmentation dynamique utilise des variables pour construire la logique de règle et exprimer de manière dynamique les relations.

Pour illustrer la valeur de cette fonctionnalité de segmentation avancée, imaginez un architecte de données collaborant avec un spécialiste du marketing afin d’identifier les clients qui ont effectué des achats en dehors de leur État d’origine.

La segmentation statique nécessite de définir des segments individuels dotés d’un attribut unique pour l’État d’origine, avant de filtrer les événements d’achat dont l’état ne correspond pas à l’État d’origine. Une définition de segment explicite de ce type serait &quot;Je recherche des personnes de l’Utah dont l’état de leur achat n’est pas Utah&quot;. Pour créer une audience à l’aide de cette méthode, vous devez définir une définition de segment pour chaque état des États-Unis, pour un total de 50 segments.

En raison des différentes combinaisons de définitions de segment qui apparaissent inévitablement à mesure que vous évoluez, le processus manuel requis pour la segmentation statique prend plus de temps, ce qui réduit votre efficacité globale.

En attribuant une variable à l’attribut purchase state , votre définition de segment dynamique simplifie &quot;la recherche d’un achat pour lequel l’état de cet achat n’est pas égal à l’état d’origine du client&quot;. Vous pouvez ainsi consolider 50 segments statiques en une seule définition de segment dynamique.

### Segmentation d’entités multiples {#multi-entity}

Grâce à la fonction de segmentation d’entités multiples avancée, vous pouvez élargir les données [!DNL Real-Time Customer Profile] avec des données supplémentaires basées sur des produits, des boutiques ou d’autres personnes non-personnes, également appelées entités « de dimension ». Par conséquent, [!DNL Segmentation Service] peut accéder à d’autres champs pendant la définition de segment comme s’ils étaient natifs de la banque de données de [!DNL Profile]. La segmentation d’entités multiples offre une certaine souplesse dans l’identification des audiences en fonction des données qui correspondent à vos propres besoins commerciaux. Pour plus d’informations, notamment sur les cas d’utilisation et les workflows, consultez le [guide de segmentation d’entités multiples](multi-entity-segmentation.md).

## [!DNL Segmentation Service] types de données

[!DNL Segmentation Service] prend en charge divers types de données primitives et complexes. Vous trouverez des informations détaillées, notamment une liste des types de données pris en charge, dans le [guide des types de données pris en charge](./data-types.md).

## Étapes suivantes

[!DNL Segmentation Service] fournit un processus consolidé pour créer des audiences à partir de [!DNL Real-Time Customer Profile] data.

Pour plus d’informations sur l’utilisation de l’interface utilisateur de Segmentation Service, veuillez lire le [Présentation de l’interface utilisateur de Segmentation Service](./ui/overview.md).

Pour savoir comment composer des audiences dans l’interface utilisateur, veuillez lire le [Guide sur la composition de l’audience](./ui/audience-composition.md). Pour savoir comment définir des définitions de segment dans l’interface utilisateur, voir [Guide du créateur de segments](./ui/overview.md). Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, consultez le tutoriel sur [création de définitions de segment à l’aide de l’API](./tutorials/create-a-segment.md).

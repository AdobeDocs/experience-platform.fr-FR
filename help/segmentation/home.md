---
solution: Experience Platform
title: Présentation de Segmentation Service
description: Découvrez Adobe Experience Platform Segmentation Service et le rôle qu’il occupe dans l’écosystème de Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 95%

---

# Présentation de [!DNL Segmentation Service]

Le [!DNL Segmentation Service] d’Adobe Experience Platform fournit une interface utilisateur et une API RESTful qui vous permettent de créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

Ce document offre une présentation de [!DNL Segmentation Service] et de son rôle dans Adobe Experience Platform.

## Prise en main de [!DNL Segmentation Service]

Vous devez comprendre les termes clés suivants utilisés dans ce document :

- **Segmentation** : division d’un grand groupe de personnes (tels que des clientes et des clients, des prospects, des utilisateurs et des utilisatrices ou des organisations) en groupes plus petits partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.
- **Audience** : un groupe de personnes qui partagent des comportements et/ou des caractéristiques similaires. Ce groupe de personnes peut être généré par Adobe Experience Platform à l’aide de définitions de segment (audience générée par Platform) ou à partir de sources externes (audience générée en externe).
- **Définition de segment** : l’ensemble des règles utilisées par Adobe Experience Platform pour décrire les caractéristiques ou le comportement clés d’une audience cible.

## Fonctionnement de la segmentation

La segmentation est le processus de définition d’attributs ou de comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de clients potentiels de votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat.

Une fois qu’une audience a été définie sur le plan conceptuel, elle est créée dans [!DNL Experience Platform]. En règle générale, les audiences sont créées par la personne spécialiste du marketing ou des audiences, bien que certaines organisations préfèrent qu’elles soient créées par leur propre service marketing, en collaboration avec leur propre personnel chargé de l’analyse des données. Lors de la révision des données envoyées à [!DNL Platform], la personne qui analyse les données peut créer l’audience de deux manières. Elle peut créer une définition de segment en sélectionnant les champs et les valeurs qui seront utilisés pour créer les règles ou les conditions de l’audience, ou composer une audience à l’aide de la composition de l’audience.

## Créer des audiences

Les audiences peuvent être créées de deux manières différentes sur Adobe Experience Platform : elles peuvent être directement composées en tant qu’audiences ou par le biais de définitions de segment dérivées de Platform.

### Composition de l’audience

Lorsque vous composez directement une audience sur Platform, utilisez la composition de l’audience. Pour savoir comment utiliser la fonctionnalité de composition d’audience pour créer une audience, consultez le [Guide de la composition d’audience](./ui/audience-composition.md).

### Définitions de segment

Qu’elles soient créées grâce à une API ou au [!DNL Segment Builder], les définitions de segments sont finalement définies à l’aide du [!DNL Profile Query Language] (PQL). C’est là que la définition conceptuelle du segment est décrite dans le langage conçu pour récupérer les profils répondant aux critères. Pour plus d’informations, voir la [présentation de PQL](./pql/overview.md).

Pour savoir comment créer et utiliser des segments dans le [!DNL Segment Builder] (l’implémentation de l’interface utilisateur de [!DNL Segmentation Service]), consultez le [guide du créateur de segments](./ui/overview.md).

Pour plus d’informations sur la création de définitions de segments à l’aide de l’API, suivez le tutoriel sur la [création de définitions de segments à l’aide de l’API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Dans l’éventualité où un schéma est étendu, tous les chargements ultérieurs doivent mettre à jour les nouveaux champs ajoutés en conséquence. Pour plus d’informations sur la personnalisation du [!DNL Experience Data Model] (XDM), consultez le [tutoriel de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).
>
>En outre, si une valeur d’expiration de l’événement d’expérience est activée sur le jeu de données, cela peut affecter l’appartenance de la définition de segment créée. Veuillez lire le guide sur l’[expiration des événements d’expérience](../profile/event-expirations.md) pour plus d’informations sur la manière dont cette fonctionnalité peut affecter la segmentation.

## Évaluer les audiences {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Méthodes d’évaluation"
>abstract="Platform prend actuellement en charge trois méthodes d’évaluation des audiences : segmentation en flux continu, segmentation par lots et segmentation Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Évaluation par diffusion en continu"
>abstract="La segmentation en flux continu est un processus continu de sélection des données qui met à jour vos audiences en réponse à l’activité des utilisateurs et des utilisatrices."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=fr" text="Évaluer les événements en temps quasi réel grâce à la segmentation par flux"

Platform prend actuellement en charge trois méthodes d’évaluation des audiences : segmentation en flux continu, segmentation par lots et segmentation Edge.

### Segmentation en flux continu {#streaming}

La segmentation en flux continu est un processus continu de sélection des données qui met à jour vos audiences en réponse à l’activité des utilisateurs et des utilisatrices. Une fois qu’une audience a été créée et enregistrée, la définition de segment est appliquée aux données entrantes dans [!DNL Real-Time Customer Profile]. Les ajouts et les suppressions de l’audience sont traités régulièrement, ce qui vous permet de vous assurer que l’audience cible reste pertinente.

Pour plus d’informations sur la segmentation par flux, consultez la [documentation sur la segmentation par flux](./api/streaming-segmentation.md).

### Segmentation par lots {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Évaluation par lots"
>abstract="Au lieu d’un processus en continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créée, l’audience est enregistrée et stockée. Exportez-la ensuite pour l’utiliser."

Au lieu d’un processus continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créée, l’audience obtenue est enregistrée et stockée afin que vous puissiez l’exporter pour l’utiliser.

Les audiences par lots sont automatiquement évaluées toutes les 24 heures. Si vous souhaitez évaluer une audience par lots à la demande, vous pouvez utiliser une tâche de segment. Pour en savoir plus sur les tâches de segmentation, consultez la [documentation sur les tâches de segmentation](./api/segment-jobs.md).

### Segmentation Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Évaluation Edge"
>abstract="La segmentation Edge permet d’évaluer instantanément les segments dans Platform sur l’Edge Network, en activant les cas d’utilisation de la personnalisation de la même page et de la page suivante."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=fr" text="Guide de l’interface utilisateur de segmentation Edge"

La segmentation Edge permet d’évaluer instantanément les segments dans Platform. [sur l’Edge Network](../web-sdk/home.md), activation des cas d’utilisation de la personnalisation de la même page et de la page suivante.

Pour en savoir plus sur la segmentation Edge, consultez la [documentation API](./api/edge-segmentation.md) ou la [documentation de l’interface utilisateur](./ui/edge-segmentation.md).

## Accéder aux résultats de la segmentation

Pour savoir comment accéder à une audience exportée, consultez le [tutoriel sur l’évaluation de la définition de segments](./tutorials/evaluate-a-segment.md).

## Métadonnées de définition de segment

Les métadonnées de définition de segment facilitent l’indexation dans le cas où l’une de vos audiences doit être réutilisée et/ou combinée.

La composition d’une définition de segments (par le biais de l’API ou du [!DNL Segment Builder]) requiert que vous définissiez un nom et une politique de fusion.

### Noms de définition de segment

Lors de la création d’une nouvelle définition de segment, vous devez fournir un nom. Le nom de la définition de segment permet d’identifier une définition de segment particulière dans la collection créée par [!DNL Segmentation Service]. Les noms de définition de segment doivent donc être explicites, concis et uniques.

>[!NOTE]
>
>Lors de la planification d’une définition de segment, n’oubliez pas que les définitions de segments peuvent être référencées à partir de n’importe quelle autre définition de segment et combinées avec elle. Lorsque vous sélectionnez un nom, pensez à la possibilité que votre définition de segment contienne des portions réutilisables.

### Politiques de fusion

Les politiques de fusion sont des règles utilisées par [!DNL Profile] pour déterminer comment les données seront hiérarchisées et combinées dans une vue unifiée sous certaines conditions.

Si aucune politique de fusion n’est définie, la politique de fusion par défaut de [!DNL Platform] est utilisée. Si vous préférez utiliser une politique de fusion spécifique à votre organisation, vous pouvez créer la vôtre et la marquer comme valeur par défaut de votre organisation.

Pour plus d’informations sur les politiques de fusion, consultez le [guide des politiques de fusion](../profile/api/merge-policies.md).

>[!NOTE]
>
>L’estimation des tailles de l’audience est basée sur la politique de fusion de profil par défaut de l’entreprise.

### Autres métadonnées de définition de segment

Outre le nom et la politique de fusion, le [!DNL Segment Builder] vous offre un champ de métadonnées de description supplémentaire dans lequel vous pouvez résumer l’objectif de votre définition de segment.

## Fonctionnalités de segmentation avancées

Les définitions de segment peuvent être configurées pour générer une audience en continu en combinant l’[ingestion de données en flux continu](../ingestion/streaming-ingestion/overview.md) avec l’une des fonctionnalités de segmentation avancées suivantes :
- [Segmentation séquentielle](#sequential)
- [Segmentation dynamique](#dynamic)
- [Segmentation d’entités multiples](#multi-entity)

Ces fonctionnalités avancées sont décrites plus en détail dans les sections suivantes.

### Segmentation séquentielle {#sequential}

Un parcours utilisateur standard est séquentiel par nature. Adobe Experience Platform vous permet de définir une série ordonnée d’audiences afin de refléter ce parcours, capturant ainsi des séquences d’événements au fur et à mesure qu’elles se produisent. Vous pouvez organiser les événements dans l’ordre souhaité en utilisant la chronologie visuelle des événements dans le [!DNL Segment Builder].

Un exemple de parcours client qui nécessiterait une segmentation séquentielle serait consultation produit > ajout du produit > passage en caisse > pas d’achat.

### Segmentation dynamique {#dynamic}

La segmentation dynamique résout les problèmes d’évolutivité auxquels sont généralement confrontées les personnes spécialistes du marketing lors de la création d’audiences pour les campagnes marketing.

Contrairement à la segmentation statique qui requiert de capturer de manière explicite et répétée chaque cas d’utilisation possible, la segmentation dynamique utilise des variables pour construire la logique de règle et exprimer de manière dynamique les relations.

Pour illustrer la valeur de cette fonctionnalité de segmentation avancée, imaginez un architecte de données collaborant avec un spécialiste du marketing afin d’identifier les clientes et les clients qui ont effectué des achats en dehors de leur État d’origine.

La segmentation statique nécessite de définir des segments individuels dotés d’un attribut unique pour l’État d’origine, avant de filtrer les événements d’achat dont l’État ne correspond pas à l’État d’origine. Une définition de segment explicite de ce type se lirait « Je cherche des personnes de l’Utah dont l’État de l’achat ne correspond pas à l’Utah ». Pour créer une audience à l’aide de cette méthode, vous devez définir une définition de segment pour chaque État des États-Unis, c’est-à-dire 50 segments.

En raison des différentes combinaisons de définitions de segments qui apparaissent inévitablement à mesure que vous évoluez, le processus manuel requis pour la segmentation statique prend plus de temps, ce qui réduit votre efficacité globale.

En attribuant une variable à l’attribut de l’État d’achat, votre définition de segment dynamique simplifie « la recherche d’un achat pour lequel l’État ne correspond pas à l’État d’origine du client ou de la cliente ». Vous pouvez ainsi consolider 50 segments statiques en une seule définition de segment dynamique.

### Segmentation d’entités multiples {#multi-entity}

Grâce à la fonction de segmentation d’entités multiples avancée, vous pouvez élargir les données [!DNL Real-Time Customer Profile] avec des données supplémentaires basées sur des produits, des boutiques ou d’autres personnes non-personnes, également appelées entités « de dimension ». Par conséquent, [!DNL Segmentation Service] peut accéder à d’autres champs pendant la définition de segment comme s’ils étaient natifs de la banque de données de [!DNL Profile]. La segmentation d’entités multiples offre une certaine souplesse dans l’identification des audiences en fonction des données qui correspondent à vos propres besoins commerciaux. Pour plus d’informations, notamment sur les cas d’utilisation et les workflows, consultez le [guide de segmentation d’entités multiples](multi-entity-segmentation.md).

## [!DNL Segmentation Service] types de données

[!DNL Segmentation Service] prend en charge divers types de données primitives et complexes. Vous trouverez des informations détaillées, notamment une liste des types de données pris en charge, dans le [guide des types de données pris en charge](./data-types.md).

## Étapes suivantes

[!DNL Segmentation Service] fournit un workflow consolidé pour créer des audiences à partir de données de [!DNL Real-Time Customer Profile].

Pour plus d’informations sur l’utilisation de l’IU de Segmentation Service, consultez la [Vue d’ensemble de l’IU de Segmentation Service](./ui/overview.md).

Pour savoir comment composer des audiences dans l’IU, consultez le [guide de la composition des audiences](./ui/audience-composition.md). Pour savoir comment définir des définitions de segments dans l’IU, consultez le [guide du créateur de segments](./ui/overview.md). Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, suivez le tutoriel sur la [création de définitions de segments à l’aide de l’API](./tutorials/create-a-segment.md).

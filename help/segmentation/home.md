---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segment;Segment;Segments;segments
solution: Experience Platform
title: Adobe Experience Platform Segmentation Service
topic: overview
description: Ce document présente Segmentation Service et le rôle qu’il joue dans Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 79%

---


# Adobe Experience Platform [!DNL Segmentation Service] overview

Adobe Experience Platform [!DNL Segmentation Service] provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], and are readily accessible by any Adobe solution.

This document provides an overview of [!DNL Segmentation Service] and the role it plays in Adobe Experience Platform.

## Getting started with [!DNL Segmentation Service]

Il est important de comprendre les termes clés suivants utilisés dans ce document :

- **Segmentation** : division d’un grand groupe d’individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou le comportement clés d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Fonctionnement de la segmentation

La segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat.

Une fois qu’un segment a été défini sur le plan conceptuel, il est créé dans [!DNL Experience Platform]. En règle générale, les segments sont créés par le spécialiste du marketing ou des audiences bien que certaines organisations préfèrent qu’ils soient créés par leur service marketing, en collaboration avec leurs analystes de données. Upon reviewing the data being sent to [!DNL Platform], the data analyst composes the segment definition by selecting which fields and values will be used to build the rules or conditions of the segment. À cet effet, on utilise l’interface utilisateur ou l’API.

## Création de segments

Qu’ils soient créés à l’aide de l’API ou en utilisant le [!DNL Segment Builder], les segments sont en fin de compte définis à l’aide [!DNL Profile Query Language] (PQL). C’est là que la définition conceptuelle du segment est décrite dans le langage conçu pour récupérer les profils répondant aux critères. Pour plus d’informations, voir la [présentation de PQL](./pql/overview.md).

To learn how to create and use segments in the [!DNL Segment Builder] (the UI implementation of [!DNL Segmentation Service]), see the [Segment Builder guide](./ui/overview.md).

Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, consultez le tutoriel sur la [création de segments ciblés à l’aide de l’API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Dans l’éventualité où un schéma est étendu, tous les chargements ultérieurs doivent mettre à jour les nouveaux champs ajoutés en conséquence. For more information on customizing [!DNL Experience Data Model] (XDM), visit the [Schema Editor tutorial](../xdm/tutorials/create-schema-ui.md).

## Évaluation de segments

### Segmentation par flux

La segmentation par flux est un processus continu de sélection des données qui met à jour vos segments en réponse à l’activité des utilisateurs. Une fois qu’un segment a été créé et enregistré, la définition de segment est appliquée aux données d’entrée [!DNL Real-time Customer Profile]. Les ajouts et les suppressions de segments sont traités régulièrement, ce qui vous permet de vous assurer que votre ciblage d’audience reste pertinent.

Pour plus d’informations sur la segmentation par flux, consultez la [documentation sur la segmentation par flux](./api/streaming-segmentation.md).

### Segmentation par lots

Au lieu d’un processus en continu de sélection de données, la segmentation par lots déplace toutes les données de profil à la fois dans les définitions de segment afin de produire des audiences correspondantes. Une fois créé, ce segment est enregistré et stocké afin que vous puissiez l’exporter pour l’utiliser.

Pour savoir comment évaluer les segments, consultez le [tutoriel sur l’évaluation des segments](./tutorials/evaluate-a-segment.md).

## Accès aux résultats de la segmentation

Pour savoir comment accéder à un segment exporté, consultez le [tutoriel sur l’évaluation des segments](./tutorials/evaluate-a-segment.md).

## Métadonnées de segment

Les métadonnées de segment facilitent l’indexation dans le cas où l’un de vos segments doit être réutilisé et/ou combiné.

Composing your segments (through either the API or [!DNL Segment Builder]) requires that you to define a segment name and merge policy.

### Noms de segment

Lors de la création d’un segment, vous devez fournir un nom de segment. Le nom de segment permet d’identifier un segment particulier dans la collection créée [!DNL Segmentation Service]. Les noms de segment doivent donc être explicites, concis et uniques.

>[!NOTE]
>
>Lors de la planification d’un segment, n’oubliez pas que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec lui. Lorsque vous sélectionnez un nom, pensez à la possibilité que votre segment contienne des portions réutilisables.

### Stratégies de fusion

Merge policies are rules used by [!DNL Profile] to determine how data will be prioritized and combined into a unified view under certain conditions.
If a merge policy is not defined, the default [!DNL Platform] merge policy is used. Si vous préférez utiliser une stratégie de fusion spécifique à votre organisation, vous pouvez créer la vôtre et la marquer comme valeur par défaut de votre organisation.

Vous trouverez plus d’informations sur les stratégies de fusion dans le guide [des stratégies de](../profile/api/merge-policies.md)fusion.

>[!NOTE]
>
>L’estimation des tailles de l’audience est basée sur la stratégie de fusion de profil par défaut de l’entreprise.

### Autres métadonnées de segment

In addition to segment name and merge policy, [!DNL Segment Builder] offers you an additional &quot;segment description&quot; metadata field where you can summarize your segment definition&#39;s purpose.

## Fonctionnalités de segmentation avancées

Les segments peuvent être configurés pour générer en permanence une audience en combinant l’[ingestion de données par flux](../ingestion/streaming-ingestion/overview.md) avec l’une des fonctionnalités de segmentation avancées suivantes :
- [Segmentation séquentielle](#sequential)
- [Segmentation dynamique](#dynamic)
- [Segmentation d’entités multiples](#multi-entity)

Ces fonctionnalités avancées sont décrites plus en détail dans les sections suivantes.

## Segmentation séquentielle {#sequential}

Un parcours utilisateur standard est séquentiel par nature. Adobe Experience Platform vous permet de définir une série ordonnée de segments afin de refléter ce parcours, capturant ainsi des séquences d’événements au fur et à mesure qu’elles se produisent. You can arrange events into their desired order by using the visual event timeline in the [!DNL Segment Builder].

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

Avec la fonction de segmentation d’entités multiples avancée, vous pouvez créer des segments à l’aide de plusieurs classes XDM, ajoutant ainsi des extensions aux schémas de personnes. As a result, [!DNL Segmentation Service] can access additional fields during segment definition as if they were native to the profile data store.

La segmentation d’entités multiples offre la souplesse nécessaire pour identifier les audiences en fonction des données pertinentes pour vos besoins commerciaux. Ce processus peut être réalisé rapidement et facilement sans avoir besoin d’expertise dans l’interrogation des bases de données. Cela vous permet d’ajouter des données clés à vos segments sans avoir à apporter des modifications coûteuses aux flux de données ni à attendre une fusion de données dorsales.

La vidéo suivante est destinée à vous aider à comprendre la segmentation multientité et décrit à la fois la segmentation multientité et le contexte de segment (charge utile de segment).

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

### Cas d’utilisation : promotion axée sur les prix

Pour illustrer la valeur de cette fonction de segmentation avancée, pensez à un architecte de données qui collabore avec un spécialiste du marketing.

In this example, the data architect is joining data for an individual (made up of schemas with [!DNL XDM Individual Profile] and [!DNL XDM ExperienceEvent] as their base classes) to another class using a key. Une fois cette association effectuée, l’architecte de données ou le spécialiste du marketing peut utiliser ces nouveaux champs lors de la définition de segment comme s’ils étaient natifs du schéma de classe de base.

**Le problème**

L’architecte de données et le spécialiste du marketing travaillent tous les deux pour le même détaillant de vêtements. Le détaillant compte plus de 1 000 magasins en Amérique du Nord et baisse régulièrement les prix des produits tout au long de leur cycle de vie. En conséquence, le spécialiste du marketing souhaite lancer une campagne spéciale pour donner aux acheteurs qui ont acheté ces articles la possibilité de les acheter à prix réduit.

Les ressources de l’architecte de données incluent l’accès aux données web issues de la navigation des clients ainsi que les données d’ajout de panier contenant les identifiants SKU des produits. Ils ont également accès à une classe « products » distincte, où sont stockées des informations supplémentaires sur les produits (y compris les prix). Leur conseil est de se concentrer sur les clients qui ont ajouté un produit à leur panier au cours des 14 derniers jours, mais qui ne l’ont pas acheté, et dont le prix a maintenant baissé.

**La solution**

>[!NOTE]
>
>Dans cet exemple, nous supposerons que l’architecte de données a déjà établi un espace de noms d’identifiant.

Using the API, the data architect relates the key from the [!DNL ExperienceEvent] schema with the &quot;products&quot; class. Doing so allows the data architect to make use of the additional fields from the &quot;products&quot; class as if they are native to the [!DNL ExperienceEvent] schema. En guise de dernière étape du travail de configuration, l’architecte de données doit importer les données appropriées dans [!DNL Real-time Customer Profile]. Pour ce faire, activez le jeu de données « products » en vue de l’utiliser avec [!DNL Profile]. With the configuration work complete, either the data architect or the marketer can build the target segment in [!DNL Segment Builder].

Voir la [présentation de la composition des schémas](../xdm/schema/composition.md#union) pour savoir comment définir des relations entre les classes XDM.

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### Cas d’utilisation

Pour illustrer la valeur de cette fonctionnalité de segmentation avancée, prenez en compte trois cas d’utilisation standard qui illustrent les défis qui se posaient dans les applications marketing avant l’amélioration de Segment Payload :
- Personnalisation des e-mails
- Reciblage des e-mails
- Reciblage publicitaire

**Personnalisation des e-mails**

Un spécialiste du marketing qui a créé une campagne par e-mail peut avoir tenté de créer un segment pour une audience cible en utilisant les achats récents des clients en boutique au cours des trois derniers mois. Idéalement, ce segment nécessiterait à la fois le nom de l’article et le nom de la boutique dans laquelle l’achat a été effectué. Avant l’amélioration, le défi consistait à capturer l’identifiant de magasin à partir de l’événement d’achat et à l’affecter au profil du client.

**Reciblage des e-mails**

Il est souvent complexe de créer et de qualifier des segments pour les campagnes par e-mail ciblant « l’abandon de panier ». Avant l’amélioration, il était difficile de savoir quels produits inclure dans un message personnalisé en raison de la disponibilité des données requises. Les données pour lesquelles les produits ont été abandonnés sont liées à des événements d’expérience qui étaient auparavant difficiles à surveiller et dont il était compliqué d’extraire des données.

**Reciblage publicitaire**

Un autre défi classique pour les professionnels du marketing a été de créer des publicités pour recibler les clients qui avaient abandonné des articles dans leur panier. Bien que les définitions de segments aient permis de relever ce défi, il n’existait pas de méthode officielle pour différencier les produits achetés des produits abandonnés avant l’amélioration. Vous pouvez désormais cibler des jeux de données spécifiques lors de la définition de segment.

## [!DNL Segmentation Service] types de données

[!DNL Segmentation Service] prend en charge divers types de données, notamment :

- Chaîne
- Identifiant uniforme de ressource
- Enum
- Nombre
- Long
- Entier
- Court
- Octet
- Booléen
- Date
- Date-heure
- Tableau
- Objet
- Map
- Événements
- Audiences externes
- Segments

Vous trouverez des informations plus détaillées sur ces types de données pris en charge dans le document [des types de données](./data-types.md)pris en charge.

## Étapes suivantes

[!DNL Segmentation Service] fournit un processus consolidé pour créer des segments à partir de [!DNL Real-time Customer Profile] données. En résumé :

- [!DNL Segmentation]La est le processus de définition d’un sous-ensemble de profils de votre banque de profils, ce qui vous permet de caractériser le comportement ou les attributs d’un groupe commercialisable souhaité. [!DNL Segmentation Service] rend ce processus possible.
- Lors de la planification d’un segment, gardez à l’esprit que les segments peuvent être référencés à partir de n’importe quel autre segment et combinés avec lui.
- Un segment peut être créé à partir de règles basées sur des données de profil, des données de série temporelle associées ou des deux.
- Les segments peuvent être évalués à la demande ou en continu. Lors de l’évaluation à la demande, toutes les données de profil sont transmises simultanément par le biais des définitions de segment. Lorsqu’elles sont évaluées de manière continue, les données sont diffusées par le biais des définitions de segment lors de leur entrée dans [!DNL Platform].

Pour savoir comment définir des segments dans l’interface utilisateur, consultez le [guide du créateur de segments](./ui/overview.md). Pour plus d’informations sur la création de définitions de segment à l’aide de l’API, voir le tutoriel sur la [création de segments à l’aide de l’API](./tutorials/create-a-segment.md).
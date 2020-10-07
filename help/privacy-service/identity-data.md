---
keywords: Experience Platform;home;popular topics;ECID;ecid
solution: Experience Platform
title: Données d’identité pour les demandes d’accès à des informations personnelles
topic: overview
description: Ce document fournit des instructions générales expliquant comment configurer vos opérations de données et tirer parti des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 45%

---


# Données d’identité pour les demandes d’accès à des informations personnelles

In order for Adobe Experience Platform [!DNL Privacy Service] to process customer requests for their private data (including access, delete, or opt-out-of-sale requests), it must be provided with unique identifiers that link a specific customer to their stored private data in your Adobe Experience Cloud enabled applications. [!DNL Privacy Service] utilise ensuite ces identifiants pour rassembler toutes les données stockées sous l’identité du client dans et les traite selon la requête du client.[!DNL Experience Cloud]

Ce document fournit des instructions générales expliquant comment configurer vos opérations de données et tirer parti des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.

## Identités et espaces de noms

Lorsqu’un client peut interagir avec votre marque via plusieurs canaux, il peut s’avérer difficile de rapprocher les différents identifiants enregistrés à partir de ces nombreuses interactions. This in turn can make it difficult to determine which data belongs to a particular person in your [!DNL Experience Cloud] applications.

For example, when handling customer data requests in [!DNL Privacy Service], an identity may represent a cookie value set under an Adobe-controlled domain, a cookie value under a third-party domain and shared with Adobe, or a custom identifier that you explicitly define within your IMS Organization.

It is therefore required that each identity sent to [!DNL Privacy Service] is accompanied with a namespace that provides context by relating the identity value to its system of origin. Un espace de noms peut représenter un concept générique tel qu’une adresse électronique (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Adobe Experience Platform Identity Service conserve un stock d’espaces de nom d’identité définis globalement et par l’utilisateur. Pour des informations plus détaillées sur les espaces de noms, consultez la [présentation des espaces de noms d’identité](../identity-service/namespaces.md). For a list of standard namespaces and namespace qualifiers that are commonly used in [!DNL Privacy Service], see the [appendix section](api/appendix.md) in the developer guide.

## ECID et service d’accord préalable

Adobe Experience Cloud [!DNL Identity Service] serves as a common identification framework for [!DNL Experience Cloud], and assigns a unique, persistent ID to each site visitor. The [!DNL Experience Cloud] ID (ECID) tracks a customer&#39;s activity through the use of a first-party cookie, can uniquely identify a device across multiple applications, and allows you to identify the same site visitor and their data in different [!DNL Experience Cloud] applications. Pour plus d’informations, consultez la [présentation d’Identity Service d’Experience Cloud](https://docs.adobe.com/content/help/fr-FR/id-service/using/intro/overview.html).

Opt-in Service, an extension of [!DNL Experience Cloud Identity Service], allows you set up protocols on your application to let visitors determine whether you can set a cookie on the visitor&#39;s device or browser. Pour des informations plus détaillées sur le service d’accord préalable, y compris sur la configuration du service pour votre application, consultez la [documentation du service d’accord préalable](https://docs.adobe.com/content/help/fr-FR/id-service/using/implementation/opt-in-service/optin-overview.html).

Once your site visitors have been assigned ECIDs, you can utilize the Adobe [!DNL Privacy JavaScript Library] to retrieve those IDs for use in privacy requests, as described in the next section.

## [!DNL Privacy JS Library]

The [!DNL Adobe Privacy JavaScript Library] provides several functions that allow you to retrieve and remove customer identities that are stored in the browser. La bibliothèque peut être configurée pour récupérer les informations d’identité de plusieurs applications Adobe, dont ECID. Through the use of callbacks or promises, you can programmatically handle successfully retrieved IDs and send them to the [!DNL Privacy Service] API.

For more information about [!DNL Privacy JS Library], including code samples for several common use cases, please refer to the [Privacy JS Library overview](js-library.md).

## Étapes suivantes

Ce document offre une brève présentation des principaux concepts impliqués dans la récupération des données d’identité client afin de pouvoir les utiliser dans les demandes d’accès à des informations personnelles. Il est recommandé de consulter les liens de documentation fournis dans chaque section pour obtenir des informations plus détaillées sur ces concepts et services. For steps on how to send retrieved IDs to [!DNL Privacy Service] for creating access, delete, or opt-out-of-sale requests, see the [Privacy Service developer guide](api/getting-started.md).
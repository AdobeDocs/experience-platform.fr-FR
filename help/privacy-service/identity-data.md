---
keywords: Experience Platform;accueil;rubriques populaires;ECID;ecid
solution: Experience Platform
title: Données d’identité pour les demandes d’accès à des informations personnelles
description: Ce document fournit des instructions générales expliquant comment configurer vos opérations de données et tirer parti des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 40%

---

# Données d’identité pour les demandes d’accès à des informations personnelles

Pour que Adobe Experience Platform [!DNL Privacy Service] puisse traiter les demandes de clients concernant leurs données privées (y compris les demandes d’accès, de suppression ou d’exclusion de la vente), il doit lui être fourni avec des identifiants uniques qui lient un client spécifique à ses données privées stockées dans vos applications Adobe Experience Cloud activées. [!DNL Privacy Service] utilise ensuite ces identifiants pour rassembler toutes les données stockées sous l’identité du client dans [!DNL Experience Cloud] et les traiter selon la demande du client.

Ce document fournit des instructions générales expliquant comment configurer vos opérations de données et tirer parti des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.

## Identités et espaces de noms

Lorsqu’un client ou une cliente peut interagir avec votre marque via plusieurs canaux, il peut s’avérer difficile de réconcilier les différents identifiants enregistrés à partir de ces nombreuses interactions. Cela peut rendre difficile de déterminer quelles données appartiennent à une personne particulière dans vos applications [!DNL Experience Cloud].

Par exemple, lors du traitement des demandes de données client dans [!DNL Privacy Service], une identité peut représenter une valeur de cookie définie sous un domaine contrôlé par l’Adobe, une valeur de cookie définie sous un domaine tiers et partagée avec l’Adobe ou un identifiant personnalisé défini explicitement au sein de votre organisation.

Il est donc nécessaire que chaque identité envoyée à [!DNL Privacy Service] soit accompagnée d’un espace de noms qui fournit un contexte en reliant la valeur d’identité à son système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse e-mail (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Le service d’identités d’Adobe Experience Platform conserve un stock d’espaces de nom d’identité définis globalement et par l’utilisateur. Pour des informations plus détaillées sur les espaces de noms, consultez la [présentation des espaces de noms d’identité](../identity-service/features/namespaces.md). Pour obtenir la liste des espaces de noms standard et des qualificateurs d’espace de noms couramment utilisés dans [!DNL Privacy Service], reportez-vous à la [section de l’annexe](api/appendix.md) du guide de l’API.

## ECID et service d’accord préalable

Adobe Experience Cloud [!DNL Identity Service] sert de cadre d’identification commun à [!DNL Experience Cloud] et affecte un identifiant persistant unique à chaque visiteur du site. L’ [!DNL Experience Cloud] ID (ECID) effectue le suivi de l’activité d’un client à l’aide d’un cookie propriétaire, peut identifier de manière unique un appareil dans plusieurs applications et vous permet d’identifier le même visiteur du site et ses données dans différentes applications [!DNL Experience Cloud]. Pour plus d’informations, consultez la [présentation du du service d’identités d’Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr).

Le service Opt-in, une extension de [!DNL Experience Cloud Identity Service], vous permet de configurer des protocoles sur votre application pour permettre aux visiteurs de déterminer si vous pouvez définir un cookie sur l’appareil ou le navigateur du visiteur. Pour des informations plus détaillées sur le service d’accord préalable, y compris sur la configuration du service pour votre application, consultez la [documentation du service d’accord préalable](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=fr).

Une fois que les visiteurs de votre site ont reçu des ECID, vous pouvez utiliser l’Adobe [!DNL Privacy JavaScript Library] pour récupérer ces ID en vue de les utiliser dans des demandes d’accès à des informations personnelles, comme décrit dans la section suivante.

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library] fournit plusieurs fonctions qui vous permettent de récupérer et de supprimer les identités de client stockées dans le navigateur. La bibliothèque peut être configurée pour récupérer les informations d’identité de plusieurs applications Adobe, dont ECID. Grâce aux rappels ou aux promesses, vous pouvez gérer par programmation les identifiants récupérés avec succès et les envoyer à l’API [!DNL Privacy Service].

Pour plus d’informations sur [!DNL Privacy JS Library], y compris des exemples de code pour plusieurs cas d’utilisation courants, reportez-vous à la [présentation de la bibliothèque JS d’Adobe Privacy](js-library.md).

## Étapes suivantes

Ce document offre une brève présentation des principaux concepts impliqués dans la récupération des données d’identité client afin de pouvoir les utiliser dans les demandes d’accès à des informations personnelles. Il est recommandé de consulter les liens de documentation fournis dans chaque section pour obtenir des informations plus détaillées sur ces concepts et services. Pour savoir comment envoyer des ID récupérés à [!DNL Privacy Service] pour créer des demandes d’accès, de suppression ou d’exclusion, consultez le [guide de l’API du Privacy Service](api/overview.md).

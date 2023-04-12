---
keywords: Experience Platform;accueil;rubriques populaires;ECID;ecid
solution: Experience Platform
title: Données d’identité pour les demandes d’accès à des informations personnelles
description: Ce document fournit des instructions générales expliquant comment configurer vos opérations de données et tirer parti des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 45%

---

# Données d’identité pour les demandes d’accès à des informations personnelles

Pour Adobe Experience Platform [!DNL Privacy Service] pour traiter les demandes des clients concernant leurs données privées (y compris les demandes d’accès, de suppression ou d’exclusion de la vente), il doit être fourni avec des identifiants uniques qui lient un client spécifique à ses données privées stockées dans vos applications Adobe Experience Cloud activées. [!DNL Privacy Service] utilise ensuite ces identifiants pour rassembler toutes les données stockées sous l’identité du client dans et les traite selon la requête du client.[!DNL Experience Cloud]

Ce document fournit des instructions générales expliquant comment configurer vos opérations de données et tirer parti des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.

## Identités et espaces de noms

Lorsqu’un client peut interagir avec votre marque via plusieurs canaux, il peut s’avérer difficile de rapprocher les différents identifiants enregistrés à partir de ces nombreuses interactions. Cela peut rendre difficile de déterminer quelles données appartiennent à une personne spécifique dans votre [!DNL Experience Cloud] applications.

Par exemple, lors du traitement des requêtes de données client dans [!DNL Privacy Service], une identité peut représenter une valeur de cookie définie sous un domaine contrôlé par l’Adobe, une valeur de cookie définie sous un domaine tiers et partagée avec un Adobe ou un identifiant personnalisé défini explicitement au sein de votre organisation.

Chaque identité envoyée à [!DNL Privacy Service] est accompagné d’un espace de noms qui fournit un contexte en reliant la valeur d’identité à son système d’origine. Un espace de noms peut représenter un concept générique tel qu’une adresse e-mail (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Adobe Experience Platform Identity Service conserve un stock d’espaces de nom d’identité définis globalement et par l’utilisateur. Pour des informations plus détaillées sur les espaces de noms, consultez la [présentation des espaces de noms d’identité](../identity-service/namespaces.md). Pour obtenir la liste des espaces de noms standard et des qualificateurs d’espace de noms couramment utilisés dans [!DNL Privacy Service], reportez-vous à la section [section de l’annexe](api/appendix.md) dans le guide de l’API.

## ECID et service d’accord préalable

Adobe Experience Cloud [!DNL Identity Service] sert de cadre d’identification commun à [!DNL Experience Cloud]et affecte un identifiant persistant unique à chaque visiteur du site. Le [!DNL Experience Cloud] L’identifiant (ECID) effectue le suivi de l’activité d’un client à l’aide d’un cookie propriétaire, peut identifier de manière unique un appareil dans plusieurs applications et vous permet d’identifier un même visiteur du site et ses données dans différentes [!DNL Experience Cloud] applications. Pour plus d’informations, consultez la [présentation d’Identity Service d’Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr).

Service Opt-in, extension de [!DNL Experience Cloud Identity Service], vous permet de configurer des protocoles sur votre application pour permettre aux visiteurs de déterminer si vous pouvez définir un cookie sur l’appareil ou le navigateur du visiteur. Pour des informations plus détaillées sur le service d’accord préalable, y compris sur la configuration du service pour votre application, consultez la [documentation du service d’accord préalable](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=fr).

Une fois que des ECID ont été attribués aux visiteurs de votre site, vous pouvez utiliser l’Adobe [!DNL Privacy JavaScript Library] pour récupérer ces identifiants afin de les utiliser dans des demandes d’accès à des informations personnelles, comme décrit dans la section suivante.

## [!DNL Privacy JS Library]

Le [!DNL Adobe Privacy JavaScript Library] fournit plusieurs fonctions qui vous permettent de récupérer et de supprimer les identités de client stockées dans le navigateur. La bibliothèque peut être configurée pour récupérer les informations d’identité de plusieurs applications Adobe, dont ECID. Grâce aux rappels ou aux promesses, vous pouvez gérer par programmation les identifiants récupérés avec succès et les envoyer au [!DNL Privacy Service] API.

Pour plus d’informations sur [!DNL Privacy JS Library], y compris des exemples de code pour plusieurs cas d’utilisation courants, reportez-vous à la section [Présentation de la bibliothèque JS d’Adobe Privacy](js-library.md).

## Étapes suivantes

Ce document offre une brève présentation des principaux concepts impliqués dans la récupération des données d’identité client afin de pouvoir les utiliser dans les demandes d’accès à des informations personnelles. Il est recommandé de consulter les liens de documentation fournis dans chaque section pour obtenir des informations plus détaillées sur ces concepts et services. Pour savoir comment envoyer des identifiants récupérés à [!DNL Privacy Service] pour créer des requêtes d’accès, de suppression ou d’exclusion de la vente, voir la section [Guide de l’API Privacy Service](api/overview.md).

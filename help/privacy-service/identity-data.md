---
keywords: Experience Platform;accueil;rubriques populaires;ECID;ecid
solution: Experience Platform
title: Données d’identité pour les demandes de confidentialité
topic-legacy: overview
description: Ce document fournit des instructions générales expliquant comment configurer vos opérations de données et tirer parti des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 44%

---

# Données d’identité pour les demandes d’accès à des informations personnelles

Pour que Adobe Experience Platform [!DNL Privacy Service] puisse traiter les demandes de clients pour leurs données privées (y compris les demandes d&#39;accès, de suppression ou d&#39;exclusion de la vente), il doit être doté d&#39;identifiants uniques qui lient un client spécifique à ses données privées stockées dans les applications Adobe Experience Cloud activées. [!DNL Privacy Service] utilise ensuite ces identifiants pour rassembler toutes les données stockées sous l’identité du client dans et les traite selon la requête du client.[!DNL Experience Cloud]

Ce document fournit des instructions générales expliquant comment configurer vos opérations de données et tirer parti des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes d’accès à des informations personnelles des clients.

## Identités et espaces de noms

Lorsqu’un client peut interagir avec votre marque via plusieurs canaux, il peut s’avérer difficile de rapprocher les différents identifiants enregistrés à partir de ces nombreuses interactions. Cela peut à son tour rendre difficile de déterminer quelles données appartiennent à une personne particulière dans vos applications [!DNL Experience Cloud].

Par exemple, lors du traitement des demandes de données client dans [!DNL Privacy Service], une identité peut représenter une valeur de cookie définie sous un domaine contrôlé par Adobe, une valeur de cookie sous un domaine tiers et partagée avec un Adobe ou un identifiant personnalisé que vous définissez explicitement dans votre organisation IMS.

Il est donc nécessaire que chaque identité envoyée à [!DNL Privacy Service] soit accompagnée d&#39;un espace de nommage qui fournit un contexte en liant la valeur d&#39;identité à son système d&#39;origine. Un espace de noms peut représenter un concept générique tel qu’une adresse électronique (« E-mail ») ou associer l’identité à une application spécifique telle qu’un identifiant Adobe Advertising Cloud ID (« AdCloud ») ou un identifiant Adobe Target (« TNTID »).

Adobe Experience Platform Identity Service conserve un stock d’espaces de nom d’identité définis globalement et par l’utilisateur. Pour des informations plus détaillées sur les espaces de noms, consultez la [présentation des espaces de noms d’identité](../identity-service/namespaces.md). Pour une liste des espaces de nommage et des qualificatifs d&#39;espace de nommage standard couramment utilisés dans [!DNL Privacy Service], consultez la section [appendice](api/appendix.md) du guide du développeur.

## ECID et service d’accord préalable

Adobe Experience Cloud [!DNL Identity Service] sert de cadre d&#39;identification commun à [!DNL Experience Cloud] et affecte un identifiant unique et persistant à chaque visiteur de site. L’[!DNL Experience Cloud] identifiant (ECID) effectue le suivi de l’activité d’un client à l’aide d’un cookie propriétaire, peut identifier de manière unique un périphérique dans plusieurs applications et vous permet d’identifier le même visiteur de site et ses données dans différentes applications [!DNL Experience Cloud]. Pour plus d’informations, consultez la [présentation d’Identity Service d’Experience Cloud](https://docs.adobe.com/content/help/fr-FR/id-service/using/intro/overview.html).

Le service d’inclusion, une extension de [!DNL Experience Cloud Identity Service], vous permet de configurer des protocoles sur votre application pour permettre aux visiteurs de déterminer si vous pouvez définir un cookie sur le visiteur ou le navigateur. Pour des informations plus détaillées sur le service d’accord préalable, y compris sur la configuration du service pour votre application, consultez la [documentation du service d’accord préalable](https://docs.adobe.com/content/help/fr-FR/id-service/using/implementation/opt-in-service/optin-overview.html).

Une fois que les visiteurs de votre site ont reçu des ECID, vous pouvez utiliser l&#39;Adobe [!DNL Privacy JavaScript Library] pour récupérer ces ID en vue de les utiliser dans des demandes de confidentialité, comme décrit dans la section suivante.

## [!DNL Privacy JS Library]

Le [!DNL Adobe Privacy JavaScript Library] fournit plusieurs fonctions qui vous permettent de récupérer et de supprimer les identités de client stockées dans le navigateur. La bibliothèque peut être configurée pour récupérer les informations d’identité de plusieurs applications Adobe, dont ECID. Grâce aux rappels ou aux promesses, vous pouvez programmer la gestion des identifiants récupérés avec succès et les envoyer à l&#39;API [!DNL Privacy Service].

Pour plus d&#39;informations sur [!DNL Privacy JS Library], y compris des exemples de code pour plusieurs cas d&#39;utilisation courants, consultez la section [Présentation de la bibliothèque JS de confidentialité](js-library.md).

## Étapes suivantes

Ce document offre une brève présentation des principaux concepts impliqués dans la récupération des données d’identité client afin de pouvoir les utiliser dans les demandes d’accès à des informations personnelles. Il est recommandé de consulter les liens de documentation fournis dans chaque section pour obtenir des informations plus détaillées sur ces concepts et services. Pour savoir comment envoyer des ID récupérés à [!DNL Privacy Service] pour créer des demandes d&#39;accès, de suppression ou d&#39;exclusion de la vente, consultez le [guide du développeur Privacy Service](api/getting-started.md).

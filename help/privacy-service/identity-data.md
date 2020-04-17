---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Données d’identité pour les demandes de confidentialité
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Données d’identité pour les demandes de confidentialité

Pour qu’Adobe Experience Platform Privacy Service puisse traiter les demandes de clients concernant leurs données privées (y compris les demandes d’accès, de suppression ou d’exclusion de la vente), il doit être doté d’identifiants uniques qui lient un client spécifique à ses données privées stockées dans vos applications Adobe Experience Cloud. Privacy Service utilise ensuite ces identifiants pour rassembler toutes les données stockées sous l’identité du client dans Experience Cloud et les traiter selon la demande du client.

Ce fournit des instructions générales sur la configuration de vos opérations de données et l’utilisation des technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes de confidentialité des clients.

## Identités et  

Lorsqu’un client peut interagir avec votre marque par le biais de plusieurs  de différents, il peut s’avérer difficile de concilier les identifiants disparates qui sont enregistrés à partir de ces nombreuses interactions. Cela peut à son tour rendre difficile de déterminer quelles données appartiennent à une personne particulière dans vos applications Experience Cloud.

Par exemple, lors du traitement des demandes de données client dans Privacy Service, une identité peut représenter une valeur de cookie définie sous un domaine contrôlé par Adobe, une valeur de cookie sous un domaine tiers et partagée avec Adobe, ou un identifiant personnalisé que vous définissez explicitement dans votre organisation IMS.

Il est donc nécessaire que chaque identité envoyée au Service de la protection de la vie privée soit accompagnée d&#39;un **** qui fournit un contexte en reliant la valeur d&#39;identité à son système de  de de . Un   peut représenter un concept générique tel qu’une adresse électronique (&quot;Email&quot;) ou associer l’identité à une application spécifique, telle qu’un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou un Adobe  ID (&quot;TNTID&quot;).

Le service d’identité Adobe Experience Platform conserve un stock de d’identité définis globalement et définis par l’utilisateur  . Pour plus d&#39;informations sur  , reportez-vous à l&#39;aperçu [des  de l&#39;](../identity-service/namespaces.md)identité . Pour un de qualificatifs standard de  et de [couramment utilisés dans Privacy Service, reportez-vous à la section](api/appendix.md) de l’annexe du guide du développeur.

## ECID et service d’inclusion

Adobe Experience Cloud Identity Service sert de cadre d’identification commun à Experience Cloud et affecte un identifiant unique et persistant à chaque de site. L’ECID (Experience Cloud ID) effectue le suivi du  d’un client par l’intermédiaire d’un cookie propriétaire, peut identifier de manière unique un périphérique dans plusieurs applications et vous permet d’identifier le même de site et ses données dans différentes applications Experience Cloud. See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/fr-FR/id-service/using/intro/overview.html) for more information.

Le service d’inclusion, une extension du service d’identité Experience Cloud, vous permet de configurer des protocoles sur votre application pour permettre aux de déterminer si vous pouvez définir un cookie sur le périphérique  ou le navigateur du. Pour plus d’informations sur le service d’inscription, y compris sur la configuration du service pour votre application, reportez-vous à la documentation [](https://docs.adobe.com/content/help/fr-FR/id-service/using/implementation/opt-in-service/optin-overview.html)du service d’inscription.

Une fois que les de votre site ont reçu des ECID, vous pouvez utiliser la bibliothèque JavaScript de confidentialité d’Adobe pour récupérer ces ID en vue de les utiliser dans des demandes de confidentialité, comme décrit dans la section suivante.

## Bibliothèque JS de confidentialité

La bibliothèque JavaScript de confidentialité d’Adobe fournit plusieurs fonctions qui vous permettent de récupérer et de supprimer les identités de client stockées dans le navigateur. La bibliothèque peut être configurée pour récupérer les informations d’identité de plusieurs applications Adobe, dont ECID. Grâce aux rappels ou aux promesses, vous pouvez gérer par programmation les identifiants récupérés et les envoyer à l’API de Privacy Service.

Pour plus d’informations sur la bibliothèque JS de confidentialité, y compris des exemples de code pour plusieurs cas d’utilisation courants, consultez la présentation [de la bibliothèque JS de](js-library.md)confidentialité.

## Étapes suivantes

Ce donne un bref aperçu des principaux concepts impliqués dans la récupération des données d’identité du client en vue de les utiliser dans les demandes de confidentialité. Il est recommandé de consulter les liens de documentation fournis dans chaque section pour obtenir des informations plus détaillées sur ces concepts et services. Pour savoir comment envoyer des ID récupérés à Privacy Service pour créer des demandes d’accès, de suppression ou d’exclusion, consultez le guide [du développeur](api/getting-started.md)Privacy Service.
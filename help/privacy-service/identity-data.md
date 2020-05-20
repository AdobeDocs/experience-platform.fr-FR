---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Données d’identité pour les demandes de confidentialité
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 3%

---


# Données d’identité pour les demandes de confidentialité

Pour qu’Adobe Experience Platform Privacy Service puisse traiter les demandes de clients concernant leurs données privées (y compris les demandes d’accès, de suppression ou d’exclusion), il doit être doté d’identifiants uniques qui lient un client spécifique à ses données privées stockées dans vos applications Adobe Experience Cloud. Privacy Service utilise ensuite ces identifiants pour rassembler toutes les données stockées sous l’identité du client dans Experience Cloud et les traiter selon la demande du client.

Ce document fournit des instructions générales sur la manière de configurer vos opérations de données et d’exploiter les technologies Adobe pour récupérer efficacement les informations d’identité appropriées pour les demandes de confidentialité des clients.

## Identités et espaces de nommage

Lorsqu’un client peut interagir avec votre marque via plusieurs canaux différents, il peut s’avérer difficile de concilier les identifiants disparates qui sont enregistrés à partir de ces nombreuses interactions. Cela peut à son tour rendre difficile de déterminer quelles données appartiennent à une personne particulière dans vos applications Experience Cloud.

Par exemple, lors du traitement des demandes de données client dans Privacy Service, une identité peut représenter une valeur de cookie définie sous un domaine contrôlé par Adobe, une valeur de cookie sous un domaine tiers et partagée avec Adobe, ou un identifiant personnalisé que vous définissez explicitement dans votre organisation IMS.

Il est donc nécessaire que chaque identité envoyée au Service de la protection des renseignements personnels soit accompagnée d&#39;un **espace de nommage** qui fournit un contexte en liant la valeur d&#39;identité à son système d&#39;origine. Un espace de nommage peut représenter un concept générique tel qu’une adresse électronique (&quot;Adresse électronique&quot;) ou associer l’identité à une application spécifique, telle qu’un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou un Adobe Cible ID (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service conserve un stock d’espaces de nommage d’identité définis globalement et définis par les utilisateurs. Pour plus d&#39;informations sur les espaces de nommage, consultez la présentation [de l&#39;espace de nommage](../identity-service/namespaces.md)d&#39;identité. Pour une liste des espaces de nommage et des qualificatifs d’espace de nommage standard couramment utilisés dans Privacy Service, consultez la section [de l’](api/appendix.md) annexe du guide du développeur.

## ECID et service d’inclusion

Adobe Experience Cloud Identity Service sert de cadre d’identification commun à Experience Cloud et affecte un identifiant unique et persistant à chaque visiteur de site. L’ECID (Experience Cloud ID) effectue le suivi de l’activité d’un client au moyen d’un cookie propriétaire, peut identifier de manière unique un périphérique dans plusieurs applications et vous permet d’identifier le même visiteur de site et ses données dans différentes applications Experience Cloud. See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/fr-FR/id-service/using/intro/overview.html) for more information.

Le service d’inclusion, une extension d’Experience Cloud Identity Service, vous permet de configurer des protocoles sur votre application pour permettre aux visiteurs de déterminer si vous pouvez définir un cookie sur le périphérique ou le navigateur du visiteur. Pour plus d’informations sur le service d’inscription, y compris sur la configuration du service pour votre application, consultez la documentation [du service d’](https://docs.adobe.com/content/help/fr-FR/id-service/using/implementation/opt-in-service/optin-overview.html)inscription.

Une fois que des ECID ont été attribués aux visiteurs de votre site, vous pouvez utiliser la bibliothèque JavaScript de traitement des données personnelles d’Adobe pour récupérer ces identifiants en vue de les utiliser dans des demandes de confidentialité, comme décrit dans la section suivante.

## Bibliothèque JS de confidentialité

La bibliothèque JavaScript d’Adobe Privacy fournit plusieurs fonctions qui vous permettent de récupérer et de supprimer les identités de client stockées dans le navigateur. La bibliothèque peut être configurée pour récupérer les informations d’identité de plusieurs applications Adobe, dont ECID. Grâce aux rappels ou aux promesses, vous pouvez programmer la gestion des identifiants récupérés avec succès et les envoyer à l’API Privacy Service.

Pour plus d’informations sur la bibliothèque JS de confidentialité, y compris des exemples de code pour plusieurs cas d’utilisation courants, consultez la présentation [de la bibliothèque JS de](js-library.md)confidentialité.

## Étapes suivantes

Ce document donne un bref aperçu des concepts centraux impliqués dans la récupération des données d&#39;identité des clients pour les utiliser dans les demandes de confidentialité. Il est recommandé de consulter les liens de documentation fournis dans chaque section pour obtenir des informations plus détaillées sur ces concepts et services. Pour savoir comment envoyer des identifiants récupérés à Privacy Service pour créer des demandes d’accès, de suppression ou d’exclusion de la vente, consultez le guide [de développement](api/getting-started.md)Privacy Service.
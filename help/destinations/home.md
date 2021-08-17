---
keywords: destinations;adobe experience platform;plateforme;présentation des destinations;activer les données;activer;activer
title: Présentation des destinations
seo-title: Présentation des destinations
description: Découvrez comment activer les données Adobe Experience Platform vers des destinations pour les campagnes marketing cross-canal, les e-mails, la publicité ciblée, etc.
seo-description: Les destinations sont des intégrations prédéfinies avec des plateformes de destination qui permettent l’activation transparente des données de Adobe Experience Platform. Vous pouvez utiliser les destinations dans Adobe Experience Platform pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: f73598224d527535aaf9ecb2aa1c26786cae2d82
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 38%

---

# Présentation d’[!DNL Destinations] {#overview}

![Bannière de présentation des destinations](./assets/overview/destinations-overview-banner.png)

Les **[!DNL Destinations]** sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

## Destinations et sources {#destinations-and-sources}

L’une des principales fonctionnalités de Platform est l’ingestion de vos données propriétaires et leur activation en fonction des besoins de votre entreprise. Utilisez [sources](../sources/home.md) pour ingérer des données dans Platform et des destinations afin d’exporter des données de Platform.

## Étapes des destinations {#steps}

* Choisissez parmi un [catalogue en libre-service](./catalog/overview.md) de toutes les destinations disponibles dans Platform.
* Utilisez les destinations pour [activer](./ui/activate-destinations.md) et envoyez des profils ou des segments aux plateformes d’automatisation marketing, de publicité numérique, etc.
* Planifiez régulièrement des exportations de données vers les destinations de votre choix.

## Commandes {#controls}

Les commandes de l’[espace de travail des destinations](./ui/destinations-workspace.md) vous permettent d’effectuer les opérations suivantes :

* parcourir le catalogue des plateformes de destination dans lesquelles vous pouvez activer vos données ;
* créer, modifier, activer et désactiver des flux de données vers les destinations du catalogue ;
* Créez un compte dans un emplacement de stockage ou liez Platform au compte dans la plateforme de destination ;
* sélectionner les segments à activer vers les destinations ;
* sélectionner les [champs XDM](../xdm/home.md) à exporter lors de l’activation de segments vers des destinations de marketing par e-mail.

## Types et catégories de destination {#types-and-categories}

Pour plus d’informations, consultez la [présentation des types et catégories de destination](./destination-types.md).

## Destinations et contrôles d’accès {#access-controls}

La fonctionnalité de destinations de Platform fonctionne avec les autorisations de contrôle d’accès de Adobe Experience Platform. Selon le niveau d’autorisation de l’utilisateur, vous pouvez afficher, gérer et activer les destinations. Pour plus d’informations sur les autorisations individuelles, consultez [Contrôle d’accès dans Adobe Experience Platform](../access-control/home.md) et faites défiler la page vers le bas.

Pour plus d’informations sur les contrôles d’accès, consultez le [Guide de l’utilisateur du contrôle d’accès](../access-control/ui/overview.md).

## [!DNL Data Governance] restrictions sur l’activation des données vers les destinations {#data-governance}

La gouvernance des données est appliquée pour les destinations de Platform par le biais :

* *les* actions marketing que vous pouvez sélectionner dans le workflow de création de destinations ;
* ** Stratégies d’utilisation des données qui limitent l’activation des données contenant certains libellés d’utilisation vers les destinations avec certaines actions marketing.

Pour plus d’informations sur les [actions marketing](../data-governance/policies/overview.md) et la [résolution des violations de stratégie de données](../data-governance/enforcement/auto-enforcement.md), voir la section [!DNL Data Governance] de la documentation Platform.

Pour plus d’informations sur la sélection d’actions marketing dans le processus de création de destination, consultez les pages suivantes pour les différents types de destination dans Platform :

* [Destinations publicitaires - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Destinations publicitaires - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinations publicitaires - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Destinations de stockage dans le cloud](./catalog/cloud-storage/overview.md)
* [Destinations de marketing par e-mail ](./catalog/email-marketing/overview.md)
* [Destinations sociales](./catalog/social/overview.md)

Pour plus d’informations sur les violations de stratégie de données dans le processus d’activation des segments, voir l’étape Révision dans [Activation des profils et des segments vers une destination](./ui/activate-destinations.md#review).

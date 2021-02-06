---
keywords: destinations;adobe experience platform;platform;destinations overview;activate data;activate; activate;
title: Présentation des destinations
seo-title: Présentation des destinations
description: Découvrez comment activer les données Adobe Experience Platform vers des destinations pour des campagnes marketing inter-canaux, des courriels, des publicités ciblées, etc.
seo-description: Les destinations sont des intégrations préétablies avec des plateformes de destination qui permettent une activation transparente des données de Adobe Experience Platform. Vous pouvez utiliser les Destinations dans la Adobe Experience Platform pour activer vos données connues et inconnues pour les campagnes marketing par canal, les campagnes par courriel, les publicités ciblées et de nombreux autres cas d’utilisation.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 40%

---


# [!DNL Destinations] aperçu {#overview}

![Bannière de présentation des destinations](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sont des intégrations préétablies avec des plateformes de destination qui permettent une activation transparente des données de Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

## Destinations et sources {#destinations-and-sources}

L’une des fonctionnalités de base de Platform consiste à ingérer vos données propriétaires et à les activer en fonction de vos besoins professionnels. Utilisez les sources pour importer des données dans la plate-forme et les destinations pour exporter des données de la plate-forme.

## Étapes des destinations {#steps}

* Choisissez dans un [catalogue en libre-service](./catalog/overview.md) de toutes les destinations disponibles dans Platform.
* Utilisez les **[!UICONTROL destinations]** pour [activer](./ui/activate-destinations.md) et envoyer des profils ou des segments aux plateformes d’automatisation marketing, de publicité numérique, etc.
* Planifiez régulièrement des exportations de données vers les destinations de votre choix.

## Commandes {#controls}

Les commandes de l’[espace de travail des destinations](./ui/destinations-workspace.md) vous permettent d’effectuer les opérations suivantes :

* parcourir le catalogue des plateformes de destination dans lesquelles vous pouvez activer vos données ;
* créer, modifier, activer et désactiver des flux de données vers les destinations du catalogue ;
* Créez un compte dans un emplacement d’enregistrement ou liez la plate-forme au compte dans la plate-forme de destination ;
* sélectionner les segments à activer vers les destinations ;
* sélectionner les [champs XDM](../xdm/home.md) à exporter lors de l’activation de segments vers des destinations de marketing par e-mail.

## Types et catégories de destination  {#types-and-categories}

Pour plus d’informations, consultez la [présentation des types et catégories de destination](./destination-types.md).

## Destinations et contrôles d’accès  {#access-controls}

La fonctionnalité de destinations dans Platform fonctionne avec les autorisations de contrôle d&#39;accès Adobe Experience Platform. Selon le niveau d’autorisation de l’utilisateur, vous pouvez afficher, gérer et activer les destinations. Pour plus d’informations sur les autorisations individuelles, consultez [Contrôle d’accès dans Adobe Experience Platform](../access-control/home.md) et faites défiler la page vers le bas.

Pour plus d’informations sur les contrôles d’accès, consultez le [Guide de l’utilisateur du contrôle d’accès](../access-control/ui/overview.md).

## [!DNL Data Governance] restrictions sur l’activation des données vers les destinations  {#data-governance}

La gouvernance des données est appliquée pour les destinations de plateformes par le biais :

* *Utilisation marketing* que vous pouvez sélectionner dans le processus de création de destinations ;
* *Règles* d’utilisation des données qui limitent l’activation des données contenant certaines étiquettes d’utilisation vers des destinations présentant certains cas d’utilisation marketing.

Voir [!DNL Data Governance] dans la documentation de la plate-forme pour plus d&#39;informations sur [les cas d&#39;utilisation marketing](../data-governance/policies/overview.md) et [la résolution des violations de stratégie de données](../data-governance/enforcement/auto-enforcement.md).

Pour plus d&#39;informations sur la sélection des cas d&#39;utilisation marketing dans le flux de travail de création de destination, consultez les pages suivantes pour les différents types de destination dans la plate-forme :

* [Destinations publicitaires - Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [Destinations publicitaires - Publicités Google](./catalog/advertising/google-ads-destination.md)
* [Destinations publicitaires - Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [Destinations de stockage dans le cloud](./catalog/cloud-storage/workflow.md)
* [Destinations de marketing par e-mail](./catalog/email-marketing/overview.md)
* [Destinations de réseau social](./catalog/social/workflow.md)

Pour plus d&#39;informations sur les violations de la stratégie de données dans le processus d&#39;activation des segments, voir l&#39;étape de révision dans [Activation des profils et des segments vers une destination](./ui/activate-destinations.md#review).
---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;destinations;destination;rtcdp
title: Présentation des destinations
seo-title: Présentation des destinations
description: Activez les données de Platform vers des destinations pour les campagnes marketing cross-canal, les emails, les publicités ciblées, et bien plus encore.
seo-description: Les destinations sont des intégrations préconfigurées à des plateformes de destination qui permettent l’activation transparente des données provenant de la plateforme des données clients en temps réel. Vous pouvez utiliser les destinations dans la plateforme de données client en temps réel pour activer vos données connues et inconnues pour les campagnes marketing intercanaux, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 73%

---


# [!DNL Destinations] aperçu {#overview}

![Bannière de présentation des destinations](./assets/overview/destinations-overview-banner.png)

Les **[!DNL Destinations]** sont des intégrations préconfigurées à des plateformes de destination qui permettent l’activation transparente des données provenant de la plateforme de données clients en temps réel. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

## Destinations et sources {#destinations-and-sources}

L’une des principales fonctionnalités de la plateforme des données clients en temps réel est l’ingestion de vos données propriétaires et leur activation en fonction des besoins de votre entreprise. Utilisez les sources pour ingérer des données dans la plateforme de données clients en temps réel et les destinations pour exporter des données depuis cette même plateforme.

## Étapes des destinations {#steps}

* Effectuez un choix parmi un [catalogue en libre-service](./catalog/overview.md) de toutes les destinations disponibles dans la plateforme de données clients en temps réel.
* Utilisez les **[!UICONTROL destinations]** pour [activer](./ui/activate-destinations.md) et envoyer des profils ou des segments aux plateformes d’automatisation marketing, de publicité numérique, etc.
* Planifiez régulièrement des exportations de données vers les destinations de votre choix.

## Commandes {#controls}

Les commandes de l’[espace de travail des destinations](./ui/destinations-workspace.md) vous permettent d’effectuer les opérations suivantes :

* parcourir le catalogue des plateformes de destination dans lesquelles vous pouvez activer vos données ;
* créer, modifier, activer et désactiver des flux de données vers les destinations du catalogue ;
* créer un compte dans un emplacement de stockage ou lier la plateforme des données clients en temps réel au compte dans la plateforme des destinations ;
* sélectionner les segments à activer vers les destinations ;
* sélectionner les [champs XDM](../xdm/home.md) à exporter lors de l’activation de segments vers des destinations de marketing par e-mail.

## Types et catégories de destination {#types-and-categories}

Pour plus d’informations, consultez la [présentation des types et catégories de destination](./destination-types.md).

## Destinations et contrôles d’accès {#access-controls}

La fonctionnalité de destinations de la plateforme de données clients en temps réel fonctionne avec les autorisations de contrôle d’accès d’Adobe Experience Platform. Selon le niveau d’autorisation de l’utilisateur, vous pouvez afficher, gérer et activer les destinations. Pour plus d’informations sur les autorisations individuelles, consultez [Contrôle d’accès dans Adobe Experience Platform](../access-control/home.md) et faites défiler la page vers le bas.

Pour plus d’informations sur les contrôles d’accès, consultez le [Guide de l’utilisateur du contrôle d’accès](../access-control/ui/overview.md).

## [!DNL Data Governance] restrictions sur l’activation des données vers les destinations {#data-governance}

La gouvernance des données est appliquée pour les destinations CDP en temps réel par le biais :

* *Cas* d’utilisation marketing que vous pouvez sélectionner dans le processus de création de destinations ;
* *Stratégies* d’utilisation des données qui limitent l’activation des données contenant certaines étiquettes d’utilisation vers des destinations présentant certains cas d’utilisation marketing.

Pour plus d’informations sur les cas [!DNL Data Governance] d’utilisation [marketing et la](../rtcdp/privacy/data-governance-overview.md#destinations) résolution des violations [](../rtcdp/privacy/data-governance-overview.md#enforcement)de la stratégie de données, voir la documentation CDP en temps réel.

Pour plus d’informations sur la sélection des cas d’utilisation marketing dans le flux de travail de création de destination, voir les pages suivantes pour les différents types de destination dans le CDP en temps réel :

* [Destinations publicitaires - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Destinations publicitaires - Publicités Google](./catalog/advertising/google-ads-destination.md)
* [Destinations publicitaires - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Destinations de stockage dans le cloud](./catalog/cloud-storage/workflow.md)
* [Destinations de marketing par e-mail](./catalog/email-marketing/overview.md)
* [Destinations de réseau social](./catalog/social/workflow.md)

Pour plus d’informations sur les violations de la stratégie de données dans le processus d’activation des segments, voir l’étape de révision dans [Activation des profils et des segments vers une destination](./ui/activate-destinations.md#review).
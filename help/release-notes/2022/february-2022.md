---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 3ae4d0f0a92c96b15c605c6654693fd6d7e94ba8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 41%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : 23 février 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [Sources](#sources)

## Collecte de données {#data-collection}

Platform fournit une suite de technologies qui vous permet de collecter des données d’expérience client côté client et de les envoyer au réseau Adobe Experience Platform Edge où elles peuvent être enrichies, transformées et distribuées vers des destinations Adobe ou non Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Amélioration du workflow de l’interface utilisateur pour la configuration des flux de données | Le workflow de création d’un nouveau flux de données dans l’interface utilisateur de collecte de données a été mis à jour. Lors de l’ajout de services à un flux de données, seuls les services auxquels vous avez accès seront inclus dans la liste des options. Consultez le guide sur la [configuration d’un flux de données](../../edge/fundamentals/datastreams.md) pour plus d’informations. |
| Préparation de données pour la collecte de données | Si vous utilisez le SDK Web de Adobe Experience Platform, vous pouvez désormais tirer parti des fonctionnalités de préparation des données pour mapper vos données au modèle de données d’expérience (XDM) côté serveur. Voir la section sur [Préparation de données pour la collecte de données](../../edge/fundamentals/datastreams.md#data-prep) dans le guide datastreams pour plus d’informations. |
| Identifiants d’appareils propriétaires | Vous pouvez désormais envoyer vos propres ID d’appareil au réseau Adobe Experience Platform Edge lors de la collecte de données client à l’aide du SDK Web Platform, ce qui vous permet de contourner les restrictions récentes du navigateur sur la durée de vie des cookies tiers. Consultez le guide sur la [identifiants d’appareils propriétaires](../../edge/identity/first-party-device-ids.md) pour plus d’informations. |

Pour plus d’informations sur la collecte de données dans Platform, voir [présentation de la collecte de données](../../collection/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM). 

**Nouvelle fonctionnalité**

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Data Prep] Prise en charge du connecteur source Adobe Analytics | Le connecteur source Adobe Analytics prend désormais en charge les fonctionnalités de préparation de données, ce qui vous permet de mapper vos données de suite de rapports Analytics à un schéma XDM cible lors de la création d’un flux de données. Voir le tutoriel sur [création d’un connecteur source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) pour plus d’informations. |

Pour plus d’informations sur [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## [!DNL Identity Service] {#identity}

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leur comportement en rapprochant des identités entre les appareils et les systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelle autorisation pour `view-identity-graph` | Vous pouvez désormais utiliser la variable `view-identity-graph` autorisation de contrôler si les utilisateurs de votre entreprise peuvent afficher des données de graphique d’identités. Les utilisateurs ne disposant pas de cette autorisation ne pourront pas accéder à la visionneuse de graphiques d’identités dans l’interface utilisateur ou lors de l’accès à [!DNL Identity Service] API qui renvoient des identités. Voir [présentation du contrôle d’accès](../../access-control/home.md) pour plus d’informations sur les autorisations. |

Pour des informations plus générales sur le [!DNL Identity Service], reportez-vous à la [présentation du service d’identités](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Sources bêta passant à la version générale | Les sources suivantes ont été promues de la version bêta à la version générale : <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).

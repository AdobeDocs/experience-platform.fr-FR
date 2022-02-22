---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
source-git-commit: 762a4b7336f1c26b79883db9484d8f5fc7bff53c
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 62%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : 23 février 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [Sources](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM). 

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Data Prep] Prise en charge du connecteur source Adobe Analytics | Le connecteur source Adobe Analytics prend désormais en charge les fonctionnalités de préparation de données, ce qui vous permet de mapper vos données de suite de rapports Analytics à un schéma XDM cible lors de la création d’un flux de données. Voir le tutoriel sur [création d’un connecteur source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) pour plus d’informations. |

Pour plus d’informations sur [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## [!DNL Identity Service] {#identity}

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leur comportement en rapprochant des identités entre les appareils et les systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelle autorisation pour `view-identity-graph` | Vous pouvez désormais utiliser la variable `view-identity-graph` autorisation de contrôler si les utilisateurs de votre entreprise peuvent afficher des données de graphique d’identités. Les utilisateurs ne disposant pas de cette autorisation ne pourront pas accéder à la visionneuse de graphiques d’identités dans l’interface utilisateur ou lors de l’accès à [!DNL Identity Service] API qui renvoient des identités. Voir [présentation du contrôle d’accès](../../access-control/home.md) pour plus d’informations sur les autorisations. |

Pour des informations plus générales sur le [!DNL Identity Service], reportez-vous à la [présentation du service d’identités](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Sources bêta passant à la version générale | Les sources suivantes ont été promues de la version bêta à la version générale : <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).

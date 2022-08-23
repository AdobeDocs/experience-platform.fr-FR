---
title: Notes de mise à jour de Adobe Experience Platform - Août 2022
description: Notes de mise à jour d’août 2022 pour Adobe Experience Platform.
source-git-commit: 925991d58c3cdd84e13b12a095e9681b8f4b254b
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 35%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 24 août 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Préparation de données](#data-prep)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Sources](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM). 

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’ingestion d’enregistrements avec des avertissements | La préparation des données localisera désormais les avertissements (erreurs non critiques) dans les champs et permettra d’ingérer le reste de la ligne. Toutes les erreurs de transformation du mappeur sont désormais signalées comme avertissements et les lignes partiellement ingérées sont considérées comme réussies, avec un avertissement.  La surveillance est également prise en charge sur les enregistrements avec des avertissements et des informations de diagnostic. Actuellement, l’ingestion partielle des enregistrements avec avertissements n’est disponible que pour la diffusion en continu des données. Consultez la documentation sur [ingestion d’enregistrements avec des avertissements](../../sources/tutorials/ui/monitor-streaming.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur [!DNL Data Prep], consultez la présentation de [[!DNL Data Prep] ](../../data-prep/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Schéma global | [[!UICONTROL Schéma d’entité AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Décrit les entités dénormalisées pour Adobe Journey Optimizer. |
| Classe | [[!UICONTROL Entités d’exécution AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Décrit les entités d’exécution Adobe Journey Optimizer à utiliser dans la segmentation. |
| Groupe de champs | [[!UICONTROL Objets de travail Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Groupe de champs wrapper qui référence tous les groupes de champs spécifiques à l’objet de niveau inférieur pour Adobe Workfront. |

{style=&quot;table-layout:auto&quot;}

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [[!UICONTROL Champs communs des événements d’étape du Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Deux nouvelles propriétés ont été ajoutées : `origTimeStamp` et `experienceID`. |
| Groupe de champs | [[!UICONTROL Détails de l’appartenance à un segment]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | En complément de [!UICONTROL XDM Individual Profile], ce groupe de champs peut désormais être utilisé dans les schémas basés sur la classe XDM Business Account . |
| Groupe de champs | (Multiple) | Plusieurs groupes de champs liés aux activités Marketo B2B ont été mis à jour vers un état stable. Voir ce qui suit : [requête d’extraction](https://github.com/adobe/xdm/pull/1593/files) pour plus d’informations. |
| Groupe de champs | (Multiple) | Plusieurs groupes de champs liés à la météo ont été mis à jour afin de corriger les erreurs qui se produisaient pour `uvIndex` et `sunsetTime`. Voir ce qui suit : [requête d’extraction](https://github.com/adobe/xdm/pull/1602/files) pour plus d’informations. |
| Type de données | [[!UICONTROL Élément de liste de produits]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Une nouvelle propriété `productImageUrl` a été ajouté. |
| Type de données | [[!UICONTROL Informations détaillées sur les données de la QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Une nouvelle propriété `framesPerSecond` a été ajouté. |
| Type de données | [[!UICONTROL Informations détaillées sur la session]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` a été renommé `appVersion`. `meta:enum` et `description` ont également été mises à jour. |
| Types de données et groupes de champs | (Multiple) | Plusieurs types de données et groupes de champs de médias comportent de nouveaux champs et des descriptions mises à jour. Voir ce qui suit : [requête d’extraction](https://github.com/adobe/xdm/pull/1582/files) pour plus d’informations. |
| (Toutes) | (Multiple) | Tous les objets de schéma qui contiennent une propriété `enum` contient désormais également un champ correspondant. `meta:enum` champ pour indiquer les valeurs d’affichage de chaque contrainte. Voir ce qui suit : [requête d’extraction](https://github.com/adobe/xdm/pull/1601/files) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale des sources en libre-service (SDK par lots) | Développez, testez et intégrez votre source de données basée sur l’API REST pour ingérer des données de lot dans Experience Platform à l’aide de spécifications de source faciles à configurer. Avec le SDK Sources, vous pouvez : <ul><li>Configurez une nouvelle source pour le catalogue Experience Platform.</li><li>Définissez les spécifications de votre source, y compris les informations relatives aux types d’authentification pris en charge, à la planification et à la manière dont les données de ressource sont récupérées.</li><li>Créez une documentation destinée aux utilisateurs pour votre nouvelle source.</li></ul> Pour plus d’informations, consultez la documentation sur [Sources en libre-service (SDK par lots)](../../sources/sources-sdk/overview.md). |
| Disponibilité générale de la source [!DNL Google BigQuery] | Utilisez la variable [!DNL Google BigQuery] source pour ingérer des données à partir de votre [!DNL Google BigQuery] entrepôt de données vers Experience Platform. Pour plus d’informations, consultez la documentation relative à la [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] source (bêta) | Utilisez la variable [!DNL Teradata Vantage] source pour ingérer des données à partir d’environnements multicloud hybrides vers Experience Platform. Pour plus d’informations, consultez la documentation relative à la [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Prise en charge inter-régions de la source Adobe Analytics | Vous pouvez désormais ingérer des suites de rapports à partir de n’importe quelle région (États-Unis, Royaume-Uni ou Singapour). Les suites de rapports doivent être mappées à la même organisation que l’instance Sandbox Experience Platform dans laquelle la connexion source est créée. Pour plus d’informations, consultez le guide sur [création d’une connexion source Adobe Analytics dans l’interface utilisateur](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Prise en charge des API pour l’ingestion à la demande | Utilisez l’ingestion à la demande pour créer des exécutions de flux ad hoc pour un flux de données donné avec la variable [!DNL Flow Service] API. Les exécutions de flux créées doivent être définies sur une ingestion unique. Pour plus d’informations, consultez le guide sur [création d’une exécution de flux pour l’ingestion à la demande à l’aide de l’API](../../sources/tutorials/api/on-demand-ingestion.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).

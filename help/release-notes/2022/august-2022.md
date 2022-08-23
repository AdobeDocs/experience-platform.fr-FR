---
title: Notes de mise à jour de Adobe Experience Platform - Août 2022
description: Notes de mise à jour d’août 2022 pour Adobe Experience Platform.
source-git-commit: b8513fa214ea74eec6809796cc194466e05cbb21
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 32%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 24 août 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Préparation de données](#data-prep)
- [Sources](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM). 

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’ingestion d’enregistrements avec des avertissements | La préparation des données localisera désormais les avertissements (erreurs non critiques) dans les champs et permettra d’ingérer le reste de la ligne. Toutes les erreurs de transformation du mappeur sont désormais signalées comme avertissements et les lignes partiellement ingérées sont considérées comme réussies, avec un avertissement.  La surveillance est également prise en charge sur les enregistrements avec des avertissements et des informations de diagnostic. Actuellement, l’ingestion partielle des enregistrements avec avertissements n’est disponible que pour la diffusion en continu des données. Consultez la documentation sur [ingestion d’enregistrements avec des avertissements](../../sources/tutorials/ui/monitor-streaming.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur [!DNL Data Prep], consultez la présentation de [[!DNL Data Prep] ](../../data-prep/home.md).

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

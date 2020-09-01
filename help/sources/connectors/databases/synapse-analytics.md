---
keywords: Experience Platform;home;popular topics;Azure Synapse Analytics;azure synapse analytics;Synapse;synapse
solution: Experience Platform
title: Connecteur Azure Synapse Analytics
topic: overview
description: La documentation ci-dessous fournit des informations sur la façon de connecter Azure Synapse Analytics à Platform à l'aide d'API ou de l'interface utilisateur.
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 12%

---


# (Bêta) [!DNL Azure Synapse Analytics] Connecteur

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’une base de données tierce. [!DNL Platform] peut se connecter à différents types de bases de données, telles que relationnelles, NoSQL ou des entrepôts de données. Les fournisseurs de base de données sont pris en charge [!DNL Azure Synapse Analytics].

## LISTE AUTORISÉE d&#39;adresse IP

Les adresses IP suivantes doivent être ajoutées à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources.

### Région est-américaine

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Région de l&#39;Europe occidentale

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australie-Est

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Azure Synapse Analytics] à [!DNL Platform] l’aide des API ou de l’interface utilisateur :

## Se connecter [!DNL Azure Synapse Analytics] à [!DNL Platform] l’aide des API

- [Création d&#39;un connecteur Azure Synapse Analytics à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/create/databases/synapse-analytics.md)
- [Exploration d’un système de base de données à l’aide de l’API du service de flux](../../tutorials/api/explore/database-nosql.md)
- [Collecte de données à partir d’une base de données à l’aide de l’API du service de flux](../../tutorials/api/collect/database-nosql.md)

## Se connecter [!DNL Azure Synapse Analytics] à [!DNL Platform] l’aide de l’interface utilisateur

- [Création d&#39;un connecteur source Azure Synapse Analytics dans l&#39;interface utilisateur](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Configuration d’un flux de données pour un connecteur de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
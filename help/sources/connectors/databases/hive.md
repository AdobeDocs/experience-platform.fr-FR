---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Apache Hive sur le connecteur Azure HDInsights
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 11%

---


# (Bêta) [!DNL Apache Hive] sur le [!DNL Azure HDInsights] connecteur

>[!NOTE]
>
>Le connecteur Apache Hive sur Azure HDInsights est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../home.md#terms-and-conditions) sources.

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’une base de données tierce. [!DNL Platform] peut se connecter à différents types de bases de données, telles que relationnelles, NoSQL ou des entrepôts de données. La prise en charge des fournisseurs de base de données inclut [!DNL Apache Hive] l&#39;activation [!DNL Azure HDInsights].

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

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Apache Hive][!DNL Azure HDInsights] à [!DNL Platform] l’aide des API ou de l’interface utilisateur :

## Se connecter [!DNL Apache Hive] à [!DNL Azure HDInsights][!DNL Platform] à l’aide des API

- [Création d&#39;une Apache Hive sur le connecteur Azure HDInsights à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/create/databases/hive.md)
- [Exploration d’un système de base de données à l’aide de l’API du service de flux](../../tutorials/api/explore/database-nosql.md)
- [Collecte de données à partir d’une base de données à l’aide de l’API du service de flux](../../tutorials/api/collect/database-nosql.md)

## Se connecter [!DNL Apache Hive] à [!DNL Azure HDInsights][!DNL Platform] à l&#39;aide de l&#39;interface utilisateur

- [Création d&#39;un Apache Hive sur le connecteur source Azure HDInsights dans l&#39;interface utilisateur](../../tutorials/ui/create/databases/hive.md)
- [Configuration d’un flux de données pour un connecteur de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
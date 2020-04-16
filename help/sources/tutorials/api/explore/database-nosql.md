---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exploration d’une base de données ou d’un système NoSQL à l’aide de l’API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 4c34ecdaeb4a0df1faf2dd54e8a264b9126f20b4

---


# Exploration d’une base de données ou d’un système NoSQL à l’aide de l’API Flow Service

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API Flow Service pour explorer des bases de données ou des systèmes NoSQL.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
* [Sandbox](../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à une base de données ou à un système NoSQL à l’aide de l’API Flow Service.

### Obtention d’une connexion de base

Pour explorer votre base de données ou votre système NoSQL à l’aide des API Platform, vous devez posséder un ID de connexion de base valide. Si vous ne disposez pas déjà d’une connexion de base pour la base de données ou le système NoSQL avec lequel vous souhaitez travailler, vous pouvez en créer une à l’aide des didacticiels suivants :

* [Amazon Redshift](../create/databases/redshift.md)
* [Apache Spark sur Azure HDInsights ](../create/databases/spark.md)
* [Azure Synapse Analytics](../create/databases/synapse-analytics.md)
* [de table Azure](../create/databases/ats.md)
* [Google BigQuery](../create/databases/bigquery.md)
* [Hiver](../create/databases/hive.md)
* [MariaDB](../create/databases/mariadb.md)
* [MySQL](../create/databases/mysql.md)
* [Phoenix](../create/databases/phoenix.md)
* [PostgreSQL](../create/databases/postgres.md)
* [SQL Server ](../create/databases/sql-server.md)

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type : `application/json`

## Explorez vos tableaux de données

En utilisant la connexion de base pour votre base de données ou votre système NoSQL, vous pouvez explorer vos tableaux de données en exécutant des requêtes GET. Utilisez l&#39;appel suivant pour trouver le chemin du tableau que vous souhaitez inspecter ou assimiler dans Platform.

**Format API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID d’une base de données ou connexion de base NoSQL. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de tables de votre base de données ou système NoSQL. Trouvez la table que vous souhaitez amener dans Plateforme et prenez note de sa `path` propriété, comme vous devez le fournir dans l&#39;étape suivante pour inspecter sa structure.

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Vérification de la structure d’un tableau

Pour inspecter la structure d&#39;une table à partir de votre base de données ou du système NoSQL, exécutez une requête GET tout en spécifiant le chemin d&#39;une table comme paramètre .

**Format API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID d’une base de données ou connexion de base NoSQL. |
| `{TABLE_PATH}` | Chemin d’accès d’un tableau. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure du tableau spécifié. Les détails concernant chacune des colonnes du tableau sont situés dans les éléments du `columns` tableau.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "TestID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez exploré votre base de données ou votre système NoSQL, trouvé le chemin de la table que vous souhaitez intégrer dans Platform, et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter les données de votre base de données ou système NoSQL et les importer dans Platform](../collect/database-nosql.md).
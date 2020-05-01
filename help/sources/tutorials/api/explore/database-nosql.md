---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exploration d’une base de données à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: c4162d88a688ce2028de08b63e7b7eab954a0e29

---


# Exploration d’une base de données à l’aide de l’API du service de flux

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API Flow Service pour explorer le contenu et la structure de fichiers d’une base de données tierce.

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plate-forme.
* [Sandbox](../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à une base de données tierce à l’aide de l’API Flow Service.

### Collecte des informations d’identification requises

Ce didacticiel vous oblige à établir une connexion valide avec la base de données tierce à partir de laquelle vous souhaitez importer des données. Une connexion valide implique l&#39;ID de spécification de connexion et l&#39;ID de connexion de votre base de données. Pour plus d’informations sur la création d’une connexion à une base de données et la récupération de ces valeurs, consultez l’aperçu [des connecteurs](./../../../home.md#database)source.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Explorez vos tableaux de données

A l’aide de l’ID de connexion de votre base de données, vous pouvez explorer vos tables de données en exécutant des requêtes GET. Utilisez l&#39;appel suivant pour trouver le chemin d&#39;accès de la table que vous souhaitez inspecter ou assimiler dans la plate-forme.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID d’une connexion à la base de données. |

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de tables de votre base de données. Trouvez la table que vous souhaitez apporter à Plateforme et prenez note de sa `path` propriété, car vous devez la fournir à l&#39;étape suivante pour inspecter sa structure.

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

## Inspecter la structure d’un tableau

Pour inspecter la structure d&#39;une table à partir de votre base de données, exécutez une requête GET tout en spécifiant le chemin d&#39;une table en tant que paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID d’une connexion à la base de données. |
| `{TABLE_PATH}` | Chemin d’accès d’un tableau. |

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure de la table spécifiée. Les détails concernant chacune des colonnes du tableau se trouvent dans les éléments du `columns` tableau.

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

En suivant ce tutoriel, vous avez exploré votre base de données, trouvé le chemin de la table que vous souhaitez intégrer dans Platform, et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter des données de votre base de données et les importer dans Platform](../collect/database-nosql.md).
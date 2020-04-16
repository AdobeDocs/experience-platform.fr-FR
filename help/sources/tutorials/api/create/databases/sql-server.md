---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur SQL Server à l’aide de l’API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 173faf861ca8feb6dd4e2159b0708e41fa0f601f

---


# Création d’un connecteur Microsoft SQL Server à l’aide de l’API Flow Service

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API Flow Service pour vous guider tout au long des étapes nécessaires à la connexion d’Experience Platform à un serveur Microsoft SQL (ci-après dénommé &quot;SQL Server&quot;).

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à SQL Server à l’aide de l’API Flow Service.

### Collecte des informations d’identification requises

Pour vous connecter à SQL Server, vous devez fournir la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion associée à votre compte SQL Server. |

Pour plus d&#39;informations sur la prise en main de SQL Server, reportez-vous à [ce](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server) .

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../../../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type : `application/json`

## Rechercher les spécifications de connexion

Pour créer une connexion SQL Server, un ensemble de spécifications de connexion SQL Server doit exister dans le service de flux. La première étape de la connexion de Platform à SQL Server consiste à récupérer ces spécifications.

**Format API**

Chaque source disponible possède son propre jeu de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d’authentification. L’envoi d’une requête GET au `/connectionSpecs` point de fin renverra les spécifications de connexion pour toutes les sources disponibles. Vous pouvez également inclure le `property=name=="sql-server"` pour obtenir des informations spécifiques à SQL Server.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="sql-server"
```

**Requête**

La requête suivante récupère les spécifications de connexion pour SQL Server.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="sql-server"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les spécifications de connexion pour SQL Server, y compris son identifiant unique (`id`). Cet ID est requis à l’étape suivante pour créer une connexion de base.

```json
{
    "items": [
        {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "name": "sql-server",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Connection String Based Authentication",
                    "type": "connectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to SQL Server database",
                        "properties": {
                            "connectionString": {
                                "type": "string",
                                "description": "connection string to connect to any SQL Server database.",
                                "format": "password",
                                "pattern": "^(Data Source=)(.*)(;Initial Catalog=)(.*)(;Integrated Security=)(.*)(;User ID=)(.*)(;Password=)(.*)(;)",
                                "examples": [
                                    "Data Source=<servername>\\<instance name if using named instance>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;"
                                ]
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Créer une connexion de base

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base est requise par compte SQL Server, car elle peut être utilisée pour créer plusieurs connecteurs source afin d&#39;importer des données différentes.

**Format API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for sql-server",
        "description": "Base connection for sql-server",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "version": "1.0"
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion associée à votre authentification SQL Server. |
| `connectionSpec.id` | Spécification de connexion (`id`) collectée à l’étape précédente. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion de base SQL Server à l’aide de l’API Flow Service et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet ID de connexion de base dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données ou des systèmes NoSQL à l’aide de l’API](../../explore/database-nosql.md)Flow Service.

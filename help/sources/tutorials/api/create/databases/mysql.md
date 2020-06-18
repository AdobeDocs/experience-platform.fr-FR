---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur MySQL à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: e4ed6ae3ee668cd0db741bd07d2fb7be593db4c9
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---


# Création d’un connecteur MySQL à l’aide de l’API du service de flux

>[!NOTE]
>Le connecteur MySQL est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Le service de flux permet de collecter et de centraliser les données client provenant de diverses sources disparates au sein de l’Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API du service de flux pour vous guider dans les étapes de connexion de l’Experience Platform à MySQL.

## Prise en main

Ce guide exige une compréhension pratique des éléments suivants de l&#39;Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance Platform unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à MySQL à l’aide de l’API de service de flux.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte à votre enregistrement MySQL, vous devez fournir la valeur de la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion MySQL associée à votre compte. Le modèle de chaîne de connexion MySQL est le suivant : `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | ID utilisé pour générer une connexion. L&#39;ID de spécification de connexion fixe pour MySQL est `26d738e0-8963-47ea-aadf-c60de735468a`. |

Pour plus d&#39;informations sur l&#39;obtention d&#39;une chaîne de connexion, consultez [ce document](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)MySQL.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de l’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour passer des appels aux API Platform, vous devez d’abord suivre le didacticiel [d’](../../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources en Experience Platform, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte MySQL, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion MySQL, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande POST. L’ID de spécification de connexion pour MySQL est `26d738e0-8963-47ea-aadf-c60de735468a`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "MySQL Test Connection",
        "description": "MySQL Test Connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "26d738e0-8963-47ea-aadf-c60de735468a",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion MySQL associée à votre compte. Le modèle de chaîne de connexion MySQL est le suivant : `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | ID de spécification de connexion fixe pour MySQL : `26d738e0-8963-47ea-aadf-c60de735468a`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre base de données dans le didacticiel suivant.

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion MySQL à l’aide de l’API Flow Service et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet ID de connexion dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données ou des systèmes NoSQL à l’aide de l’API](../../explore/database-nosql.md)Flow Service.
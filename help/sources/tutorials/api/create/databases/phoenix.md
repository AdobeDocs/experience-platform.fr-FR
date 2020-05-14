---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur Phoenix à l’aide de l’API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 1%

---


# Création d’un connecteur Phoenix à l’aide de l’API Flow Service

>[!NOTE]
>Le connecteur Phoenix est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API Flow Service pour vous guider à travers les étapes de connexion d’une base de données Phoenix à la plate-forme Experience.

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plate-forme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à Phoenix à l’aide de l’API Flow Service.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte à Phoenix, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur Phoenix. |
| `username` | Nom d’utilisateur utilisé pour accéder au serveur Phoenix. |
| `password` | Mot de passe correspondant à l’utilisateur. |
| `port` | port TCP utilisé par le serveur Phoenix pour écouter les connexions client. Si vous vous connectez à Azure HDInsights, spécifiez le port 443. |
| `httpPath` | URL partielle correspondant au serveur Phoenix. Spécifiez /hbasephoenix0 si vous utilisez la grappe Azure HDInsights. |
| `enableSsl` | Valeur booléenne. Indique si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour Phoenix est : `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://python-phoenixdb.readthedocs.io/en/latest/api.html)Phoenix.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte Phoenix, car elle peut être utilisée pour créer plusieurs connecteurs source afin d&#39;importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion Phoenix, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande POST. L&#39;ID de spécification de connexion pour Phoenix est `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | Hôte du serveur Phoenix. |
| `auth.params.username` | Nom d’utilisateur associé à votre connexion Phoenix. |
| `auth.params.password` | Mot de passe associé à votre connexion Phoenix. |
| `auth.params.port` | Port TCP de votre connexion Phoenix. |
| `auth.params.httpPath` | Chemin d’accès HTTP partiel pour votre connexion Phoenix. |
| `auth.params.enableSsl` | Valeur booléenne qui spécifie si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | ID de spécification de connexion Phoenix : `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion Phoenix à l’aide de l’API Flow Service et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données à l’aide de l’API](../../explore/database-nosql.md)Flow Service.
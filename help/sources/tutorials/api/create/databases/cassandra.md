---
keywords: Experience Platform;home;popular topics;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Création d’un connecteur Apache Cassandra à l’aide de l’API Flow Service
topic: overview
type: Tutorial
description: Ce didacticiel utilise l’API Flow Service pour vous guider à travers les étapes permettant de connecter Apache Cassandra (ci-après appelée "Cassandra") à un Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 16%

---


# Création d’un [!DNL Apache Cassandra] connecteur à l’aide de l’ [!DNL Flow Service] API

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce tutoriel utilise l&#39; [!DNL Flow Service] API pour vous guider dans les étapes de connexion [!DNL Apache Cassandra] (ci-après appelée &quot;Cassandra&quot;) à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to Cassandra using the [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] établir une connexion avec [!DNL Cassandra], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du [!DNL Cassandra] serveur. |
| `port` | port TCP utilisé par le [!DNL Cassandra] serveur pour écouter les connexions client. Le port par défaut est `9042`. |
| `username` | Nom d’utilisateur utilisé pour la connexion au [!DNL Cassandra] serveur pour l’authentification. |
| `password` | Mot de passe de connexion au [!DNL Cassandra] serveur pour l’authentification. |
| `connectionSpec.id` | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour [!DNL Cassandra] est `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://cassandra.apache.org/doc/latest/operating/security.html#authentication)Cassandra.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Un seul connecteur est nécessaire par [!DNL Cassandra] compte, car il peut être utilisé pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une [!DNL Cassandra] connexion, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL Cassandra] est `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.host` | Adresse IP ou nom d’hôte du [!DNL Cassandra] serveur. |
| `auth.params.port` | port TCP utilisé par le [!DNL Cassandra] serveur pour écouter les connexions client. Le port par défaut est `9042`. |
| `auth.params.username` | Nom d’utilisateur utilisé pour la connexion au [!DNL Cassandra] serveur pour l’authentification. |
| `auth.params.password` | Mot de passe de connexion au [!DNL Cassandra] serveur pour l’authentification. |
| `connectionSpec.id` | ID de la spécification de [!DNL Cassandra] connexion : `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une [!DNL Cassandra] connexion à l’aide de l’ [!DNL Flow Service] API et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données à l’aide de l’API](../../explore/database-nosql.md)Flow Service.

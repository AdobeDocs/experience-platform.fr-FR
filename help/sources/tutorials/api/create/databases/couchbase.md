---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur Couchbase à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 18%

---


# Création d’un [!DNL Couchbase] connecteur à l’aide de l’ [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL Couchbase] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

[!DNL Flow Service] sert à collecter et à centraliser les données client provenant de diverses sources disparates pour les importer dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API du service de flux pour vous guider à travers les étapes de la connexion [!DNL Couchbase] à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL Couchbase] using the [!DNL Flow Service] API.

### Collecte des informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL Couchbase] instance. Le modèle de chaîne de connexion pour [!DNL Couchbase] est `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Pour plus d&#39;informations sur l&#39;acquisition d&#39;une chaîne de connexion, consultez [ce document](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)Couchbase. |
| `connectionSpec.id` | Identificateur nécessaire pour créer une connexion. L&#39;ID de spécification de connexion fixe pour [!DNL Couchbase] est `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Un seul connecteur est nécessaire par [!DNL Couchbase] compte, car il peut être utilisé pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

The following request creates a new [!DNL Couchbase] connection, configured by the properties provided in the payload:.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Couchbase test connection",
        "description": "A test connection for a Couchbase source",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                    "connectionString": "Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];"
                }
        },
        "connectionSpec": {
            "id": "1fe283f6-9bec-11ea-bb37-0242ac130002",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour la connexion à un [!DNL Couchbase] compte. Le modèle de chaîne de connexion est le suivant : `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. |
| `connectionSpec.id` | ID de la spécification de [!DNL Couchbase] connexion : `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

**Réponse**

A successful response returns the details of the newly created connection, including its unique identifier (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "54997109-07b5-40b7-9971-0907b5a0b75a",
    "etag": "\"280168f5-0000-0200-0000-5ed72b230000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une [!DNL Couchbase] connexion à l’aide de l’ [!DNL Flow Service] API et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données à l’aide de l’API](../../explore/database-nosql.md)Flow Service.

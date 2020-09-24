---
keywords: Experience Platform;home;popular topics;greenplum;Greenplum
solution: Experience Platform
title: Création d’un connecteur GreenPlum à l’aide de l’API du service de flux
topic: overview
type: Tutorial
description: Ce didacticiel utilise l’API du service de flux pour vous guider à travers les étapes nécessaires à la connexion de GreenPlum à l’Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 16%

---


# Création d’un [!DNL GreenPlum] connecteur à l’aide de l’ [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL GreenPlum] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [!DNL Flow Service] API pour vous guider à travers les étapes de la connexion [!DNL GreenPlum] à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL GreenPlum] using the [!DNL Flow Service] API.

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL GreenPlum] instance. Le modèle de chaîne de connexion pour [!DNL GreenPlum] est `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | Identificateur nécessaire pour créer une connexion. L&#39;ID de spécification de connexion fixe pour [!DNL GreenPlum] est `37b6bf40-d318-4655-90be-5cd6f65d334b`. |

Pour plus d&#39;informations sur l&#39;acquisition d&#39;une chaîne de connexion, consultez [ce document](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn)GreenPlum.

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

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Un seul connecteur est nécessaire par [!DNL GreenPlum] compte, car il peut être utilisé pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une [!DNL GreenPlum] connexion, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL GreenPlum] est `37b6bf40-d318-4655-90be-5cd6f65d334b`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "GreenPlum test connection",
        "description": "A test connection for a GreenPlum source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "connectionString": "HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "37b6bf40-d318-4655-90be-5cd6f65d334b",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour la connexion à un [!DNL GreenPlum] compte. Le modèle de chaîne de connexion est le suivant : `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | ID de la spécification de [!DNL GreenPlum] connexion : `37b6bf40-d318-4655-90be-5cd6f65d334b`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une [!DNL GreenPlum] connexion à l’aide de l’ [!DNL Flow Service] API et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données à l’aide de l’API](../../explore/database-nosql.md)Flow Service.

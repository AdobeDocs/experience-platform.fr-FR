---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur HubSpot à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 15%

---


# Création d’un [!DNL HubSpot] connecteur à l’aide de l’ [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL HubSpot] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [!DNL Flow Service] API pour vous guider à travers les étapes de la connexion [!DNL Experience Platform] à [!DNL HubSpot].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL HubSpot] using the [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] se connecter à [!DNL HubSpot], vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| ID client | ID client associé à votre [!DNL HubSpot] application. |
| Secret client | Le secret client associé à votre [!DNL HubSpot] application. |
| jeton d&#39;accès | Jeton d&#39;accès obtenu lors de l’authentification initiale de l’intégration OAuth. |
| Actualiser le jeton | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |
| ID de spécification de connexion | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour [!DNL HubSpot] est : `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Pour plus d&#39;informations sur la prise en main, reportez-vous à ce document [](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)HubSpot.

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

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par [!DNL HubSpot] compte, car elle peut être utilisée pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```https
POST /connections
```

**Requête**

Pour créer une [!DNL HubSpot] connexion, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL HubSpot] est `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.clientId` | ID client associé à votre [!DNL HubSpot] application. |
| `auth.params.clientSecret` | Le secret client associé à votre [!DNL HubSpot] application. |
| `auth.params.accessToken` | Jeton d&#39;accès obtenu lors de l’authentification initiale de l’intégration OAuth. |
| `auth.params.refreshToken` | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée pour l’API, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

En suivant ce didacticiel, vous avez créé une [!DNL HubSpot] connexion à l’aide de l’ [!DNL Flow Service] API et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant de connexion dans le didacticiel suivant lorsque vous apprendrez à [explorer les systèmes d’automatisation marketing à l’aide de l’API](../../explore/marketing-automation.md)de service de flux.
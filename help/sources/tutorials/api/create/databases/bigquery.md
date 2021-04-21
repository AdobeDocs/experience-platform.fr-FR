---
keywords: Experience Platform;accueil;rubriques populaires;bigquery;Google;google;Google BigQuery
solution: Experience Platform
title: Création d’une connexion à la source Google BigQuery à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Google BigQuery à l’aide de l’API de service de flux.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 23%

---

# Créez une connexion source [!DNL Google BigQuery] à l’aide de l’API [!DNL Flow Service].

>[!NOTE]
>
>Le connecteur [!DNL Google BigQuery] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider dans les étapes de connexion de [!DNL Experience Platform] à [!DNL Google BigQuery] (ci-après appelée &quot;BigQuery&quot;).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à BigQuery à l&#39;aide de l&#39;API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] connecte BigQuery à la plate-forme, vous devez fournir les valeurs d&#39;authentification OAuth 2.0 suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `project` | ID du projet [!DNL BigQuery] par défaut à requête. |
| `clientID` | Valeur d’ID utilisée pour générer le jeton d’actualisation. |
| `clientSecret` | Valeur secrète utilisée pour générer le jeton d’actualisation. |
| `refreshToken` | Jeton d’actualisation obtenu à partir de [!DNL Google] utilisé pour autoriser l’accès à [!DNL BigQuery]. |

Pour plus d&#39;informations sur ces valeurs, consultez [ce document BigQuery](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte [!DNL BigQuery], car elle peut être utilisée pour créer plusieurs flux de données afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion [!DNL BigQuery], l&#39;identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL BigQuery] est `3c9b37f8-13a6-43d8-bad3-b863b941fedd`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.project` | ID du projet [!DNL BigQuery] par défaut à requête. contre. |
| `auth.params.clientId` | Valeur d’ID utilisée pour générer le jeton d’actualisation. |
| `auth.params.clientSecret` | Valeur cliente utilisée pour générer le jeton d’actualisation. |
| `auth.params.refreshToken` | Jeton d’actualisation obtenu à partir de [!DNL Google] utilisé pour autoriser l’accès à [!DNL BigQuery]. |
| `connectionSpec.id` | Spécification de connexion `id` de votre compte [!DNL BigQuery] récupérée à l&#39;étape précédente. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion [!DNL BigQuery] à l&#39;aide de l&#39;API [!DNL Flow Service] et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cet ID de connexion dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données ou des systèmes NoSQL à l’aide de l’API Flow Service](../../explore/database-nosql.md).

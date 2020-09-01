---
keywords: Experience Platform;home;popular topics;streaming connection;create streaming connection;api guide;tutorial;create a streaming connection;streaming ingestion;ingestion;
solution: Experience Platform
title: Création d’une connexion en continu à l’aide de l’API
topic: tutorial
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 62%

---


# Création d’une connexion en continu à l’aide de l’API

This tutorial will help you begin using streaming ingestion APIs, part of the Adobe Experience Platform Data [!DNL Ingestion Service] APIs.

## Prise en main

L’enregistrement d’une connexion en continu est requis pour commencer la diffusion des données en continu vers Adobe Experience Platform. Lors de l’enregistrement d’une connexion en continu, vous devez fournir des détails clés, tels que la source des données en continu.

Après avoir enregistré une connexion en continu, vous obtiendrez, en tant que producteur des données, une URL unique que vous pourrez utiliser pour diffuser en continu des données vers Platform.

Ce tutoriel nécessite également une connaissance pratique de divers services Adobe Experience Platform. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience.
- [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de plusieurs sources.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API d’ingestion par flux.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Création d’une connexion

Une connexion spécifie la source et contient les informations requises pour rendre le flux compatible avec les API d’ingestion par flux.

**Format d’API**

```http
POST /flowservice/connections
```

**Requête**

>[!NOTE]
>
>Les valeurs des variables répertoriées `providerId` et `connectionSpec` **doivent** être utilisées comme illustré dans l’exemple, car elles correspondent à ce qui indique à l’API que vous créez une connexion en continu pour l’ingestion par flux..

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec des informations sur la nouvelle connexion.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | L’`id` de votre nouvelle connexion. On parlera ici de `{CONNECTION_ID}`. |
| `etag` | Identifiant attribué à la connexion, spécifiant la révision de la connexion. |

## Obtenir l’URL de collecte de données

Une fois la connexion créée, vous pouvez alors récupérer l’URL de collecte de données.

**Format d’API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | La valeur `id` de la connexion que vous avez créée précédemment. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la connexion demandée. L’URL de collecte de données est automatiquement créée avec la connexion et peut être récupérée à l’aide de la valeur `inletUrl`.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Étapes suivantes

Maintenant que vous avez créé une connexion en continu, vous pouvez diffuser des données de série temporelle ou d’enregistrement, ce qui vous permet d’ingérer des données dans [!DNL Platform]. To learn how to stream time series data to [!DNL Platform], go to the [streaming time series data tutorial](./streaming-time-series-data.md). To learn how to stream record data to [!DNL Platform], go to the [streaming record data tutorial](./streaming-record-data.md).

## Annexe

Cette section fournit des informations supplémentaires sur la création de connexions en continu à l’aide de l’API.

### Connexions en continu authentifiées

Authenticated data collection allows Adobe Experience Platform services, such as [!DNL Real-time Customer Profile] and [!DNL Identity], to differentiate between records coming from trusted sources and untrusted sources. Les clients qui souhaitent envoyer des informations d&#39;identification personnelle (informations d&#39;identification personnelle) peuvent le faire en envoyant des Jetons d&#39;accès IMS dans le cadre de la demande du POST. Si le jeton IMS est valide, les enregistrements sont marqués comme collectés auprès de sources fiables.

Pour plus d’informations sur la création d’une connexion en continu authentifiée, consultez le [tutoriel relatif à la création d’une connexion en continu authentifiée](create-authenticated-streaming-connection.md).
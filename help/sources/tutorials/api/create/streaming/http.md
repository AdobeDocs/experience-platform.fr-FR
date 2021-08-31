---
keywords: Experience Platform;accueil;rubriques les plus consultées;connexion en continu;créer une connexion en continu;guide d’api;tutoriel;créer une connexion en continu;ingestion en continu;ingestion ;
solution: Experience Platform
title: Création d’une connexion en continu à l’aide de l’API
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel vous aidera à commencer à utiliser les API d’ingestion par flux, qui font partie des API d’Adobe Experience Platform Data Ingestion Service.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 0ff93d580482f44954321089659bd2fc062f3f61
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 37%

---


# Création d’une connexion en continu à l’aide de l’API

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables.

Ce tutoriel utilise l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) pour vous guider dans les étapes de création d’une connexion en continu à l’aide de l’API Flow Service.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Cadre normalisé selon lequel  [!DNL Platform] organise les données d’expérience.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

En outre, la création d’une connexion en continu nécessite que vous disposiez d’un schéma XDM cible et d’un jeu de données. Pour savoir comment les créer, consultez le tutoriel sur [données d’enregistrement en continu](../../../../../ingestion/tutorials/streaming-record-data.md) ou le tutoriel sur [données de série temporelle en flux continu](../../../../../ingestion/tutorials/streaming-time-series-data.md).

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API d’ingestion par flux.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d&#39;appels API pour démontrer comment formater vos requêtes. Il s&#39;agit notamment de chemins d&#39;accès, d&#39;en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../../../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Création d’une connexion de base

Une connexion de base spécifie la source et contient les informations requises pour rendre le flux compatible avec les API d’ingestion par flux. Lors de la création d’une connexion de base, vous avez la possibilité de créer une connexion non authentifiée et authentifiée.

### Connexion non authentifiée

Les connexions non authentifiées sont la connexion en continu standard que vous pouvez créer lorsque vous souhaitez diffuser des données dans Platform.

**Format d’API**

```http
POST /flowservice/connections
```

**Requête**

Pour créer une connexion en continu, l’identifiant du fournisseur et l’identifiant de spécification de connexion doivent être fournis dans le cadre de la demande du POST. L’ID de fournisseur est `521eee4d-8cbe-4906-bb48-fb6bd4450033` et l’ID de spécification de connexion est `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
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
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.sourceId` | L’identifiant de la connexion en continu que vous souhaitez créer. |
| `auth.params.dataType` | Type de données de la connexion en continu. Cette valeur doit être `xdm`. |
| `auth.params.name` | Nom de la connexion en continu que vous souhaitez créer. |
| `connectionSpec.id` | La spécification de connexion `id` pour les connexions en continu. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de la nouvelle connexion, y compris son identifiant unique (`id`).

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

### Connexion authentifiée

Les connexions authentifiées doivent être utilisées lorsque vous devez différencier les enregistrements provenant de sources approuvées et non approuvées. Les utilisateurs qui souhaitent envoyer des informations avec des informations d’identification personnelle (PII) doivent créer une connexion authentifiée lors de la diffusion d’informations vers Platform.

**Format d’API**

```http
POST /flowservice/connections
```

**Requête**

Pour créer une connexion en continu, l’identifiant du fournisseur et l’identifiant de spécification de connexion doivent être fournis dans le cadre de la demande du POST. L’ID de fournisseur est `521eee4d-8cbe-4906-bb48-fb6bd4450033` et l’ID de spécification de connexion est `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
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
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Propriété | Description |
| -------- | ----------- |
| `auth.params.sourceId` | L’identifiant de la connexion en continu que vous souhaitez créer. |
| `auth.params.dataType` | Type de données de la connexion en continu. Cette valeur doit être `xdm`. |
| `auth.params.name` | Nom de la connexion en continu que vous souhaitez créer. |
| `auth.params.authenticationRequired` | Le paramètre qui spécifie que la connexion en continu créée |
| `connectionSpec.id` | La spécification de connexion `id` pour les connexions en continu. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de la nouvelle connexion, y compris son identifiant unique (`id`).

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

## Obtention de l’URL du point de terminaison de diffusion

Une fois la connexion de base créée, vous pouvez désormais récupérer l’URL de votre point de terminaison de diffusion en continu.

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

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la connexion demandée. L’URL du point de terminaison de la diffusion en continu est automatiquement créée avec la connexion et peut être récupérée à l’aide de la valeur `inletUrl`.

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

## Création d’une connexion source

Après avoir créé votre connexion de base, vous devez créer une connexion source. Lors de la création d’une connexion source, vous aurez besoin de la valeur `id` de la connexion de base créée.

**Format d’API**

```http
POST /flowservice/sourceConnections
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    }
}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec le détail de la nouvelle connexion source, y compris son identifiant unique (`id`).

```json
{
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
}
```

## Créer une connexion cible

Une connexion cible représente la connexion à la destination où se trouvent les données ingérées. Pour créer une connexion cible, vous devez indiquer l’identifiant de spécification de connexion fixe associé au lac de données. Cet identifiant de spécification de connexion est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma cible d’un jeu de données cible et de l’identifiant de spécification de connexion au lac de données. Grâce à ces identifiants, vous pouvez créer une connexion cible à l’aide de l’API [!DNL Flow Service] pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

```http
POST /flowservice/targetConnections
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de la nouvelle connexion cible, y compris son identifiant unique (`id`).

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## Création d’un flux de données

Une fois vos connexions source et cible créées, vous pouvez désormais créer un flux de données. Le flux de données est chargé de planifier et de collecter les données d’une source. Vous pouvez créer un flux de données en exécutant une requête de POST vers le point de terminaison `/flows`.

**Format d’API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample flow",
    "description": "Sample flow description",
    "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "{SOURCE_CONNECTION_ID}"
    ],
    "targetConnectionIds": [
        "{TARGET_CONNECTION_ID}"
    ]
}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails du nouveau flux de données, y compris son identifiant unique (`id`).

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion HTTP en continu, ce qui vous permet d’utiliser le point de terminaison de diffusion pour ingérer des données dans Platform. Pour obtenir des instructions sur la création d’une connexion en continu dans l’interface utilisateur, consultez le [tutoriel sur la création d’une connexion en continu](../../../ui/create/streaming/http.md).

Pour savoir comment diffuser des données vers Platform, lisez le tutoriel sur [diffusion en continu de données de série temporelle](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou le tutoriel sur [diffusion en continu de données d’enregistrement](../../../../../ingestion/tutorials/streaming-record-data.md).

## Annexe

Cette section fournit des informations supplémentaires sur la création de connexions en continu à l’aide de l’API.

### Envoi de messages à une connexion en continu authentifiée

Si l’authentification est activée pour une connexion en continu, le client doit ajouter l’en-tête `Authorization` à sa requête.

Si l’en-tête `Authorization` n’est pas présent ou si un jeton d’accès non valide/arrivé à expiration est envoyé, une réponse HTTP 401 Non autorisé est renvoyée, avec une réponse similaire à celle-ci :

**Réponse**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```

### Publier les données brutes à ingérer dans Platform {#ingest-data}

Maintenant que vous avez créé votre flux, vous pouvez envoyer votre message JSON au point de terminaison de diffusion que vous avez précédemment créé.

**Format d’API**

```http
POST /collection/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | La valeur `id` de la connexion en continu que vous venez de créer. |

**Requête**

L’exemple de requête ingère des données brutes au point de terminaison de diffusion en continu qui a été créé précédemment.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails des informations nouvellement ingérées.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Propriété | Description |
| -------- | ----------- |
| `{CONNECTION_ID}` | L’identifiant de la connexion en continu précédemment créée. |
| `xactionId` | Un identifiant unique généré côté serveur pour l’enregistrement que vous venez d’envoyer. Cet identifiant aide Adobe à suivre le cycle de vie de cet enregistrement sur différents systèmes et en cas de débogage. |
| `receivedTimeMs` | Un horodatage (en millisecondes) indiquant l’heure de réception de la requête. |

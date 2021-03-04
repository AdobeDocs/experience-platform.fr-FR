---
keywords: Experience Platform ; accueil ; rubriques populaires ; connexion en flux continu ; créer une connexion en flux continu ; guide d’API ; didacticiel ; créer une connexion en flux continu ; assimilation en flux continu ; assimilation ;
solution: Experience Platform
title: Création d’une connexion de diffusion en continu à l’aide de l’API
topic: didacticiel
type: Tutoriel
description: Ce tutoriel vous aidera à commencer à utiliser les API d’ingestion par flux, qui font partie des API d’Adobe Experience Platform Data Ingestion Service.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 42%

---


# Création d’une connexion en continu à l’aide de l’API

Le service de flux permet de collecter et de centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider dans les étapes de création d&#39;une connexion en flux continu à l&#39;aide de l&#39;API de service de flux.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Cadre normalisé selon lequel  [!DNL Platform] organiser les données d’expérience.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de sources multiples.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API d’ingestion par flux.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../../../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Création d’une connexion

Une connexion spécifie la source et contient les informations requises pour rendre le flux compatible avec les API d’ingestion par flux. Lors de la création d’une connexion, vous avez la possibilité de créer une connexion non authentifiée et une connexion authentifiée.

### Connexion non authentifiée

Les connexions non authentifiées sont la connexion de flux continu standard que vous pouvez créer lorsque vous souhaitez diffuser des données dans la plate-forme.

**Format d’API**

```http
POST /flowservice/connections
```

**Requête**

Pour créer une connexion en flux continu, l’ID du fournisseur et l’ID de spécification de connexion doivent être fournis dans le cadre de la demande du POST. L&#39;ID de fournisseur est `521eee4d-8cbe-4906-bb48-fb6bd4450033` et l&#39;ID de spécification de connexion est `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

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
 }
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.sourceId` | ID de la connexion de diffusion en continu que vous souhaitez créer. |
| `auth.params.dataType` | Type de données de la connexion de flux continu. Cette valeur doit être `xdm`. |
| `auth.params.name` | Nom de la connexion de diffusion en continu que vous souhaitez créer. |
| `connectionSpec.id` | Spécification de connexion `id` pour les connexions en flux continu. |

**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 201 avec les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`).

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

Les connexions authentifiées doivent être utilisées lorsque vous devez différencier les enregistrements provenant de sources approuvées et non approuvées. Les utilisateurs qui souhaitent envoyer des informations à l’aide d’informations d’identification personnelle doivent créer une connexion authentifiée lors de la diffusion d’informations sur la plate-forme.

**Format d’API**

```http
POST /flowservice/connections
```

**Requête**

Pour créer une connexion en flux continu, l’ID du fournisseur et l’ID de spécification de connexion doivent être fournis dans le cadre de la demande du POST. L&#39;ID de fournisseur est `521eee4d-8cbe-4906-bb48-fb6bd4450033` et l&#39;ID de spécification de connexion est `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

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
| `auth.params.sourceId` | ID de la connexion de diffusion en continu que vous souhaitez créer. |
| `auth.params.dataType` | Type de données de la connexion de flux continu. Cette valeur doit être `xdm`. |
| `auth.params.name` | Nom de la connexion de diffusion en continu que vous souhaitez créer. |
| `auth.params.authenticationRequired` | Paramètre spécifiant que la connexion de flux continu créée |
| `connectionSpec.id` | Spécification de connexion `id` pour les connexions en flux continu. |

**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 201 avec les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`).

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

## Obtenir l’URL du point de terminaison de flux continu

Une fois la connexion créée, vous pouvez désormais récupérer votre URL de point de terminaison de diffusion en continu.

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

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la connexion demandée. L’URL du point de terminaison de diffusion en continu est automatiquement créée avec la connexion et peut être récupérée à l’aide de la valeur `inletUrl`.

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

En suivant ce didacticiel, vous avez créé une connexion HTTP en flux continu, ce qui vous permet d’utiliser le point de terminaison de flux continu pour assimiler des données dans la plate-forme. Pour obtenir des instructions sur la création d’une connexion en flux continu dans l’interface utilisateur, consultez le [didacticiel sur la création d’une connexion en flux continu](../../../ui/create/streaming/http.md).

Pour savoir comment diffuser les données sur la plateforme, veuillez lire le didacticiel sur [les données de séries chronologiques en flux continu](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou le didacticiel sur [les données d&#39;enregistrement en flux continu](../../../../../ingestion/tutorials/streaming-record-data.md).

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

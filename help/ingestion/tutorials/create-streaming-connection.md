---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’une connexion en flux continu à l’aide de l’API
topic: tutorial
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 2%

---


# Création d’une connexion en flux continu à l’aide de l’API

Ce didacticiel vous aidera à commencer à utiliser les API d’assimilation en flux continu, qui font partie des API Adobe Experience Platform Data Ingestion Service.

## Prise en main

L’enregistrement de la connexion en flux continu est requis pour début des données en flux continu vers Adobe Experience Platform. Lors de l’enregistrement d’une connexion de diffusion en continu, vous devez fournir certains détails clés, tels que la source des données de diffusion en continu.

Après l’enregistrement d’une connexion de diffusion en continu, vous, en tant que producteur de données, disposez d’une URL unique qui peut être utilisée pour diffuser des données vers la plate-forme.

Ce didacticiel nécessite également une connaissance pratique de divers services Adobe Experience Platform. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la Plateforme organise les données d&#39;expérience.
- [Profil](../../profile/home.md)client en temps réel : Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de plusieurs sources.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API d’assimilation en flux continu.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Création d’une connexion

Une connexion spécifie la source et contient les informations requises pour rendre le flux compatible avec les API de diffusion en continu.

**Format d’API**

```http
POST /flowservice/connections
```

**Requête**

>[!NOTE] Les valeurs des éléments répertoriés `providerId` et des éléments `connectionSpec` doivent **** être utilisées comme indiqué dans l’exemple, car il s’agit de ce qui indique à l’API que vous créez une connexion de diffusion en continu pour l’assimilation en flux continu.

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

Une réponse réussie renvoie l’état HTTP 201 avec les détails de la connexion nouvellement créée.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Le nom `id` de votre nouvelle connexion. On parle ici de `{CONNECTION_ID}`. |
| `etag` | Identificateur attribué à la connexion, spécifiant la révision de la connexion. |

## Obtenir l&#39;URL de collecte de données

Une fois la connexion créée, vous pouvez désormais récupérer l’URL de collecte de données.

**Format d’API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de la connexion que vous avez créée précédemment. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 200 avec des informations détaillées sur la connexion demandée. L’URL de collecte de données est automatiquement créée avec la connexion et peut être récupérée à l’aide de la `inletUrl` valeur.

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

Maintenant que vous avez créé une connexion de diffusion en continu, vous pouvez diffuser des séries chronologiques ou enregistrer des données, ce qui vous permet d’assimiler des données dans la plate-forme. Pour savoir comment diffuser des données de série chronologique sur la plateforme, consultez le didacticiel [sur les données de série chronologique](./streaming-time-series-data.md)en flux continu. Pour savoir comment diffuser les données d’enregistrement sur la plate-forme, consultez le didacticiel [sur les données d’enregistrement](./streaming-record-data.md)en flux continu.

## Annexe

Cette section fournit des informations supplémentaires sur la création de connexions en flux continu à l’aide de l’API.

### Connexions de flux continu authentifiées

La collecte de données authentifiées permet aux services Adobe Experience Platform, tels que le Profil et l’identité des clients en temps réel, de différencier les enregistrements provenant de sources approuvées des enregistrements provenant de sources non approuvées. Les clients qui souhaitent envoyer des informations d&#39;identification personnelle (informations d&#39;identification personnelle) peuvent le faire en envoyant des Jetons d&#39;accès IMS dans le cadre de la demande POST. Si le jeton IMS est valide, les enregistrements sont marqués comme collectés auprès de sources fiables.

Pour plus d’informations sur la création d’une connexion de flux continu authentifiée, consultez le didacticiel [](create-authenticated-streaming-connection.md)Création d’une connexion de flux continu authentifiée.
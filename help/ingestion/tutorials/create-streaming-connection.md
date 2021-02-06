---
keywords: Experience Platform ; accueil ; rubriques populaires ; connexion en flux continu ; créer une connexion en flux continu ; guide d’API ; didacticiel ; créer une connexion en flux continu ; assimilation en flux continu ; assimilation ;
solution: Experience Platform
title: Création d’une connexion de diffusion en continu à l’aide de l’API
topic: tutorial
type: Tutorial
description: Ce tutoriel vous aidera à commencer à utiliser les API d’ingestion par flux, qui font partie des API d’Adobe Experience Platform Data Ingestion Service.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 72%

---


# Création d’une connexion en continu à l’aide de l’API

Ce didacticiel vous aidera à commencer à utiliser les API d’assimilation en flux continu, qui font partie des API de données Adobe Experience Platform [!DNL Ingestion Service].

## Prise en main

L’enregistrement d’une connexion en continu est requis pour commencer la diffusion des données en continu vers Adobe Experience Platform. Lors de l’enregistrement d’une connexion en continu, vous devez fournir des détails clés, tels que la source des données en continu.

Après avoir enregistré une connexion en continu, vous obtiendrez, en tant que producteur des données, une URL unique que vous pourrez utiliser pour diffuser en continu des données vers Platform.

Ce tutoriel nécessite également une connaissance pratique de divers services Adobe Experience Platform. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel  [!DNL Platform] organiser les données d’expérience.
- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API d’ingestion par flux.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

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

Maintenant que vous avez créé une connexion en continu, vous pouvez diffuser des données de série temporelle ou d’enregistrement, ce qui vous permet d’ingérer des données dans [!DNL Platform]. Pour savoir comment diffuser des données de série chronologique vers [!DNL Platform], consultez le [didacticiel de données de série chronologique en flux continu](./streaming-time-series-data.md). Pour savoir comment diffuser les données d&#39;enregistrement dans [!DNL Platform], consultez le [didacticiel de données d&#39;enregistrement en flux continu](./streaming-record-data.md).

## Annexe

Cette section fournit des informations supplémentaires sur la création de connexions en continu à l’aide de l’API.

### Connexions en continu authentifiées

La collecte de données authentifiées permet aux services Adobe Experience Platform, tels que [!DNL Real-time Customer Profile] et [!DNL Identity], de faire la distinction entre les enregistrements provenant de sources approuvées et les sources non approuvées. Les clients qui souhaitent envoyer des informations d&#39;identification personnelle (informations d&#39;identification personnelle) peuvent le faire en envoyant des Jetons d&#39;accès IMS dans le cadre de la demande du POST. Si le jeton IMS est valide, les enregistrements sont marqués comme collectés auprès de sources fiables.

Pour plus d’informations sur la création d’une connexion en continu authentifiée, consultez le [tutoriel relatif à la création d’une connexion en continu authentifiée](create-authenticated-streaming-connection.md).
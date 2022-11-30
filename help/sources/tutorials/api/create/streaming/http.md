---
keywords: Experience Platform;accueil;rubriques les plus consultées;connexion en continu;créer une connexion en continu;guide d’api;tutoriel;créer une connexion en continu;ingestion en continu;ingestion ;
title: Création d’une connexion en continu d’API HTTP à l’aide de l’API Flow Service
description: Ce tutoriel explique comment créer une connexion en continu à l’aide de la source d’API HTTP pour les données brutes et XDM à l’aide de l’API Flow Service.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 26c967418e983322cc39aa799a681d258638d769
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 42%

---


# Créez une connexion en continu à l’API HTTP à l’aide de la fonction [!DNL Flow Service] API

Le service de flux permet de collecter et de centraliser les données client à partir de différentes sources dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables.

Ce tutoriel utilise la méthode [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) pour vous guider dans les étapes de création d’une connexion en continu à l’aide de la fonction [!DNL Flow Service] API.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Le cadre normalisé selon lequel [!DNL Platform] organise les données d’expérience.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

En outre, la création d’une connexion en continu nécessite que vous disposiez d’un schéma XDM cible et d’un jeu de données. Pour savoir comment les créer, consultez le tutoriel sur [données d’enregistrement en continu](../../../../../ingestion/tutorials/streaming-record-data.md) ou du tutoriel sur [diffusion en continu de données de série temporelle](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base spécifie la source et contient les informations requises pour rendre le flux compatible avec les API d’ingestion par flux. Lors de la création d’une connexion de base, vous avez la possibilité de créer une connexion non authentifiée et authentifiée.

### Connexion non authentifiée

Les connexions non authentifiées sont la connexion en continu standard que vous pouvez créer lorsque vous souhaitez diffuser des données dans Platform.

Pour créer une connexion de base non authentifiée, envoyez une requête de POST au `/connections` point de terminaison tout en fournissant un nom pour votre connexion, le type de données et l’identifiant de spécification de connexion de l’API HTTP. Cet identifiant est `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**Format d’API**

```http
POST /flowservice/connections
```

**Requête**

La requête suivante crée une connexion de base pour l’API HTTP.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB Données brutes]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion de base. Assurez-vous que le nom est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion de base. |
| `description` | (Facultatif) Propriété que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `connectionSpec.id` | Identifiant de spécification de connexion qui correspond à l’API HTTP. Cet identifiant est `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | Type de données de la connexion en continu. Les valeurs prises en charge sont les suivantes : `xdm` et `raw`. |
| `auth.params.name` | Nom de la connexion en continu que vous souhaitez créer. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de la nouvelle connexion, y compris son identifiant unique (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Le `id` de la connexion de base que vous venez de créer. |
| `etag` | Identifiant attribué à la connexion, spécifiant la version de la connexion de base. |

### Connexion authentifiée

Les connexions authentifiées doivent être utilisées lorsque vous devez différencier les enregistrements provenant de sources approuvées et non approuvées. Les utilisateurs qui souhaitent envoyer des informations avec des informations d’identification personnelle (PII) doivent créer une connexion authentifiée lors de la diffusion d’informations vers Platform.

Pour créer une connexion de base authentifiée, vous devez indiquer votre ID source et indiquer si l’authentification est requise lors de l’exécution d’une requête de POST à la variable `/connections` point de terminaison .


**Format d’API**

```http
POST /flowservice/connections
```

**Requête**

La requête suivante crée une connexion de base authentifiée pour l’API HTTP.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "{SOURCE_ID}",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB Données brutes]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "raw",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| Propriété | Description |
| -------- | ----------- |
| `auth.params.sourceId` | L’identifiant de la connexion en continu que vous souhaitez créer. |
| `auth.params.authenticationRequired` | Le paramètre qui spécifie que la connexion en continu créée |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de la nouvelle connexion, y compris son identifiant unique (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## Obtention de l’URL du point de terminaison de diffusion

Une fois la connexion de base créée, vous pouvez désormais récupérer l’URL de votre point de terminaison de diffusion en continu.

**Format d’API**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | La valeur `id` de la connexion que vous avez créée précédemment. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la connexion demandée. L’URL du point de terminaison de diffusion en continu est automatiquement créée avec la connexion et peut être récupérée à l’aide de la fonction `inletUrl` .

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## Créer une connexion source {#source}

Pour créer une connexion source, envoyez une requête de POST au `/sourceConnections` point de terminaison tout en fournissant votre identifiant de connexion de base.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
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
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Créer un schéma XDM cible {#target-schema}

Pour que les données sources soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Le schéma cible est ensuite utilisé pour créer un jeu de données Platform contenant les données sources.

Un schéma XDM cible peut être créé en adressant une requête POST à l’[API Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, suivez le tutoriel sur la [création d’un schéma à l’aide de l’API](../../../../../xdm/api/schemas.md).

### Créer un jeu de données cible {#target-dataset}

Un jeu de données cible peut être créé en adressant une requête POST à l’[API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) et en fournissant l’identifiant du schéma cible dans la payload.

Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, suivez le tutoriel sur la [création d’un jeu de données à l’aide de l’API](../../../../../catalog/api/create-dataset.md).

## Créer une connexion cible {#target}

Une connexion cible représente la connexion à la destination où se trouvent les données ingérées. Pour créer une connexion cible, envoyez une requête de POST à `/targetConnections` tout en fournissant des identifiants pour votre jeu de données cible et votre schéma XDM cible. Au cours de cette étape, vous devez également fournir l’identifiant de spécification de connexion au lac de données. Cet identifiant est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de la nouvelle connexion cible, y compris son identifiant unique (`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Créer un mappage {#mapping}

Pour que les données sources soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible se rattache.

Pour créer un jeu de mappage, envoyez une requête POST au point dʼentrée `mappingSets` de lʼ[[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) et indiquez votre schéma XDM cible `$id` et les détails des jeux de mappages que vous souhaitez créer.

**Format d’API**

```http
POST /mappingSets
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `xdmSchema` | La valeur `$id` du schéma XDM cible. |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

```json
{
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

| Propriété | Description |
| --- | --- |

## Créer un flux de données

Une fois vos connexions source et cible créées, vous pouvez désormais créer un flux de données. Le flux de données est chargé de planifier et de collecter les données d’une source. Vous pouvez créer un flux de données en adressant une requête de POST au `/flows` point de terminaison .

**Format d’API**

```http
POST /flows
```

**Requête**

>[!BEGINTABS]

>[!TAB Sans transformations]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB Avec transformations]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| Propriété | Description |
| --- | --- |
| `name` | Nom du flux de données. Assurez-vous que le nom de votre flux de données est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre flux de données. |
| `description` | (Facultatif) Propriété que vous pouvez inclure pour fournir plus d’informations sur votre flux de données. |
| `flowSpec.id` | L’identifiant de spécification de flux pour [!DNL HTTP API]. Pour créer un flux de données avec des transformations, vous devez utiliser  `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. Pour créer un flux de données sans conversion, utilisez `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | [Identifiant de connexion source](#source) récupéré lors d’une étape précédente. |
| `targetConnectionIds` | [Identifiant de connexion cible](#target) récupéré lors d’une étape précédente. |
| `transformations.params.mappingId` | [Identifiant de mappage](#mapping) récupéré lors d’une étape précédente. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails du nouveau flux de données, y compris son identifiant unique (`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```


## Données de publication à ingérer dans Platform {#ingest-data}

Maintenant que vous avez créé votre flux, vous pouvez envoyer votre message JSON au point de terminaison de diffusion que vous avez précédemment créé.

**Format d’API**

```http
POST /collection/{INLET_URL}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INLET_URL}` | Votre URL de point de terminaison de diffusion en continu. Vous pouvez récupérer cette URL en effectuant une requête de GET à la variable `/connections` point de terminaison tout en fournissant votre identifiant de connexion de base. |

**Requête**

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB Données brutes]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
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

>[!ENDTABS]

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails des informations nouvellement ingérées.

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Propriété | Description |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | L’identifiant de la connexion en continu précédemment créée. |
| `xactionId` | Un identifiant unique généré côté serveur pour l’enregistrement que vous venez d’envoyer. Cet identifiant aide Adobe à suivre le cycle de vie de cet enregistrement sur différents systèmes et en cas de débogage. |
| `receivedTimeMs` | Un horodatage (en millisecondes) indiquant l’heure de réception de la requête. |


## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion HTTP en continu, ce qui vous permet d’utiliser le point de terminaison de diffusion pour ingérer des données dans Platform. Pour obtenir des instructions sur la création d’une connexion en continu dans l’interface utilisateur, veuillez lire le [tutoriel sur la création d’une connexion en continu](../../../ui/create/streaming/http.md).

Pour savoir comment diffuser des données vers Platform, veuillez lire le tutoriel sur [diffusion en continu de données de série temporelle](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou du tutoriel sur [données d’enregistrement en continu](../../../../../ingestion/tutorials/streaming-record-data.md).

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

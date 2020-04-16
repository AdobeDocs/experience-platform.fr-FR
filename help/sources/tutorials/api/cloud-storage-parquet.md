---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Invitation de données de parquet à partir d’un système de  de cloud tiers système  à l’aide de l’API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 0e993e3b0ad4ff58a67e7db742f97c5fb2c3308d

---


# Invitation de données de parquet à partir d’un système de  de cloud tiers système  à l’aide de l’API Flow Service

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API du service de flux pour vous guider tout au long des étapes d’assimilation des données de parquet d’un système de Cloud  tiers.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Sources](../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
- [Sandbox](../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir assimiler correctement les données de parquet d’un de cloud tiers  à l’aide de l’API de service de flux.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

- Content-Type : `application/json`

## Création d’une connexion

Afin d’assimiler des données de parquet à l’aide des API Platform, vous devez posséder une connexion valide pour le cloud tiers  la source  à laquelle vous accédez. Si vous ne disposez pas encore d’une connexion pour le   avec lequel vous souhaitez travailler, vous pouvez en créer une à l’aide des didacticiels suivants :

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure Data Lake   Gen2](./create/cloud-storage/adls-gen2.md)
- [Google Cloud Store](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

Récupérez et stockez l’identifiant unique (`$id`) de la connexion, puis passez à l’étape suivante de ce didacticiel.

## Création d’un  

Pour que les données source soient utilisées dans Platform, un de  doit également être créé pour structurer les données source en fonction de vos besoins. Le  est ensuite utilisé pour créer un jeu de données de plateforme dans lequel les données source sont contenues.

Si vous préférez utiliser l’interface utilisateur dans la plateforme d’expérience, le didacticiel [de l’éditeur de ](../../../xdm/tutorials/create-schema-ui.md) fournit des instructions étape par étape pour exécuter des actions similaires dans l’éditeur de  de.

**Format API**

```http
POST /schemaregistry/tenant/schemas
```

**Requête**

L’exemple de requête suivant crée un  XDM qui étend la classe de XDM Individuel.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle  de, y compris son identifiant unique (`$id`). Cet ID est requis à l’étape suivante pour créer une connexion source.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’une connexion source {#source}

Une fois un XDM  créé, une connexion source peut désormais être créée à l’aide d’une requête POST sur l’API du service de flux. Une connexion source consiste en une connexion pour l’API, un format de données source et une référence au XDM  récupéré à l’étape précédente.

**Format API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | La connexion de l’API qui représente votre cloud  . |
| `data.schema.id` | Le (`$id`) si le  xdm  récupéré à l’étape précédente. |
| `params.path` | Chemin d’accès du fichier source. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source nouvellement créée. Stockez cette valeur comme elle est requise dans les étapes suivantes pour créer une connexion .

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## Création d’une connexion de base de jeux de données

Pour importer des données externes dans la plateforme, une connexion de base de données de jeu de plateformes d’expérience doit d’abord être acquise.

Pour créer une connexion de base de jeux de données, suivez les étapes décrites dans le didacticiel [sur la connexion de base de jeux de](./create-dataset-base-connection.md)données.

Continuez à suivre les étapes décrites dans le guide du développeur jusqu’à ce que vous ayez créé une connexion de base de jeux de données. Récupérez et stockez l’identifiant unique (`$id`) et utilisez-le comme identifiant de connexion de base à l’étape suivante pour créer une connexion .

## Création d’un jeu de données de 

Vous pouvez créer un jeu de données  en exécutant une requête POST sur l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog Service, en indiquant l’ID du  de  dans la charge utile.

**Format API**

```http
POST /catalog/dataSets
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "fileDescription": {
            "format": "parquet"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `schemaRef.id` | ID de votre  XDM . |

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;ID du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’ID du jeu de données est une chaîne générée par le système en lecture seule qui est utilisée pour référencer le jeu de données dans les appels d’API. Stockez l’ID du jeu de données  du, comme requis dans les étapes suivantes pour créer une connexion  et un flux de données.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## Création d’une connexion {#target}

Vous disposez maintenant des identifiants uniques pour une connexion de base de jeux de données, un  et un jeu de données de  dedonnées. A l’aide de ces identifiants, vous pouvez créer une connexion  à l’aide de l’API du service de flux afin de spécifier le jeu de données qui contiendra les données source entrantes.

**Format API**

```http
POST /targetConnections
```

**Requête**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | ID de votre connexion de base de jeux de données. |
| `data.schema.id` | Le `$id` du XDM . |
| `params.dataSetId` | ID du jeu de données . |
| `connectionSpec.id` | Identifiant de spécification de connexion pour votre  Cloud . |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion . Stockez cette valeur comme elle est requise dans les étapes ultérieures.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## Création d’un flux de données

La dernière étape pour ingérer des données de parquet à partir d&#39;un de cloud tiers  est de créer un flux de données. Les valeurs requises suivantes sont désormais préparées :

- [ID de connexion source](#source)
- [ID de connexion](#target)

Un flux de données est responsable de la planification et de la collecte de données à partir d’une source. Vous pouvez créer un flux de données en exécutant une requête POST tout en fournissant les valeurs mentionnées précédemment dans la charge utile.

**Format API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `sourceConnectionIds` | ID de connexion source récupéré lors d’une étape précédente. |
| `targetConnectionIds` | L’ID de connexion  du a été récupéré lors d’une étape précédente. |

**Réponse**

Une réponse réussie renvoie l’ID (`id`) du flux de données nouvellement créé.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur source pour collecter les données sur le parquet de votre système de  de nuages tiers sur une base planifiée. Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que les  de clients en temps réel et l’espace de travail des sciences de données. Pour plus d’informations, reportez-vous au  suivant :

- [Présentation du profil client en temps réel](../../../profile/home.md)
- [Présentation de l’espace de travail Data Science](../../../data-science-workspace/home.md)
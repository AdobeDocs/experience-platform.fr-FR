---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion par lots;ingestion par lots;ingestion;guide de développement;guide d’api;charger;ingérer le paramètre;ingérer le fichier json ;
solution: Experience Platform
title: Guide de l’API Batch Ingestion
description: Ce document fournit un guide complet aux développeurs qui utilisent les API d’ingestion par lots pour Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 087a714c579c4c3b95feac3d587ed13589b6a752
workflow-type: tm+mt
source-wordcount: '2373'
ht-degree: 77%

---

# Guide de développement de l’ingestion par lots

Ce document fournit un guide complet sur l’utilisation des [points de terminaison de l’API d’ingestion par lots](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion) dans Adobe Experience Platform. Pour une présentation des API d’ingestion par lots, y compris les conditions préalables et les bonnes pratiques, veuillez commencer par lire la [présentation de l’API d’ingestion par lots](overview.md).

L’annexe de ce document fournit des informations sur le [formatage des données à utiliser pour l’ingestion](#data-transformation-for-batch-ingestion), y compris des exemples de fichiers de données CSV et JSON.

## Prise en main

Les points de terminaison d’API utilisés dans ce guide font partie de l’[API Data Ingestion](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). L’ingestion de données fournit une API RESTful grâce à laquelle vous pouvez effectuer des opérations CRUD sur les types d’objets pris en charge.

Avant de poursuivre, consultez la [présentation de l’API d’ingestion par lots](overview.md) et le [guide de prise en main](getting-started.md).

## Ingestion de fichiers JSON

>[!NOTE]
>
>Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devez passer au chargement de fichiers volumineux.

### Création d’un lot

Vous devrez tout d’abord créer un lot au format JSON en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni.

>[!NOTE]
>
>Les exemples ci-dessous concernent le format JSON à une seule ligne. Pour ingérer un format JSON à plusieurs lignes, l’indicateur `isMultiLineJson` doit être défini. Pour plus d’informations, reportez-vous au [guide de dépannage de l’ingestion par lots](./troubleshooting.md).

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |

### Chargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser l’identifiant de lot de la réponse de création de lot pour charger les fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

>[!NOTE]
>
>Reportez-vous à l’annexe pour y trouver un [exemple de fichier de données JSON correctement formaté](#data-transformation-for-batch-ingestion).

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d’accès au fichier est l’emplacement où le fichier sera enregistré côté Adobe. |

**Requête**

>[!NOTE]
>
>L’API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier est le chemin d’accès au fichier local, tel que `Users/sample-user/Downloads/sample.json`. |

**Réponse**

```http
200 OK
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les différentes parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```http
200 OK
```

## Ingestion de fichiers Parquet {#ingest-parquet-files}

>[!NOTE]
>
>Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devrez passer au chargement de fichiers volumineux.

### Création d’un lot

Vous devrez tout d’abord créer un lot, avec Parquet en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni.

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| Paramètre | Description |
| --------- | ------------ |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{USER_ID}` | L’identifiant de l’utilisateur qui a créé le lot. |

### Chargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d’accès au fichier est l’emplacement où le fichier sera enregistré côté Adobe. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier est le chemin d’accès au fichier local, tel que `Users/sample-user/Downloads/sample.json`. |

**Réponse**

```http
200 OK
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les différentes parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez signaler comme prêt pour être terminé. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Ingestion de fichiers Parquet volumineux

>[!NOTE]
>
>Cette section explique comment charger des fichiers d’une taille supérieure à 256 Mo. Les fichiers volumineux sont chargés en blocs, puis assemblés au moyen d’un signal API.

### Création d’un lot

Vous devrez tout d’abord créer un lot, avec Parquet en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni.

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{USER_ID}` | L’identifiant de l’utilisateur qui a créé le lot. |

### Initialisation d’un fichier volumineux

Après la création du lot, vous devrez initialiser le fichier volumineux avant de charger les blocs dans le lot.

**Format d’API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{FILE_NAME}` | Le nom du fichier sur le point d’être initialisé. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
201 Created
```

### Chargement des blocs d’un fichier volumineux

Une fois le fichier créé, tous les blocs suivants peuvent être chargés en exécutant des requêtes PATCH répétées, une pour chaque section du fichier.

**Format d’API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d’accès au fichier est l’emplacement où le fichier sera enregistré côté Adobe. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONTENT_RANGE}` | En entiers, le début et la fin de la plage demandée. |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier est le chemin d’accès au fichier local, tel que `Users/sample-user/Downloads/sample.json`. |


**Réponse**

```http
200 OK
```

### Terminer le fichier volumineux

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

**Format d’API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez signaler comme étant terminé. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez signaler comme étant terminé. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
201 Created
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les différentes parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez signaler comme étant terminé. |


**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Ingestion de fichiers CSV

Pour ingérer des fichiers CSV, vous devrez créer une classe, un schéma et un jeu de données qui prend en charge le format CSV. Pour obtenir des informations détaillées sur la création de la classe et du schéma nécessaires, suivez les instructions fournies dans le [tutoriel de création de schémas ad hoc](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devrez passer au chargement de fichiers volumineux.

### Création d’un jeu de données

Après avoir suivi les instructions ci-dessus pour créer la classe et le schéma nécessaires, vous devrez créer un jeu de données capable de prendre en charge le format CSV.

**Format d’API**

```http
POST /catalog/dataSets
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| Paramètre | Description |
| --------- | ----------- |
| `{TENANT_ID}` | Cet identifiant est utilisé pour assurer que les espaces de noms des ressources que vous créez sont corrects et contenus dans votre organisation IMS. |
| `{SCHEMA_ID}` | L’identifiant du schéma que vous avez créé. |

### Création d’un lot

Vous devrez ensuite créer un lot au format d’entrée CSV. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma lié au jeu de données fourni.

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{USER_ID}` | L’identifiant de l’utilisateur qui a créé le lot. |

### Chargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

>[!NOTE]
>
>Reportez-vous à l’annexe pour y trouver un [exemple de fichier de données CSV correctement formaté](#data-transformation-for-batch-ingestion).

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d’accès au fichier est l’emplacement où le fichier sera enregistré côté Adobe. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier est le chemin d’accès au fichier local, tel que `Users/sample-user/Downloads/sample.json`. |


**Réponse**

```http
200 OK
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```http
200 OK
```

## Annulation d’un lot

Il est toujours possible d’annuler un lot pendant son traitement. Une fois qu’un lot est finalisé (et que son état passe par exemple à « réussi » ou « échec »), il est impossible de l’annuler.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez annuler. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Suppression d’un lot {#delete-a-batch}

Vous pouvez supprimer un lot en exécutant la requête POST suivante avec le paramètre de requête `action=REVERT` vers l’identifiant du lot que vous souhaitez supprimer. Le lot est marqué comme « inactif », ce qui le rend éligible pour le nettoyage de la mémoire. Le lot sera collecté de manière asynchrone : il sera alors marqué comme « supprimé ».

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez supprimer. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Correction d’un lot

Il peut parfois être nécessaire de mettre à jour les données dans la banque de profils de votre entreprise. Par exemple, vous devrez peut-être corriger des enregistrements ou modifier une valeur d’attribut. Adobe Experience Platform prend en charge la mise à jour ou le correctif des données de la banque de profils par le biais d’une action d’insertion ou de &quot;correction d’un lot&quot;.

>[!NOTE]
>
>Ces mises à jour ne sont autorisées que sur les enregistrements de profil, et non sur les événements d’expérience.

Les éléments suivants sont requis pour corriger un lot :

- **Jeu de données activé pour les mises à jour de profil et d’attribut.** Pour ce faire, vous devez utiliser des balises de jeu de données et ajouter une  `isUpsert:true` balise spécifique au  `unifiedProfile` tableau . Pour obtenir des détails sur la procédure de création d’un jeu de données ou de configuration d’un jeu de données existant à des fins de publication, suivez le tutoriel portant sur l’[activation d’un jeu de données pour les mises à jour de profil](../../catalog/datasets/enable-upsert.md).
- **Fichier parquet contenant les champs à corriger et les champs d’identité du profil.** Le format de données utilisé pour corriger un lot est similaire au processus normal d’ingestion par lots. L’entrée requise est un fichier Parquet. En plus des champs à mettre à jour, les données chargées doivent contenir les champs d’identité afin de correspondre aux données de la banque de profils.

Une fois qu’un jeu de données est activé pour Profile et upsert, et qu’un fichier Parquet contient les champs que vous souhaitez corriger ainsi que les champs d’identité nécessaires, vous pouvez suivre les étapes d’[ingestion de fichiers Parquet](#ingest-parquet-files) afin de terminer le correctif par ingestion par lots.

## Relecture d’un lot

Si vous souhaitez remplacer un lot déjà ingéré, vous pouvez le faire grâce à la fonctionnalité « relecture de lot ». Cette action équivaut à supprimer l’ancien lot et à en ingérer un nouveau pour le remplacer.

### Création d’un lot

Vous devrez tout d’abord créer un lot au format JSON en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni. Vous devrez également fournir le ou les anciens lots comme référence dans la section de relecture. Dans l’exemple ci-dessous, vous effectuez la relecture de lots aux identifiants `batchIdA` et `batchIdB`.

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| Paramètre | Description |
| --------- | ----------- | 
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{USER_ID}` | L’identifiant de l’utilisateur qui a créé le lot. |


### Chargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d’accès au fichier est l’emplacement où le fichier sera enregistré côté Adobe. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream. Évitez d’employer l’option curl -F, car elle utilise par défaut une requête à parties multiples incompatible avec l’API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier est le chemin d’accès au fichier local, tel que `Users/sample-user/Downloads/sample.json`. |

**Réponse**

```http
200 OK
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les différentes parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez terminer. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```http
200 OK
```

## Annexe

La section suivante contient des informations supplémentaires sur l’ingestion de données dans Experience Platform à l’aide de l’ingestion par lots.

### Transformation des données pour l’ingestion par lots

Pour ingérer un fichier de données dans [!DNL Experience Platform], la structure hiérarchique du fichier doit être conforme au schéma [Modèle de données d’expérience (XDM)](../../xdm/home.md) associé au jeu de données dans lequel il est chargé.

Vous trouverez des informations sur le mappage d’un fichier CSV pour être conforme à un schéma XDM dans le document traitant des [exemples de transformations](../../etl/transformations.md), ainsi qu’un exemple de fichier de données JSON correctement formaté. Les exemples de fichiers fournis dans ce document se trouvent ici :

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)

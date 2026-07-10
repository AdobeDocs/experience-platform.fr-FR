---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion par lots;ingestion par lots;ingestion;guide de développement;guide d’api;chargement;ingérer Parquet;ingérer json;
solution: Experience Platform
title: Guide de l’API d’ingestion par lots
description: Ce document fournit un guide complet aux développeurs qui travaillent avec des API d’ingestion par lots pour Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
TQID: https://experienceleague.adobe.com/oCAUvP0cM4dw1wEXnVCbjIkNGIlwSKb31A5h5s3-MTM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: cb424651efb1b4d71717c06a4b0d6e9354f0dcc7
workflow-type: tm+mt
source-wordcount: 2532
ht-degree: 62%

---

# Guide de développement de l’ingestion par lots

Ce document fournit un guide complet sur l’utilisation des points d’entrée [API d’ingestion par lots](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion) dans Adobe Experience Platform. Pour obtenir un aperçu des API d’ingestion par lots, y compris les conditions préalables et les bonnes pratiques, commencez par lire la [&#x200B; présentation de l’API d’ingestion par lots &#x200B;](overview.md).

L’annexe de ce document fournit des informations sur le [formatage des données à utiliser pour l’ingestion](#data-transformation-for-batch-ingestion), y compris des exemples de fichiers de données CSV et JSON.

## Prise en main

Les points d’entrée d’API utilisés dans ce guide font partie de l’[API Batch Ingestion](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion). L’ingestion par lots est fournie par le biais d’une API RESTful où vous pouvez effectuer des opérations CRUD de base sur les types d’objets pris en charge.

Avant de poursuivre, consultez la présentation de l’API d’ingestion par lots [batch ingestion](overview.md) et le [&#x200B; guide de prise en main](getting-started.md).

## Ingestion de fichiers JSON

>[!NOTE]
>
>- Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devez passer au chargement de fichiers volumineux.
>
>- Utilisez des objets JSON à une seule ligne (JSONL) au lieu du JSON multiligne comme entrée pour l’ingestion par lots. Les objets JSON à une seule ligne (JSONL) offrent de meilleures performances, car le système peut diviser un fichier d’entrée en plusieurs blocs et les traiter en parallèle, tandis que le format JSON multiligne ne peut pas être divisé. Cela peut réduire considérablement les coûts de traitement des données et améliorer la latence du traitement par lots.

### Création d’un lot

Vous devrez tout d’abord créer un lot au format JSON en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni.

>[!NOTE]
>
>Les exemples ci-dessous concernent le format JSON à une seule ligne (JSONL). Pour ingérer un format JSON à plusieurs lignes, l’indicateur `isMultiLineJson` doit être défini. Pour plus d’informations, reportez-vous au [guide de dépannage de l’ingestion par lots](./troubleshooting.md).

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
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
    "imsOrg": "{ORG_ID}",
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

Maintenant que vous avez créé un lot, vous pouvez utiliser l’ID de lot de la réponse de création de lot pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

>[!NOTE]
>
>Voir la section annexe pour un [exemple de fichier de données JSON correctement formaté](#data-transformation-for-batch-ingestion).

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Nom du fichier à charger. Veillez à utiliser un nom de fichier unique afin qu’il n’entre pas en conflit avec un autre fichier pour le lot de fichiers envoyé. |

**Requête**

>[!NOTE]
>
>L’API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Chemin d’accès complet et nom du fichier que vous essayez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `acme/customers/campaigns/summer.json`. |

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```http
200 OK
```

## Ingestion de fichiers Parquet {#ingest-parquet-files}

>[!NOTE]
>
>Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devrez passer au chargement de fichiers volumineux.

### Création d’un lot

Vous devrez tout d’abord créer un lot, avec Parquet en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni.

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
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
    "imsOrg": "{ORG_ID}",
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
| `{FILE_NAME}` | Nom du fichier à charger. Veillez à utiliser un nom de fichier unique afin qu’il n’entre pas en conflit avec un autre fichier pour le lot de fichiers envoyé. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Chemin d’accès complet et nom du fichier que vous essayez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `acme/customers/campaigns/summer.parquet`. |

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Ingestion de fichiers Parquet volumineux

>[!NOTE]
>
>Cette section explique comment télécharger des fichiers dont la taille est supérieure à 256 Mo. Les fichiers volumineux sont chargés en blocs, puis assemblés au moyen d’un signal API.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
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
    "imsOrg": "{ORG_ID}",
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{FILE_NAME}` | Nom du fichier à charger. Veillez à utiliser un nom de fichier unique afin qu’il n’entre pas en conflit avec un autre fichier pour le lot de fichiers envoyé. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONTENT_RANGE}` | En entiers, le début et la fin de la plage demandée. |
| `{FILE_PATH_AND_NAME}` | Chemin d’accès complet et nom du fichier que vous essayez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `acme/customers/campaigns/summer.json`. |


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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
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
>Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devrez passer au chargement de fichiers volumineux.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{TENANT_ID}` | Cet identifiant permet de s’assurer que les ressources que vous créez ont un espace de noms correct et sont contenues dans votre organisation. |
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
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
    "imsOrg": "{ORG_ID}",
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
>Voir la section annexe pour un [exemple de fichier de données CSV correctement formaté](#data-transformation-for-batch-ingestion).

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Nom du fichier à charger. Veillez à utiliser un nom de fichier unique afin qu’il n’entre pas en conflit avec un autre fichier pour le lot de fichiers envoyé. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Chemin d’accès complet et nom du fichier que vous essayez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `acme/customers/campaigns/summer.csv`. |


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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Suppression d’un lot {#delete-a-batch}

Vous pouvez supprimer un lot en exécutant la requête POST suivante avec le paramètre de requête `action=REVERT` vers l’identifiant du lot que vous souhaitez supprimer. Le lot est marqué comme « inactif », ce qui le rend éligible pour la récupération de l’espace mémoire. Le lot sera collecté de manière asynchrone : il sera alors marqué comme « supprimé ».

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Application d’un correctif à un lot

Il peut parfois être nécessaire de mettre à jour les données du magasin de profils de votre entreprise. Vous pouvez par exemple avoir besoin de corriger des enregistrements ou de modifier une valeur d’attribut. Adobe Experience Platform prend en charge la mise à jour ou l’application de correctifs aux données de la banque de profils par le biais d’une action upsert ou d’un « correctif par lot ».

>[!NOTE]
>
>Ces mises à jour sont autorisées uniquement sur les enregistrements de profil, et non sur les événements d’expérience.

Les éléments suivants sont requis pour appliquer un correctif à un lot :

- **Jeu de données activé pour les mises à jour de profil et d’attribut.** Cette opération s’effectue par le biais de balises de jeu de données et nécessite l’ajout d’une balise `isUpsert:true` spécifique au tableau de `unifiedProfile`. Pour obtenir des instructions détaillées sur la création d’un jeu de données ou la configuration d’un jeu de données existant à mettre à jour, suivez le tutoriel [Activation d’un jeu de données pour les mises à jour de profil](../../catalog/datasets/enable-upsert.md).
- **Fichier parquet contenant les champs à corriger et les champs d’identité du profil.** Le format de données pour l’application de correctifs à un lot est similaire au processus normal d’ingestion par lots. L’entrée requise est un fichier Parquet. En plus des champs à mettre à jour, les données chargées doivent contenir les champs d’identité afin de correspondre aux données de la banque de profils.

Une fois que vous disposez d’un jeu de données activé pour Profile et upsert, et d’un fichier Parquet contenant les champs que vous souhaitez corriger ainsi que les champs d’identité nécessaires, vous pouvez suivre les étapes de [ingestion de fichiers Parquet](#ingest-parquet-files) afin d’appliquer le correctif par ingestion par lots.

## Relecture d’un lot

Si vous souhaitez remplacer un lot déjà ingéré, vous pouvez le faire grâce à la fonctionnalité « relecture de lot ». Cette action équivaut à supprimer l’ancien lot et à en ingérer un nouveau pour le remplacer.

### Création d’un lot

Vous devrez tout d’abord créer un lot au format JSON en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni. Vous devrez également fournir le ou les anciens lots comme référence dans la section de relecture. Dans l’exemple ci-dessous, vous lisez à nouveau des lots avec des identifiants `batchIdA` et `batchIdB`.

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
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
    "imsOrg": "{ORG_ID}",
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
| `{FILE_NAME}` | Nom du fichier à charger. Veillez à utiliser un nom de fichier unique afin qu’il n’entre pas en conflit avec un autre fichier pour le lot de fichiers envoyé. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream. Évitez d’employer l’option curl -F, car elle utilise par défaut une requête à parties multiples incompatible avec l’API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Chemin d’accès complet et nom du fichier que vous essayez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `acme/customers/campaigns/summer.json`. |

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```http
200 OK
```

## Annexe

La section suivante contient des informations supplémentaires sur l’ingestion de données dans Experience Platform à l’aide de l’ingestion par lots.

### Transformation des données pour l’ingestion par lots

Pour ingérer un fichier de données dans Experience Platform, la structure hiérarchique du fichier doit être conforme au schéma [&#x200B; Modèle de données d’expérience (XDM)](../../xdm/home.md) associé au jeu de données dans lequel il est chargé.

Vous trouverez des informations sur le mappage d’un fichier CSV pour être conforme à un schéma XDM dans le document traitant des [exemples de transformations](../../etl/transformations.md), ainsi qu’un exemple de fichier de données JSON correctement formaté. Les exemples de fichiers fournis dans ce document se trouvent ici :

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)

Voici un exemple de payload JSONL (JSON à une seule ligne) formatée pour l’ingestion dans Experience Platform, provenant du fichier « CRM_single_line_profiles.json » :

+++Sélectionner pour afficher la payload

```json
{"person":{"name":{"courtesyTitle":"Mr","firstName":"Ewart","lastName":"Bennedsen"},"gender":"male","birthDayAndMonth":"09-25","birthDate":"2004-09-25","birthYear":2004},"identityMap":{"CRMID":[{"id":"71a16013-d805-7ece-9ac4-8f2cd66e8eaa","primary":false}],"ECID":[{"id":"87098882279810196101440938110216748923","primary":false},{"id":"55019962992006103186215643814973128178","primary":false}],"LOYALTYID":[{"id":"2e33192000007456-0365c00000000000","primary":true}]},"homePhone":{"number":"256-284-7231"},"personalEmail":{"address":"ebennedsenex@jiathis.com"},"homeAddress":{"street1":"72BuhlerCrossing","city":"Anniston","stateProvince":"Alabama","country":"US","postalCode":"36205","_schema":{"latitude":33.708276,"longitude":-85.7922905}}}
{"person":{"name":{"courtesyTitle":"Dr","firstName":"Novelia","lastName":"Ansteys"},"gender":"female","birthDayAndMonth":"10-31","birthDate":"1987-10-31","birthYear":1987},"identityMap":{"CRMID":[{"id":"2eeb6532-82e1-0d58-8955-bf97de66a6f5","primary":false}],"ECID":[{"id":"50829196174854544323574004005273946998","primary":false},{"id":"65233136134594262632703695260919939885","primary":false}],"LOYALTYID":[{"id":"2e3319208000765b-3811c00000000001","primary":true}]},"homePhone":{"number":"704-181-6371"},"personalEmail":{"address":"nansteysdk@spotify.com"},"homeAddress":{"street1":"79NorthfieldHill","city":"Charlotte","stateProvince":"NorthCarolina","country":"US","postalCode":"28299","_schema":{"latitude":35.2188655,"longitude":-80.8108888}}}
{"person":{"name":{"courtesyTitle":"Mr","firstName":"Ulises","lastName":"Mochan"},"gender":"male","birthDayAndMonth":"03-20","birthDate":"1996-03-20","birthYear":1996},"identityMap":{"CRMID":[{"id":"6f393075-addb-bdd6-73f8-31c393b700f5","primary":false}],"ECID":[{"id":"70086119428645095847094710218289660855","primary":false},{"id":"82011353387947708954389153068944017636","primary":false}],"LOYALTYID":[{"id":"2e33192080003023-26b2000000000002","primary":true}]},"homePhone":{"number":"720-837-4159"},"personalEmail":{"address":"umochanco@gnu.org"},"homeAddress":{"street1":"00671MifflinTrail","city":"Lacolle","stateProvince":"Québec","country":"CA","postalCode":"E5A","_schema":{"latitude":45.08338,"longitude":-73.36585}}}
{"person":{"name":{"courtesyTitle":"Mrs","firstName":"Friederike","lastName":"Durrell"},"gender":"female","birthDayAndMonth":"01-3","birthDate":"1979-01-3","birthYear":1979},"identityMap":{"CRMID":[{"id":"33d018ec-5fed-f1a3-56aa-079370a9511b","primary":false}],"ECID":[{"id":"50164729868919217963697788808932473456","primary":false},{"id":"64452712468609735658703639722261004071","primary":false}],"LOYALTYID":[{"id":"2e33192080006dfc-0cdf400000000003","primary":true}]},"homePhone":{"number":"798-528-3458"},"personalEmail":{"address":"fdurrellbj@utexas.edu"},"homeAddress":{"street1":"47FremontHill","city":"Independencia","stateProvince":"VeracruzLlave","country":"MX","postalCode":"91891","_schema":{"latitude":19.3803931,"longitude":-99.1476908}}}
```

+++

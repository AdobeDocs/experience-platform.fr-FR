---
keywords: Experience Platform;home;popular topics;dataset;Dataset;create a dataset;create dataset;enable dataset
solution: Experience Platform
title: Création d’un jeu de données
topic: developer guide
description: Ce document explique comment créer un objet de jeu de données dans le catalogue.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 66%

---


# Création d’un jeu de données

In order to create a dataset using the [!DNL Catalog] API, you must know the `$id` value of the [!DNL Experience Data Model] (XDM) schema on which the dataset will be based. Once you have the schema ID, you can create a dataset by making a POST request to the `/datasets` endpoint in the [!DNL Catalog] API.

>[!NOTE]
>
>This document only covers how to create a dataset object in [!DNL Catalog]. Pour obtenir des instructions complètes sur la création, le remplissage et la surveillance d’un jeu de données, reportez-vous au [tutoriel](../datasets/create.md) suivant.

**Format d’API**

```HTTP
POST /dataSets
```

**Requête**

La requête suivante crée un jeu de données se référant à un schéma précédemment défini.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du jeu de données à créer. |
| `schemaRef.id` | La valeur `$id` de l’URI pour le schéma XDM sur lequel sera basé le jeu de données. |

>[!NOTE]
>
> Cet exemple utilise le format de fichier [parquet](https://parquet.apache.org/documentation/latest/) pour sa propriété `containerFormat`. Vous trouverez un exemple d’utilisation du format de fichier JSON dans le [guide de développement de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un objet de réponse constitué d’un tableau contenant l’identifiant du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

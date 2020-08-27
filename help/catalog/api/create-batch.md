---
keywords: Experience Platform;home;popular topics;create batch;catalog service;api
solution: Experience Platform
title: Création d’un jeu de données
topic: developer guide
description: Pour qu’un jeu de données puisse ingérer des données, un lot doit lui être associé. A l’aide de la valeur id d’un jeu de données existant, vous pouvez créer un lot en envoyant une requête de POST au point de terminaison /batches de l’API Catalog.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 79%

---


# Création d’un lot

Pour qu’un jeu de données puisse ingérer des données, un lot doit lui être associé. À l’aide de la valeur `id` d’un jeu de données existant, vous pouvez créer un lot en envoyant une requête POST vers le point de terminaison `/batches` dans l’API [!DNL Catalog]

**Format d’API**

```HTTP
POST /batches
```

**Requête**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Propriété | Description |
| --- | --- |
| `datasetId` | L’`id` du jeu de données auquel le lot sera associé. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) ainsi qu’un objet de réponse contenant les détails du lot nouvellement créé, y compris son `id`, une chaîne en lecture seule générée par le système.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

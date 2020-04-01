---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un jeu de données
topic: developer guide
translation-type: tm+mt
source-git-commit: a25ca22fb8ec9eb95f74e4fd76a7f18e87343085

---


# Création d’un lot

Pour qu’un jeu de données puisse assimiler des données, un lot doit lui être associé. A l’aide de la `id` valeur d’un jeu de données existant, vous pouvez créer un lot en envoyant une requête POST au point de fin `/batches` dans l’API de catalogue.

**Format API**

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
| `datasetId` | Le jeu `id` de données auquel le lot sera associé. |

**Réponse**

Une réponse réussie renvoie HTTP Status 201 (Créé) et un objet de réponse contenant les détails du lot nouvellement créé, y compris sa chaîne générée par le système `id`, en lecture seule.

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

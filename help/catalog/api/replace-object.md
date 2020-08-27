---
keywords: Experience Platform;home;popular topics;catalog;api;replace an object
solution: Experience Platform
title: Remplacement d’un objet
topic: developer guide
description: Vous pouvez remplacer les contenus d’un objet Catalog à l’aide d’une requête PUT, dans lequel l’intégralité des ressources est remplacée par le payload de la requête.
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 68%

---


# Remplacement d’un objet

You can overwrite the contents of a [!DNL Catalog] object using a PUT request, wherein the entire resource is replaced with the request payload.

>[!NOTE]
>
>If you only need to update a few specific fields within a [!DNL Catalog] object, using a PATCH request may be more efficient.

**Format d’API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be replaced. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante remplace un jeu de données avec les valeurs fournies dans le payload.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**Réponse**

Une réponse réussie renvoie un tableau contenant l’identifiant de l’objet remplacé. Cet identifiant doit correspondre à celui envoyé dans la requête PUT. L’exécution d’une requête GET pour cet objet affiche désormais que ses détails ont été remplacés par ceux fournis dans le payload de la requête PUT précédente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

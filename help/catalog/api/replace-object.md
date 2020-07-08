---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Remplacement d’un objet
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 4%

---


# Remplacement d’un objet

Vous pouvez remplacer le contenu d’un objet Catalog à l’aide d’une requête PUT, dans laquelle la ressource entière est remplacée par la charge utile de la requête.

>[!NOTE]
>
>Si vous devez uniquement mettre à jour quelques champs spécifiques dans un objet Catalog, il peut s’avérer plus efficace d’utiliser une requête PATCH.

**Format d’API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à remplacer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique à mettre à jour. |

**Requête**

La requête suivante remplace un jeu de données par les valeurs fournies dans la charge utile.

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

Une réponse réussie renvoie un tableau contenant l&#39;identifiant de l&#39;objet remplacé. Cet identifiant doit correspondre à celui envoyé dans la demande PUT. L’exécution d’une requête GET pour cet objet montre maintenant que ses détails ont été remplacés par ceux fournis dans la charge utile de la requête PUT précédente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

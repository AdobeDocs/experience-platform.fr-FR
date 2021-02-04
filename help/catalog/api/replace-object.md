---
keywords: Experience Platform ; accueil ; rubriques populaires ; catalogue ; api ; remplacer un objet
solution: Experience Platform
title: Remplacement d’un objet
topic: developer guide
description: Vous pouvez remplacer les contenus d’un objet Catalog à l’aide d’une requête PUT, dans lequel l’intégralité des ressources est remplacée par le payload de la requête.
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 64%

---


# Remplacement d’un objet

Vous pouvez remplacer le contenu d&#39;un objet [!DNL Catalog] à l&#39;aide d&#39;une requête de PUT, dans laquelle la ressource entière est remplacée par la charge utile de la requête.

>[!NOTE]
>
>Si vous devez uniquement mettre à jour quelques champs spécifiques dans un objet [!DNL Catalog], l&#39;utilisation d&#39;une requête de PATCH peut s&#39;avérer plus efficace.

**Format d’API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d&#39;objet [!DNL Catalog] à remplacer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

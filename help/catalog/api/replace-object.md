---
keywords: Experience Platform;accueil;rubriques populaires;catalogue;api;remplacer un objet
solution: Experience Platform
title: Remplacement d’un objet de catalogue
description: Vous pouvez remplacer les contenus d’un objet Catalog à l’aide d’une requête PUT, dans lequel l’intégralité des ressources est remplacée par le payload de la requête.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 60%

---

# Remplacement d’un objet Catalogue

Vous pouvez remplacer le contenu d’un objet [!DNL Catalog] à l’aide d’une requête de PUT, dans laquelle la ressource entière est remplacée par le payload de la requête.

>[!NOTE]
>
>Si vous n’avez besoin de mettre à jour que quelques champs spécifiques dans un objet [!DNL Catalog], l’utilisation d’une requête de PATCH peut être plus efficace.

**Format d’API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Le type d’objet [!DNL Catalog] à remplacer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante remplace un jeu de données avec les valeurs fournies dans le payload.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**Réponse**

Une réponse réussie renvoie un tableau contenant l’identifiant de l’objet remplacé. Cet identifiant doit correspondre à celui envoyé dans la requête PUT. L’exécution d’une requête GET pour cet objet affiche désormais que ses détails ont été remplacés par ceux fournis dans le payload de la requête PUT précédente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

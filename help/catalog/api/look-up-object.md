---
keywords: Experience Platform;home;popular topics;catalog;object lookup;api
solution: Experience Platform
title: Recherche d’un objet
topic: developer guide
description: 'Si vous connaissez l’identifiant unique d’un objet Catalog spécifique, vous pouvez exécuter une requête GET pour afficher les détails de cet objet. '
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 81%

---


# Recherche d’un objet

If you know the unique identifier for a specific [!DNL Catalog] object, you can perform a GET request to view that object&#39;s details.

>[!NOTE]
>
>Lors de l’affichage d’objets spécifiques, il est toujours recommandé de [filtrer par propriétés](filter-data.md) et de renvoyer uniquement les propriétés qui vous intéressent.

**Format d’API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be retrieved. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | L’identifiant de l’objet spécifique que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère un jeu de données à l’aide de son identifiant, renvoyant ses propriétés `name`, `description`, `state`, `tags` et `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie le jeu de données spécifié contenant uniquement les `properties` demandées dans le corps.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
>Les propriétés dont les valeurs comportent le préfixe `@` représentent des objets interconnectés. Consultez la section de l’annexe sur [l’affichage des objets interconnectés](appendix.md#view-interrelated-objects) pour savoir comment afficher les détails de ces objets.

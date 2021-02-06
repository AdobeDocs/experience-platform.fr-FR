---
keywords: Experience Platform ; accueil ; rubriques populaires ; catalogue ; recherche d’objet ; api
solution: Experience Platform
title: Rechercher un objet de catalogue
topic: developer guide
description: 'Si vous connaissez l’identifiant unique d’un objet Catalog spécifique, vous pouvez exécuter une requête GET pour afficher les détails de cet objet. '
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 71%

---


# Rechercher un objet Catalogue

Si vous connaissez l&#39;identifiant unique d&#39;un objet [!DNL Catalog] spécifique, vous pouvez exécuter une demande de GET pour vue des détails de cet objet.

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
| `{OBJECT_TYPE}` | Type d&#39;objet [!DNL Catalog] à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

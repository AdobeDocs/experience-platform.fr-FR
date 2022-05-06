---
keywords: Experience Platform;accueil;rubriques populaires;catalogue;recherche d’objet;api
solution: Experience Platform
title: Recherche d’un objet de catalogue
topic-legacy: developer guide
description: Si vous connaissez l’identifiant unique d’un objet Catalog spécifique, vous pouvez exécuter une requête GET pour afficher les détails de cet objet.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 71%

---

# Recherche d’un objet Catalogue

Si vous connaissez l’identifiant unique d’une [!DNL Catalog] , vous pouvez exécuter une requête de GET pour afficher les détails de cet objet.

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
| `{OBJECT_TYPE}` | Le type de [!DNL Catalog] à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | L’identifiant de l’objet spécifique que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère un jeu de données à l’aide de son identifiant, renvoyant ses propriétés `name`, `description`, `state`, `tags` et `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

---
keywords: Experience Platform;accueil;rubriques populaires;catalogue;recherche d’objet;api
solution: Experience Platform
title: Recherche d’un objet de catalogue
description: Si vous connaissez l’identifiant unique d’un objet Catalog spécifique, vous pouvez exécuter une requête GET pour afficher les détails de cet objet.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 44%

---

# Recherche d’un objet Catalogue

Si vous connaissez l’identifiant unique d’un objet [!DNL Catalog] spécifique, vous pouvez exécuter une requête de GET pour afficher les détails de cet objet.

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
| `{OBJECT_TYPE}` | Type d’objet [!DNL Catalog] à récupérer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | L’identifiant de l’objet spécifique que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère un jeu de données à l’aide de son identifiant, renvoyant ses propriétés `name`, `description`, `tags` et `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
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
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>Les propriétés dont les valeurs comportent le préfixe `@` représentent des objets interconnectés. Consultez la section de l’annexe sur [l’affichage des objets interconnectés](appendix.md#view-interrelated-objects) pour savoir comment afficher les détails de ces objets.

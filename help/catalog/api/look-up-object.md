---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Rechercher un objet
topic: developer guide
translation-type: tm+mt
source-git-commit: 4dcd174eda98fee1e8cf668819809bd061c6e8bb
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 2%

---


# Rechercher un objet

Si vous connaissez l&#39;identifiant unique d&#39;un objet Catalog spécifique, vous pouvez exécuter une requête GET pour vue les détails de cet objet.

>[!NOTE] Lors de l’affichage d’objets spécifiques, il est toujours recommandé de [filtrer par propriétés](filter-data.md) et de ne renvoyer que les propriétés qui vous intéressent.

**Format d’API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificateur de l&#39;objet spécifique que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère un jeu de données par son identifiant, en renvoyant ses `name`, `description`, `state`, `tags`et `files` propriétés.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie le jeu de données spécifié avec uniquement le jeu demandé `properties` dans le corps.

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

>[!NOTE] Les propriétés dont les valeurs comportent un préfixe `@` représentent des objets interconnectés. Consultez la section de l’annexe sur l’ [affichage des objets](appendix.md#view-interrelated-objects) interconnectés pour savoir comment vue les détails de ces objets.

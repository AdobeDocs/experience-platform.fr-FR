---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Rechercher plusieurs objets
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 2%

---


# Rechercher plusieurs objets

Si vous souhaitez vue plusieurs objets spécifiques, plutôt que d’effectuer une requête par objet, Catalog fournit un raccourci simple pour demander plusieurs objets du même type. Vous pouvez utiliser une seule requête GET pour renvoyer plusieurs objets spécifiques en incluant une liste d’ID séparée par des virgules.

>[!NOTE]
>
>Même lorsque vous demandez des objets de catalogue spécifiques, il est recommandé de n’envoyer que les propriétés dont vous avez besoin que `properties` le paramètre de requête.

**Format d’API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| `{OBJECT_TYPE}` | Type d&#39;objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Identifiant de l&#39;un des objets spécifiques que vous souhaitez récupérer. |

**Requête**

La requête suivante inclut une liste d’ID de jeux de données séparés par des virgules ainsi qu’une liste de propriétés séparées par des virgules à renvoyer pour chaque jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste des jeux de données spécifiés, contenant uniquement les propriétés demandées (`name`, `description`et `files`) pour chacun d’eux.

>[!NOTE]
>
>Si un objet renvoyé ne contient pas un ou plusieurs des propriétés demandées indiquées par la `properties` requête, la réponse renvoie uniquement les propriétés demandées qu&#39;elle inclut, comme indiqué dans les sections &quot;Exemple de jeu de données 3&quot; et &quot;Exemple de jeu de données 4&quot; ci-dessous.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```

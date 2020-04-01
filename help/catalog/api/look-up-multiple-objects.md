---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recherche de plusieurs objets
topic: developer guide
translation-type: tm+mt
source-git-commit: f3e9da9ab3d02006c07c59b17751c971a95d49bc

---


# Recherche de plusieurs objets

Si vous souhaitez plusieurs objets spécifiques au lieu d’effectuer une requête par objet, le catalogue fournit un raccourci simple pour demander plusieurs objets du même type. Vous pouvez utiliser une requête GET unique pour renvoyer plusieurs objets spécifiques en incluant un d’ID séparé par des virgules.

>[!NOTE] Même lors de la demande d’objets de catalogue spécifiques, il est toujours recommandé de `properties` le paramètre de renvoyer uniquement les propriétés dont vous avez besoin.

**Format API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> || `{ID}` | Identifiant de l&#39;un des objets spécifiques que vous souhaitez récupérer. |

**Requête**

La requête suivante inclut un d’ID de jeu de données séparé par des virgules, ainsi qu’un de propriétés séparées par des virgules à renvoyer pour chaque jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un  des jeux de données spécifiés, contenant uniquement les propriétés demandées (`name`, `description`et `files`) pour chacun d’eux.

>[!NOTE] Si un objet renvoyé ne contient pas un ou plusieurs des propriétés demandées indiquées par le `properties` , la réponse renvoie uniquement les propriétés demandées qu’il inclut, comme illustré dans les sections &quot;Exemple de jeu de données 3&quot; et &quot;Exemple de jeu de données 4&quot; ci-dessous.

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

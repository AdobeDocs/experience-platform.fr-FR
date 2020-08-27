---
keywords: Experience Platform;home;popular topics;catalog;multiple object lookup;api
solution: Experience Platform
title: Recherche de plusieurs objets
topic: developer guide
description: Si vous souhaitez afficher plusieurs objets spécifiques au lieu d’effectuer une requête par objet, le catalogue fournit un raccourci simple pour demander plusieurs objets du même type. Vous pouvez utiliser une requête GET unique pour renvoyer plusieurs objets spécifiques en incluant une liste d’identifiants séparés par des virgules.
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 63%

---


# Recherche de plusieurs objets

If you wish to view several specific objects, rather than making one request per object, [!DNL Catalog] provides a simple shortcut for requesting multiple objects of the same type. Vous pouvez utiliser une requête GET unique pour renvoyer plusieurs objets spécifiques en incluant une liste d’identifiants séparés par des virgules.

>[!NOTE]
>
>Even when requesting specific [!DNL Catalog] objects, it is still best practice to `properties` query parameter to return only the properties you need.

**Format d’API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| `{OBJECT_TYPE}` | Le type d’objets à récupérer. [!DNL Catalog] Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Un identifiant de l’un des objets spécifiques que vous souhaitez récupérer. |

**Requête**

La requête suivante inclut une liste d’identifiants de jeux de données séparés par des virgules, ainsi qu’une liste de propriétés séparées par des virgules à renvoyer pour chaque jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste des jeux de données spécifiés contenant uniquement les propriétés demandées (`name`, `description` et `files`) pour chacun d’eux.

>[!NOTE]
>
>If a returned object does not contain one ore more of the requested properties indicated by the `properties` query, the response returns only the requested properties that it does include, as shown in ***`Sample Dataset 3`*** and ***`Sample Dataset 4`*** below.

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

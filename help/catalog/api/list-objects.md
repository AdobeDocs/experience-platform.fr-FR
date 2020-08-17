---
keywords: Experience Platform;home;popular topics;filter;Filter;filter data;Filter data
solution: Experience Platform
title: Liste des objets
topic: developer guide
description: Vous pouvez récupérer une liste de tous les objets disponibles d’un type spécifique à l’aide d’un seul appel API. Une bonne pratique consiste à inclure des filtres qui limitent la taille de la réponse.
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 58%

---


# Liste des objets

Vous pouvez récupérer une liste de tous les objets disponibles d’un type spécifique à l’aide d’un seul appel API. Une bonne pratique consiste à inclure des filtres qui limitent la taille de la réponse.

**Format d’API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be listed. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Un paramètre de requête utilisé pour filtrer les résultats renvoyés dans la réponse. Plusieurs paramètres sont séparés par des esperluettes (`&`). Pour plus d’informations, consultez le guide sur le [filtrage des données de Catalog](filter-data.md). |

**Requête**

L’exemple de requête ci-dessous récupère une liste de jeux de données, avec un filtre `limit` réduisant la réponse à cinq résultats et un filtre `properties` limitant les propriétés affichées pour chaque jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

A successful response returns a list of [!DNL Catalog] objects in the form of key-value pairs, filtered by the query parameters provided in the request. For each key-value pair, the key represents a unique identifier for the [!DNL Catalog] object in question, which can then be used in another call to [view that specific object](look-up-object.md) for more details.

>[!NOTE]
>
>If a returned object does not contain one or more of the requested properties indicated by the `properties` query, the response returns only the requested properties that it does include, as shown in ***`Sample Dataset 3`*** and ***`Sample Dataset 4`*** below.

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

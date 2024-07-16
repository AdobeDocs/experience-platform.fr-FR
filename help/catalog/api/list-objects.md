---
keywords: Experience Platform;accueil;rubriques populaires;filtre;filtre;filtrer les données;filtrer les données
solution: Experience Platform
title: Objets Catalogue de listes
description: Vous pouvez récupérer une liste de tous les objets disponibles d’un type spécifique à l’aide d’un seul appel API. Une bonne pratique consiste à inclure des filtres qui limitent la taille de la réponse.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 53%

---

# Objets Catalogue de listes

Vous pouvez récupérer une liste de tous les objets disponibles d’un type spécifique à l’aide d’un seul appel API. Une bonne pratique consiste à inclure des filtres qui limitent la taille de la réponse.

**Format d’API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Le type d’objet [!DNL Catalog] à répertorier. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | Un paramètre de requête utilisé pour filtrer les résultats renvoyés dans la réponse. Plusieurs paramètres sont séparés par des esperluettes (`&`). Pour plus d’informations, consultez le guide sur le [filtrage des données de Catalog](filter-data.md). |

**Requête**

L’exemple de requête ci-dessous récupère une liste de jeux de données, avec un filtre `limit` réduisant la réponse à cinq résultats et un filtre `properties` limitant les propriétés affichées pour chaque jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’objets [!DNL Catalog] sous la forme de paires clé-valeur, filtrées par les paramètres de requête fournis dans la requête. Pour chaque paire clé-valeur, la clé représente un identifiant unique pour l’objet [!DNL Catalog] en question, qui peut ensuite être utilisé dans un autre appel à [afficher cet objet spécifique](look-up-object.md) pour plus de détails.

>[!NOTE]
>
>Si un objet renvoyé ne contient pas une ou plusieurs des propriétés demandées indiquées par la requête `properties`, la réponse renvoie uniquement les propriétés demandées incluses, comme illustré dans les sections ***`Sample Dataset 3`*** et ***`Sample Dataset 4`*** ci-dessous.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```

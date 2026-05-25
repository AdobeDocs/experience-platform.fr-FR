---
keywords: Experience Platform;accueil;rubriques populaires;filtre;Filtrer;filtrer les données;Filtrer les données
solution: Experience Platform
title: Liste des objets de catalogue
description: Vous pouvez récupérer une liste de tous les objets disponibles d’un type spécifique à l’aide d’un seul appel API. Une bonne pratique consiste à inclure des filtres qui limitent la taille de la réponse.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
TQID: https://experienceleague.adobe.com/D9kta9wIdF6XxGsLc-09mvxkyT0r5k8zfXpNJ2CLSO4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 244
ht-degree: 53%

---

# Liste des objets de catalogue

Vous pouvez récupérer une liste de tous les objets disponibles d’un type spécifique à l’aide d’un seul appel API. Une bonne pratique consiste à inclure des filtres qui limitent la taille de la réponse.

**Format d’API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type de [!DNL Catalog] objet à répertorier. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

Une réponse réussie renvoie une liste d’objets [!DNL Catalog] sous la forme de paires clé-valeur, filtrées par les paramètres de requête fournis dans la requête. Pour chaque paire clé-valeur, la clé représente un identifiant unique pour l’objet [!DNL Catalog] en question, qui peut ensuite être utilisé dans un autre appel pour [afficher cet objet spécifique](look-up-object.md) pour plus d’informations.

>[!NOTE]
>
>Si un objet renvoyé ne contient pas une ou plusieurs des propriétés demandées indiquées par la requête `properties`, la réponse renvoie uniquement les propriétés demandées qu’elle inclut, comme indiqué dans les ***`Sample Dataset 3`*** et ***`Sample Dataset 4`*** ci-dessous.

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

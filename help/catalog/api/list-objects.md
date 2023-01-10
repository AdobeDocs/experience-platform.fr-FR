---
keywords: Experience Platform;accueil;rubriques populaires;filtre;filtre;filtrer les données;filtrer les données
solution: Experience Platform
title: Objets Catalogue de listes
description: Vous pouvez récupérer une liste de tous les objets disponibles d’un type spécifique à l’aide d’un seul appel API. Une bonne pratique consiste à inclure des filtres qui limitent la taille de la réponse.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
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
| `{OBJECT_TYPE}` | Le type de [!DNL Catalog] à répertorier. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

Une réponse réussie renvoie une liste de [!DNL Catalog] sous la forme de paires clé-valeur, filtrées par les paramètres de requête fournis dans la requête. Pour chaque paire clé-valeur, la clé représente un identifiant unique pour la variable [!DNL Catalog] objet en question, qui peut ensuite être utilisé dans un autre appel à [afficher cet objet spécifique ;](look-up-object.md) pour plus d’informations.

>[!NOTE]
>
>Si un objet renvoyé ne contient pas une ou plusieurs des propriétés demandées indiquées par la variable `properties` , la réponse renvoie uniquement les propriétés demandées qu’elle inclut, comme indiqué dans la section ***`Sample Dataset 3`*** et ***`Sample Dataset 4`*** ci-dessous.

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

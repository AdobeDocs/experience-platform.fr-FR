---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' d’objets'
topic: developer guide
translation-type: tm+mt
source-git-commit: 71c73a3899ccdd1c024a811b36c411915a3b14be

---


#  d’objets

Vous pouvez récupérer un de tous les objets disponibles d’un type spécifique par le biais d’un appel d’API unique, la meilleure pratique étant d’inclure des  qui limitent la taille de la réponse.

**Format API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à répertorier. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Paramètre  utilisé pour filtrer les résultats renvoyés dans la réponse. Plusieurs paramètres sont séparés par des esperluettes (`&`). Pour plus d’informations, consultez le guide sur le [filtrage des données](filter-data.md) du catalogue. |

**Requête**

L’exemple de requête ci-dessous récupère un de jeux de données, avec un `limit` filtre qui réduit la réponse à cinq résultats et un `properties` filtre qui limite les propriétés affichées pour chaque jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un  d’objets Catalog sous la forme de paires clé-valeur, filtré par les paramètres  fournis dans la requête. Pour chaque paire clé-valeur, la clé représente un identifiant unique pour l’objet Catalog en question, qui peut ensuite être utilisé dans un autre appel pour [cet objet](look-up-object.md) spécifique pour plus de détails.

>[!NOTE] Si un objet renvoyé ne contient pas une ou plusieurs des propriétés demandées indiquées par le `properties` , la réponse renvoie uniquement les propriétés demandées qu’il inclut, comme indiqué dans les sections &quot;Exemple de jeu de données 3&quot; et &quot;Exemple de jeu de données 4&quot; ci-dessous.

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

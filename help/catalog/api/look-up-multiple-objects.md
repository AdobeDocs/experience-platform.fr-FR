---
keywords: Experience Platform;accueil;rubriques populaires;catalogue;recherche d’objets multiples;api
solution: Experience Platform
title: Recherche De Plusieurs Objets Catalogue
description: Si vous souhaitez afficher plusieurs objets spécifiques au lieu d’effectuer une requête par objet, le catalogue fournit un raccourci simple pour demander plusieurs objets du même type. Vous pouvez utiliser une requête GET unique pour renvoyer plusieurs objets spécifiques en incluant une liste d’identifiants séparés par des virgules.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 99837f7aa803f3f992dce2127089bff6279c7008
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 49%

---

# Recherche de plusieurs objets Catalog

Si vous souhaitez afficher plusieurs objets spécifiques, plutôt qu’effectuer une requête par objet, [!DNL Catalog] fournit un raccourci simple pour demander plusieurs objets du même type. Vous pouvez utiliser une requête GET unique pour renvoyer plusieurs objets spécifiques en incluant une liste d’identifiants séparés par des virgules.

>[!NOTE]
>
>Même lors de la demande d’objets [!DNL Catalog] spécifiques, il est toujours recommandé au paramètre de requête `properties` de renvoyer uniquement les propriétés dont vous avez besoin.

**Format d’API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Paramètre | Description |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Type d’objet [!DNL Catalog] à récupérer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{ID}` | Identifiant de l’un des objets spécifiques que vous souhaitez récupérer. |

**Requête**

La requête suivante inclut une liste d’identifiants de jeux de données séparés par des virgules, ainsi qu’une liste de propriétés séparées par des virgules à renvoyer pour chaque jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste des jeux de données spécifiés contenant uniquement les propriétés demandées (`name`, `description` et `files`) pour chacun d’eux.

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

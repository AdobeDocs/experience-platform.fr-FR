---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mise à jour d’un objet
topic: developer guide
translation-type: tm+mt
source-git-commit: 4361032b419622d7decc02194d38885b114749e4

---


# Mise à jour d’un objet

Vous pouvez mettre à jour une partie d’un objet Catalog en incluant son ID dans le chemin d’une requête PATCH. Ce couvre les deux méthodes d’exécution des opérations PATCH sur les objets de catalogue :

* Utilisation des champs
* Utilisation de la notation de correctif JSON

>[!NOTE] Les opérations PATCH sur un objet ne peuvent pas modifier ses champs extensibles, qui représentent des objets interconnectés.  Les modifications apportées aux objets interconnectés doivent être effectuées directement.

## Mise à jour à l’aide de champs

L’exemple d’appel suivant montre comment mettre à jour un objet à l’aide de champs et de valeurs.

**Format API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à mettre à jour. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les champs `name` et `description` d’un jeu de données avec les valeurs fournies dans la charge utile. Les champs d’objet qui ne doivent pas être mis à jour peuvent être exclus de la charge utile.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;ID du jeu de données mis à jour. Cet ID doit correspondre à celui envoyé dans la requête PATCH. L’exécution d’une requête GET pour ce jeu de données montre désormais que seules les valeurs `name` et `description` ont été mises à jour, tandis que toutes les autres valeurs restent inchangées.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Mise à jour à l’aide de la notation de correctif JSON

L’exemple d’appel suivant montre comment mettre à jour un objet à l’aide du correctif JSON, comme indiqué dans [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Format API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à mettre à jour. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les champs `name` et `description` d’un jeu de données avec les valeurs fournies dans chaque objet de correctif JSON. Lors de l’utilisation du correctif JSON, vous devez également définir l’en-tête Content-Type sur `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Réponse**

Une réponse réussie renvoie un tableau contenant l’ID de l’objet mis à jour. Cet ID doit correspondre à celui envoyé dans la requête PATCH. L’exécution d’une requête GET pour cet objet montre désormais que seules les valeurs `name` et `description` ont été mises à jour, tandis que toutes les autres valeurs restent inchangées.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

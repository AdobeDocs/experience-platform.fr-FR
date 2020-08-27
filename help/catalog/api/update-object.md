---
keywords: Experience Platform;home;popular topics;catalog;api;update an object
solution: Experience Platform
title: Mise à jour d’un objet
topic: developer guide
description: 'Vous pouvez mettre à jour un objet Catalogue en incluant son identifiant dans le chemin d’accès d’une requête PATCH. Ce document couvre l’utilisation des champs et l’utilisation de la notation de correctif JSON pour effectuer des opérations de PATCH sur des objets de catalogue. '
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 85%

---


# Mise à jour d’un objet

You can update part of a [!DNL Catalog] object by including its ID in the path of a PATCH request. Ce document couvre les deux méthodes d’exécution des opérations PATCH sur les objets Catalogue :

* Utilisation des champs
* Utilisation de la notation par patch JSON

>[!NOTE]
>
>Les opérations PATCH sur un objet ne peuvent pas modifier ses champs extensibles, qui représentent des objets interconnectés. Les modifications d’objets interconnectés doivent être effectuées directement.

## Mise à jour à l’aide de champs

L’exemple d’appel suivant montre comment mettre à jour un objet à l’aide de champs et de valeurs.

**Format d’API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be updated. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les champs `name` et `description` d’un jeu de données avec les valeurs fournies dans le payload. Les champs d’objet qui ne doivent pas être mis à jour peuvent être exclus du payload.

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

Une réponse réussie renvoie un tableau contenant l’identifiant du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. En exécutant une requête GET pour ce jeu de données, vous voyez maintenant que seules les valeurs `name` et `description` ont été mises à jour, tandis que toutes les autres valeurs restent inchangées.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Mise à jour à l’aide de la notation par patch JSON

L’exemple d’appel suivant montre comment mettre à jour un objet à l’aide d’un patch JSON, comme indiqué dans [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Format d’API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be updated. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les champs `name` et `description` d’un jeu de données avec les valeurs fournies dans chaque objet de patch JSON. Lors de l’utilisation d’un patch JSON, vous devez aussi définir l’en-tête Content-Type sur `application/json-patch+json`.

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

Une réponse réussie renvoie un tableau contenant l’identifiant de l’objet mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. En exécutant une requête GET pour cet objet, vous voyez maintenant que seules les valeurs `name` et `description` ont été mises à jour, tandis que toutes les autres valeurs restent inchangées.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

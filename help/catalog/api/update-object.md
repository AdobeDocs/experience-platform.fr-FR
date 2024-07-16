---
keywords: Experience Platform;accueil;rubriques populaires;catalogue;api;mettre à jour un objet
solution: Experience Platform
title: Mise à jour d’un objet de catalogue
description: Vous pouvez mettre à jour un objet Catalogue en incluant son identifiant dans le chemin d’accès d’une requête PATCH. Ce document couvre l’utilisation des champs et l’utilisation de la notation JSON Patch pour effectuer des opérations de PATCH sur des objets Catalog.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 296a988a67871933723ad0474c113cb93fdbf255
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 74%

---

# Mise à jour d’un objet Catalogue

Vous pouvez mettre à jour une partie d’un objet [!DNL Catalog] en incluant son identifiant dans le chemin d’accès d’une requête de PATCH. Ce document couvre les deux méthodes d’exécution des opérations PATCH sur les objets Catalogue :

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
| `{OBJECT_TYPE}` | Le type d’objet [!DNL Catalog] à mettre à jour. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les champs `name` et `description` d’un jeu de données avec les valeurs fournies dans le payload. Les champs d’objet qui ne doivent pas être mis à jour peuvent être exclus du payload.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Pour plus d’informations sur la syntaxe du correctif JSON, consultez le [guide de base de l’API](../../landing/api-fundamentals.md#json-patch).

**Format d’API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Le type d’objet [!DNL Catalog] à mettre à jour. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les champs `name` et `description` d’un jeu de données avec les valeurs fournies dans chaque objet de patch JSON. Lors de l’utilisation d’un patch JSON, vous devez aussi définir l’en-tête Content-Type sur `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

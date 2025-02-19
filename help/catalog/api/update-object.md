---
keywords: Experience Platform;accueil;rubriques populaires;catalogue;api;mettre à jour un objet
solution: Experience Platform
title: Mise à jour d’un objet de catalogue
description: Vous pouvez mettre à jour un objet Catalogue en incluant son identifiant dans le chemin d’accès d’une requête PATCH. Ce document couvre l’utilisation des champs et de la notation JSON Patch pour effectuer des opérations PATCH sur des objets de catalogue.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 41%

---

# Mise à jour d’un objet Catalog

Vous pouvez mettre à jour une partie d’un objet [!DNL Catalog] en incluant son identifiant dans le chemin d’accès d’une requête PATCH. Ce document couvre les deux méthodes d’exécution des opérations PATCH sur les objets Catalogue :

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
| `{OBJECT_TYPE}` | Type de [!DNL Catalog] objet à mettre à jour. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

## Mise à jour à l’aide de la notation par patch JSON {#patch-notation}

L’exemple d’appel suivant montre comment mettre à jour un objet à l’aide d’un patch JSON, comme indiqué dans [RFC-6902](https://tools.ietf.org/html/rfc6902).

Pour plus d’informations sur la syntaxe JSON Patch, consultez le [guide des principes de base des API](../../landing/api-fundamentals.md#json-patch).

**Format d’API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type de [!DNL Catalog] objet à mettre à jour. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

## Mise à jour à l’aide de la notation PATCH v2 {#patch-v2-notation}

Le point d’entrée `/v2/dataSets/{DATASET_ID}` offre un moyen plus flexible de mettre à jour des attributs de jeux de données complexes ou profondément imbriqués.

En règle générale, lorsque vous mettez à jour un champ profondément imbriqué (tel que `a.b.c.d`), chaque niveau du chemin d’accès doit déjà exister. S’il manque un niveau, vous devez les créer manuellement avant de définir la valeur finale. Cela nécessite souvent plusieurs opérations, ce qui ajoute de la complexité et augmente le risque d’erreurs.

Le point d’entrée `/v2/dataSets/{DATASET_ID}` crée automatiquement tous les niveaux manquants dans le chemin d’accès. Au lieu de vérifier et d’ajouter manuellement des `b` et des `c` avant de `d` définir, l’opération de `v2` de PATCH effectue cette opération pour vous.

Lorsque vous envoyez une requête PATCH au point d’entrée `/v2/dataSets/{DATASET_ID}`, il vous suffit d’envoyer la structure finale et le système remplit les parties manquantes avant d’appliquer la mise à jour.

>[!NOTE]
>
>Les en-têtes `If-Match` et `If-None-Match` sont facultatifs pour le point d’entrée `/v2/dataSets/{id}`. Les requêtes PATCH vers ce point d’entrée fusionnent dynamiquement les mises à jour, ce qui permet d’apporter des modifications sans récupérer la dernière version du jeu de données. Bien que cela réduise le risque de perte de données des mises à jour simultanées, vous pouvez utiliser `If-Match` avec les dernières `etag` pour vous assurer que les modifications ne s’appliquent qu’à une version spécifique. Sinon, `If-None-Match` empêche les mises à jour si le jeu de données n’a pas été modifié depuis la dernière version connue.

**Format d’API**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Identifiant du jeu de données à mettre à jour. |

**Requête**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**Réponse**

Une réponse réussie renvoie un tableau contenant l’identifiant du jeu de données mis à jour, qui doit correspondre à l’identifiant envoyé dans la requête PATCH. L’exécution d’une requête GET pour cet objet indique désormais que l’objet `extensions.adobe_lakeHouse.rowExpiration` a été créé sans nécessiter d’étapes de création manuelles préalables.

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### Exemple de jeu de données avant et après la mise à jour

L’exemple JSON ci-dessous illustre la structure du jeu de données **avant** la requête PATCH, où l’objet `extensions.adobe_lakeHouse.rowExpiration` n’est pas présent dans le jeu de données.

+++Sélectionner pour afficher l’exemple

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

Le fichier JSON suivant affiche la structure du jeu de données **après** la requête PATCH. La mise à jour crée automatiquement l’objet `extensions.adobe_lakeHouse.rowExpiration` manquant sans étapes de création manuelles préalables. Cet exemple montre comment la requête `/v2/` PATCH élimine la nécessité de plusieurs opérations, ce qui rend les mises à jour plus simples et plus efficaces.


+++Sélectionner pour afficher l’exemple

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

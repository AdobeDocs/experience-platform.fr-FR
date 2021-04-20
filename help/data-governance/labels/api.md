---
keywords: Experience Platform ; accueil ; rubriques populaires ; gouvernance des données ; api du libellé d’utilisation des données ; api du service de stratégie
solution: Experience Platform
title: 'Gérer les étiquettes d’utilisation des données à l’aide d’API '
topic: developer guide
description: L’API Service de dataset vous permet d’appliquer et de modifier des étiquettes d’utilisation pour les jeux de données. Il fait partie des fonctionnalités de catalogue de données Adobe Experience Platform, mais est distinct de l’API Catalog Service qui gère les métadonnées des jeux de données.
translation-type: tm+mt
source-git-commit: 4e75e3fbdcd480c384411c2f33bad5b2cdcc5c42
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 7%

---


# Gérer les étiquettes d’utilisation des données à l’aide d’API

Ce document décrit la procédure à suivre pour gérer les étiquettes d’utilisation des données à l’aide de l’API [!DNL Policy Service] et de l’API [!DNL Dataset Service].

[[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) fournit plusieurs points de terminaison qui vous permettent de créer et de gérer des étiquettes d’utilisation des données pour votre organisation.

L&#39;API [!DNL Dataset Service] vous permet d&#39;appliquer et de modifier des étiquettes d&#39;utilisation pour les jeux de données. Il fait partie des fonctionnalités de catalogue de données Adobe Experience Platform, mais est distinct de l&#39;API [!DNL Catalog Service] qui gère les métadonnées des jeux de données.

## Prise en main

Avant de lire ce guide, suivez les étapes décrites dans la section [prise en main](../../catalog/api/getting-started.md) du guide du développeur du catalogue pour rassembler les informations d’identification nécessaires pour appeler les API [!DNL Platform].

Pour invoquer les points de terminaison [!DNL Dataset Service] décrits dans ce document, vous devez disposer de la valeur `id` unique pour un jeu de données spécifique. Si vous ne possédez pas cette valeur, consultez le guide [qui répertorie les objets de catalogue](../../catalog/api/list-objects.md) pour trouver les ID de vos jeux de données existants.

## Liste de toutes les étiquettes {#list-labels}

À l&#39;aide de l&#39;API [!DNL Policy Service], vous pouvez liste toutes les étiquettes `core` ou `custom` en adressant une demande de GET à `/labels/core` ou `/labels/custom`, respectivement.

**Format d’API**

```http
GET /labels/core
GET /labels/custom
```

**Requête**

La requête suivante liste tous les libellés personnalisés créés dans votre organisation.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d&#39;étiquettes personnalisées récupérées du système. Comme l&#39;exemple de demande ci-dessus a été envoyé à `/labels/custom`, la réponse ci-dessous n&#39;affiche que les étiquettes personnalisées.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Rechercher une étiquette {#look-up-label}

Vous pouvez rechercher une étiquette spécifique en incluant la propriété `name` de cette étiquette dans le chemin d&#39;une demande de GET à l&#39;API [!DNL Policy Service].

**Format d’API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | La propriété `name` du libellé personnalisé que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère le libellé personnalisé `L2`, comme indiqué dans le chemin d’accès.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’étiquette personnalisée.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Créer ou mettre à jour une étiquette personnalisée {#create-update-label}

Pour créer ou mettre à jour une étiquette personnalisée, vous devez envoyer une requête de PUT à l&#39;API [!DNL Policy Service].

**Format d’API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | Propriété `name` d’une étiquette personnalisée. Si aucune étiquette personnalisée portant ce nom n’existe, une nouvelle étiquette est créée. S&#39;il en existe un, cette étiquette sera mise à jour. |

**Requête**

La demande suivante crée une nouvelle étiquette, `L3`, qui vise à décrire les données contenant des informations relatives aux plans de paiement sélectionnés par les clients.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Propriété | Description |
| --- | --- |
| `name` | Identifiant de chaîne unique pour l’étiquette. Cette valeur est utilisée à des fins de recherche et d’application de l’étiquette aux jeux de données et aux champs. Il est donc recommandé qu’elle soit courte et concise. |
| `category` | Catégorie de l&#39;étiquette. Bien que vous puissiez créer vos propres catégories pour les étiquettes personnalisées, il est vivement recommandé d’utiliser `Custom` si vous souhaitez que le libellé apparaisse dans l’interface utilisateur. |
| `friendlyName` | Nom convivial de l’étiquette, utilisé à des fins d’affichage. |
| `description` | (Facultatif) Description de l’étiquette afin de fournir un contexte plus poussé. |

**Réponse**

Une réponse réussie renvoie les détails d&#39;une étiquette personnalisée, avec le code HTTP 200 (OK) si une étiquette existante a été mise à jour, ou 201 (Créée) si une nouvelle étiquette a été créée.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Rechercher des étiquettes pour un jeu de données {#look-up-dataset-labels}

Vous pouvez rechercher les étiquettes d&#39;utilisation des données qui ont été appliquées à un jeu de données existant en adressant une demande de GET à l&#39;API [!DNL Dataset Service].

**Format d’API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur `id` unique du jeu de données dont vous souhaitez rechercher les étiquettes. |

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie les étiquettes d’utilisation des données qui ont été appliquées au jeu de données.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Propriété | Description |
| --- | --- |
| `labels` | Liste des étiquettes d’utilisation des données qui ont été appliquées au jeu de données. |
| `optionalLabels` | Liste de champs individuels au sein du jeu de données auxquels des étiquettes d’utilisation de données sont appliquées. Les sous-propriétés suivantes sont requises :<br/><br/>`option` : Objet contenant les attributs [!DNL Experience Data Model] (XDM) du champ. Les trois propriétés suivantes sont requises :<ul><li>`id`: Valeur URI  `$id` du schéma associé au champ.</li><li>`contentType`: Indique le format et la version du schéma. Pour plus d&#39;informations, consultez la section [versioning de schéma](../../xdm/api/getting-started.md#versioning) du guide de l&#39;API XDM.</li><li>`schemaPath`: Chemin d’accès à la propriété de schéma en question, écrite en  [syntaxe ](../../landing/api-fundamentals.md#json-pointer) JSON.</li></ul>`labels`: Liste d’étiquettes d’utilisation des données que vous souhaitez ajouter au champ. |

- id: Valeur URI $id pour le schéma XDM sur lequel repose le jeu de données.
- contentType : Indique le format et la version du schéma. Pour plus d&#39;informations, consultez la section [versioning de schéma](../../xdm/api/getting-started.md#versioning) du guide de l&#39;API XDM.
- schemaPath : Chemin d’accès à la propriété de schéma en question, écrit dans la syntaxe [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).

## Appliquer des étiquettes à un jeu de données {#apply-dataset-labels}

Vous pouvez créer un ensemble d&#39;étiquettes pour un jeu de données en les fournissant dans la charge utile d&#39;une requête de POST ou de PUT à l&#39;API [!DNL Dataset Service]. L’utilisation de l’une ou l’autre de ces méthodes remplace les étiquettes existantes et les remplace par celles fournies dans la charge utile.

**Format d’API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur `id` unique du jeu de données pour lequel vous créez des étiquettes. |

**Requête**

La demande de POST suivante ajoute une série d&#39;étiquettes au jeu de données, ainsi qu&#39;un champ spécifique dans ce jeu de données. Les champs fournis dans la charge utile sont identiques à ceux requis pour une demande de PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `labels` | Liste d’étiquettes d’utilisation des données que vous souhaitez ajouter au jeu de données. |
| `optionalLabels` | Liste de tous les champs individuels du jeu de données auxquels vous souhaitez ajouter des étiquettes. Chaque élément de ce tableau doit avoir les propriétés suivantes :<br/><br/>`option`: Objet contenant les attributs [!DNL Experience Data Model] (XDM) du champ. Les trois propriétés suivantes sont requises :<ul><li>`id`: Valeur URI  `$id` du schéma associé au champ.</li><li>`contentType`: Indique le format et la version du schéma. Pour plus d&#39;informations, consultez la section [versioning de schéma](../../xdm/api/getting-started.md#versioning) du guide de l&#39;API XDM.</li><li>`schemaPath`: Chemin d’accès à la propriété de schéma en question, écrite en  [syntaxe ](../../landing/api-fundamentals.md#json-pointer) JSON.</li></ul>`labels`: Liste d’étiquettes d’utilisation des données que vous souhaitez ajouter au champ. |

**Réponse**

Une réponse réussie renvoie les étiquettes qui ont été ajoutées au jeu de données.

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## Supprimer des étiquettes d&#39;un jeu de données {#remove-dataset-labels}

Vous pouvez supprimer les étiquettes appliquées à un jeu de données en envoyant une requête de DELETE à l&#39;API [!DNL Dataset Service].

**Format d’API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur `id` unique du jeu de données dont vous souhaitez supprimer les étiquettes. |

**Requête**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Réponse réussie : état HTTP 200 (OK), indiquant que les étiquettes ont été supprimées. Vous pouvez [rechercher les étiquettes existantes](#look-up-dataset-labels) pour le jeu de données dans un appel distinct pour le confirmer.

## Étapes suivantes

En lisant ce document, vous avez appris à gérer les étiquettes d’utilisation des données à l’aide d’API.

Une fois que vous avez ajouté des étiquettes d&#39;utilisation de données au niveau du jeu de données et du champ, vous pouvez commencer à assimiler des données dans [!DNL Experience Platform]. Pour en savoir plus, commencez par lire la [documentation sur l’ingestion de données](../../ingestion/home.md).

Désormais, vous pouvez également définir des stratégies d’utilisation des données en fonction des libellés que vous avez appliqués. Pour plus d’informations, consultez la [présentation des stratégies d’utilisation des données](../policies/overview.md).

Pour plus d&#39;informations sur la gestion des jeux de données dans [!DNL Experience Platform], consultez l&#39;[aperçu des jeux de données](../../catalog/datasets/overview.md).
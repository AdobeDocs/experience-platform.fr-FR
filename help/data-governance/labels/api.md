---
keywords: Experience Platform;accueil;rubriques populaires;gouvernance des données;api étiquette dʼutilisation des données;api de service de politique
solution: Experience Platform
title: Gestion des étiquettes dʼutilisation des données à lʼaide dʼAPI
description: LʼAPI Dataset Service vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI Catalog Service qui gère les métadonnées du jeu de données.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 100%

---


# Gestion des étiquettes dʼutilisation des données à lʼaide dʼAPI

Ce document fournit des instructions sur la manière de gérer les étiquettes dʼutilisation des données à lʼaide de lʼAPI [!DNL Policy Service] et de lʼAPI [!DNL Dataset Service].

[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) fournit plusieurs points d’entrée qui vous permettent de créer et de gérer des étiquettes dʼutilisation des données pour votre organisation.

LʼAPI [!DNL Dataset Service] vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI [!DNL Catalog Service] qui gère les métadonnées du jeu de données.

## Prise en main

Avant de lire ce guide, suivez les étapes décrites dans la [section Prise en main](../../catalog/api/getting-started.md) du guide de développement de Catalogue pour rassembler les informations dʼidentification nécessaires afin de réaliser des appels aux API de [!DNL Platform].

Pour réaliser des appels vers les points d’entrée de [!DNL Dataset Service] décrits dans ce document, vous devez disposer de la valeur `id` unique pour un jeu de données spécifique. Si vous ne possédez pas cette valeur, consultez le guide qui [répertorie les objets de Catalogue](../../catalog/api/list-objects.md) afin de trouver les identifiants de vos jeux de données existants.

## Liste de toutes les étiquettes {#list-labels}

À lʼaide de lʼAPI [!DNL Policy Service], vous pouvez répertorier toutes les étiquettes `core` ou `custom` en réalisant une requête GET à `/labels/core` ou `/labels/custom`, respectivement.

**Format d’API**

```http
GET /labels/core
GET /labels/custom
```

**Requête**

La requête suivante répertorie toutes les étiquettes personnalisées créées dans votre organisation.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste dʼétiquettes personnalisées récupérées du système. Étant donné que lʼexemple de requête ci-dessus a été envoyé à `/labels/custom`, la réponse ci-dessous nʼaffiche que les étiquettes personnalisées.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## Recherche dʼune étiquette {#look-up-label}

Vous pouvez rechercher une étiquette spécifique en incluant la propriété `name` de cette étiquette dans le chemin dʼune requête GET à lʼAPI [!DNL Policy Service].

**Format d’API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | La propriété `name` de lʼétiquette personnalisée que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère lʼétiquette personnalisée `L2`, comme indiqué dans le chemin.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de lʼétiquette personnalisée.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
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

## Création ou mise à jour dʼune étiquette personnalisée {#create-update-label}

Pour créer ou mettre à jour une étiquette personnalisée, vous devez envoyer une requête PUT à lʼAPI [!DNL Policy Service].

**Format d’API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | Propriété `name` dʼune étiquette personnalisée. Si aucune étiquette personnalisée portant ce nom nʼexiste, une nouvelle étiquette est créée. Sʼil en existe une, cette étiquette sera mise à jour. |

**Requête**

La requête suivante crée une nouvelle étiquette, `L3`, qui vise à décrire les données contenant des informations relatives aux plans de paiement choisis par les clients.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Identifiant de chaîne unique pour lʼétiquette. Cette valeur est utilisée à des fins de recherche et dʼapplication de lʼétiquette aux jeux de données et aux champs. Il est donc recommandé quʼelle soit courte et concise. |
| `category` | Catégorie de lʼétiquette. Bien que vous puissiez créer vos propres catégories pour les étiquettes personnalisées, il est vivement recommandé dʼutiliser `Custom` si vous souhaitez que lʼétiquette apparaisse dans lʼinterface utilisateur. |
| `friendlyName` | Nom convivial de lʼétiquette, utilisé pour lʼaffichage. |
| `description` | (Facultatif) Description de lʼétiquette afin de fournir un contexte plus détaillé. |

**Réponse**

Une réponse réussie renvoie les détails de lʼétiquette personnalisée, avec le code HTTP 200 (OK) si une étiquette existante a été mise à jour, ou 201 (Created) si une nouvelle étiquette a été créée.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
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

## Recherche dʼétiquettes pour un jeu de données {#look-up-dataset-labels}

Vous pouvez rechercher les étiquettes dʼutilisation des données qui ont été appliquées à un jeu de données existant en envoyant une requête GET à lʼAPI [!DNL Dataset Service].

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les étiquettes dʼutilisation des données qui ont été appliquées au jeu de données.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
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
| `labels` | Liste dʼétiquettes dʼutilisation des données qui ont été appliquées au jeu de données. |
| `optionalLabels` | Liste de champs individuels au sein du jeu de données auxquels sont appliquées des étiquettes dʼutilisation de données. Les sous-propriétés suivantes sont requises :<br/><br/>`option` : Objet contenant les attributs [!DNL Experience Data Model] (XDM) du champ. Les trois propriétés suivantes sont requises :<ul><li>`id` : valeur URI `$id` du schéma associé au champ.</li><li>`contentType` : indique le format et la version du schéma. Pour plus d’informations, reportez-vous à la section [contrôle de version des schémas](../../xdm/api/getting-started.md#versioning) du guide de l’API XDM.</li><li>`schemaPath` : le chemin d’accès à la propriété de schéma en question, écrit en syntaxe [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).</li></ul>`labels` : liste dʼétiquettes dʼutilisation des données que vous souhaitez ajouter au champ. |

- id : la valeur URI $id pour le schéma XDM sur lequel le jeu de données est basé.
- contentType : indique le format et la version du schéma. Pour plus d’informations, reportez-vous à la section [contrôle de version des schémas](../../xdm/api/getting-started.md#versioning) du guide de l’API XDM.
- schemaPath : le chemin d’accès à la propriété de schéma en question, écrit dans la syntaxe [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).

## Appliquer des libellés à un jeu de données {#apply-dataset-labels}

Vous pouvez créer un ensemble dʼétiquettes pour un jeu de données en les fournissant dans la payload dʼune requête POST ou PUT à lʼAPI [!DNL Dataset Service]. Lʼutilisation de lʼune ou lʼautre de ces méthodes supprime les étiquettes existantes et les remplace par celles fournies dans la payload.

**Format d’API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur `id` unique du jeu de données pour lequel vous créez des étiquettes. |

**Requête**

La requête POST suivante ajoute une série dʼétiquettes au jeu de données, ainsi quʼun champ spécifique dans ce jeu de données. Les champs fournis dans la payload sont identiques à ceux requis pour une requête PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `labels` | Liste dʼétiquettes dʼutilisation des données que vous souhaitez ajouter au jeu de données. |
| `optionalLabels` | Liste de tous les champs individuels dans le jeu de données auxquels vous souhaitez ajouter des étiquettes. Chaque élément de ce tableau doit avoir les propriétés suivantes :<br/><br/>`option`objet contenant les attributs [!DNL Experience Data Model] (XDM) du champ. Les trois propriétés suivantes sont requises :<ul><li>`id` : valeur URI `$id` du schéma associé au champ.</li><li>`contentType` : indique le format et la version du schéma. Pour plus d’informations, reportez-vous à la section [contrôle de version des schémas](../../xdm/api/getting-started.md#versioning) du guide de l’API XDM.</li><li>`schemaPath` : le chemin d’accès à la propriété de schéma en question, écrit en syntaxe [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).</li></ul>`labels` : liste dʼétiquettes dʼutilisation des données que vous souhaitez ajouter au champ. |

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

## Suppression des étiquettes dʼun jeu de données {#remove-dataset-labels}

Vous pouvez supprimer les étiquettes appliquées à un jeu de données en envoyant une requête DELETE à lʼAPI [!DNL Dataset Service].

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Réponse réussie état HTTP 200 (OK), indiquant que les étiquettes ont été supprimées. Vous pouvez [rechercher les étiquettes existantes](#look-up-dataset-labels) pour le jeu de données dans un appel séparé pour confirmer cela.

## Étapes suivantes

En lisant ce document, vous avez appris la gestion des étiquettes dʼutilisation des données à lʼaide dʼAPI.

Une fois que vous avez ajouté des étiquettes dʼutilisation des données au niveau du jeu de données et du champ, vous pouvez commencer à ingérer des données dans [!DNL Experience Platform]. Pour en savoir plus, commencez par lire la [documentation sur l’ingestion de données](../../ingestion/home.md).

Désormais, vous pouvez également définir des politiques d’utilisation des données en fonction des libellés que vous avez appliqués. Pour plus d’informations, consultez la [présentation des politiques d’utilisation des données](../policies/overview.md).

Pour plus dʼinformations sur la gestion des jeux de données dans [!DNL Experience Platform], consultez la [présentation des jeux de données](../../catalog/datasets/overview.md).
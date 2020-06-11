---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Gérer les étiquettes d’utilisation des données à l’aide d’API '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 3%

---


# Gérer les étiquettes d’utilisation des données à l’aide d’API

L’API Service de dataset vous permet de gérer par programmation les étiquettes d’utilisation des jeux de données. Il fait partie des fonctionnalités de catalogue de données d’Adobe Experience Platform, mais est distinct de l’API Catalog Service qui gère les métadonnées des jeux de données.

Ce document décrit la procédure à suivre pour gérer les libellés d’utilisation des données au niveau du jeu de données et des champs à l’aide de l’API Service de dataset.

## Prise en main

Avant de lire ce guide, suivez les étapes décrites dans la section [](../../catalog/api/getting-started.md) Prise en main du guide du développeur de catalogue afin de rassembler les informations d’identification requises pour appeler [!DNL Platform] les API.

Pour appeler les points de terminaison décrits dans les sections ci-dessous, vous devez disposer de la `id` valeur unique d&#39;un jeu de données spécifique. Si vous ne disposez pas de cette valeur, consultez le guide de [la liste des objets](../../catalog/api/list-objects.md) Catalog pour trouver les ID de vos jeux de données existants.

## Rechercher des étiquettes pour un jeu de données {#lookup}

Vous pouvez rechercher les étiquettes d’utilisation des données qui ont été appliquées à un jeu de données existant en faisant une demande GET.

**Format d’API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur unique `id` du jeu de données dont vous souhaitez rechercher les étiquettes. |

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
| `labels` | liste des étiquettes d’utilisation des données qui ont été appliquées au jeu de données. |
| `optionalLabels` | liste de champs individuels au sein du jeu de données auxquels des étiquettes d’utilisation de données sont appliquées. |

## Appliquer des étiquettes à un jeu de données

Vous pouvez créer un ensemble de libellés pour un jeu de données en les fournissant dans la charge utile d’une requête POST ou PUT. L’utilisation de l’une ou l’autre de ces méthodes remplace les étiquettes existantes et les remplace par celles fournies dans la charge utile.

**Format d’API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur unique `id` du jeu de données pour lequel vous créez des étiquettes. |

**Requête**

La demande POST suivante ajoute une série d’étiquettes au jeu de données, ainsi qu’un champ spécifique dans ce jeu de données. Les champs fournis dans la charge utile sont identiques à ceux requis pour une demande de test de performances (PUT).

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
| `labels` | liste d’étiquettes d’utilisation des données que vous souhaitez ajouter au jeu de données. |
| `optionalLabels` | liste de tous les champs individuels du jeu de données auxquels vous souhaitez ajouter des étiquettes. Chaque élément de ce tableau doit avoir les propriétés suivantes : <br/><br/>`option`: Objet contenant les attributs du modèle de données d’expérience (XDM) du champ. Les trois propriétés suivantes sont requises :<ul><li>id</code>: Valeur URI $id</code> du schéma associé au champ.</li><li>contentType</code>: Type de contenu et numéro de version du schéma. Cette opération doit prendre la forme d’un des en-têtes <a href="../../xdm/api/look-up-resource.md"></a> Accepter valides pour une demande de recherche XDM.</li><li>schemaPath</code>: Chemin d’accès au champ dans le schéma du jeu de données.</li></ul>`labels`: liste d’étiquettes d’utilisation des données que vous souhaitez ajouter au champ. |

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

## Suppression d’étiquettes d’un jeu de données

Vous pouvez supprimer les étiquettes appliquées à un jeu de données en exécutant une requête DELETE.

**Format d’API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur unique `id` du jeu de données dont vous souhaitez supprimer les étiquettes. |

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

Réponse réussie : état HTTP 200 (OK), indiquant que les étiquettes ont été supprimées. Vous pouvez [rechercher les étiquettes](#lookup) existantes pour le jeu de données dans un appel distinct pour le confirmer.

## Étapes suivantes

Maintenant que vous avez ajouté des étiquettes d’utilisation des données au niveau du jeu de données et des champs, vous pouvez commencer à assimiler des données dans la plate-forme d’expérience. Pour en savoir plus, début en lisant la documentation [sur l&#39;assimilation des](../../ingestion/home.md)données.

Vous pouvez également désormais définir des stratégies d’utilisation des données en fonction des étiquettes que vous avez appliquées. Pour plus d’informations, voir la présentation [des stratégies d’utilisation des](../policies/overview.md)données.

Pour plus d&#39;informations sur la gestion des jeux de données dans [!DNL Experience Platform], consultez l&#39;aperçu [des jeux de](../../catalog/datasets/overview.md)données.
---
keywords: Experience Platform ; accueil ; rubriques populaires ; api de dataset ; gérer l’utilisation des données ; api d’utilisation des données
solution: Experience Platform
title: 'Gestion des étiquettes d’utilisation des données pour les jeux de données à l’aide d’API '
topic-legacy: developer guide
description: L’API Service de dataset vous permet d’appliquer et de modifier des étiquettes d’utilisation pour les jeux de données. Il fait partie des fonctionnalités de catalogue de données Adobe Experience Platform, mais est distinct de l’API Catalog Service qui gère les métadonnées des jeux de données.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 6%

---

# Gérer les étiquettes d’utilisation des données pour les jeux de données à l’aide d’API

[[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) vous permet d&#39;appliquer et de modifier des étiquettes d&#39;utilisation pour les jeux de données. Il fait partie des fonctionnalités de catalogue de données Adobe Experience Platform, mais est distinct de l&#39;API [!DNL Catalog Service] qui gère les métadonnées des jeux de données.

Ce document explique comment gérer les étiquettes des jeux de données et des champs à l&#39;aide de [!DNL Dataset Service API]. Pour savoir comment gérer les étiquettes d’utilisation des données à l’aide des appels d’API, consultez le [guide de point de terminaison des étiquettes](../api/labels.md) pour le [!DNL Policy Service API].

## Prise en main

Avant de lire ce guide, suivez les étapes décrites dans la section [prise en main](../../catalog/api/getting-started.md) du guide du développeur du catalogue pour rassembler les informations d’identification nécessaires pour appeler les API [!DNL Platform].

Pour invoquer les points de terminaison décrits dans ce document, vous devez disposer de la valeur `id` unique pour un jeu de données spécifique. Si vous ne possédez pas cette valeur, consultez le guide [qui répertorie les objets de catalogue](../../catalog/api/list-objects.md) pour trouver les ID de vos jeux de données existants.

## Rechercher des étiquettes pour un jeu de données {#look-up}

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
| `optionalLabels` | Liste de champs individuels au sein du jeu de données auxquels des étiquettes d’utilisation de données sont appliquées. |

## Appliquer des étiquettes à un jeu de données {#apply}

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

La demande de PUT suivante met à jour les étiquettes existantes pour un jeu de données, ainsi qu’un champ spécifique dans ce jeu de données. Les champs fournis dans la charge utile sont identiques à ceux requis pour une demande de POST.

>[!IMPORTANT]
>
>Un en-tête `If-Match` valide doit être fourni lors de l&#39;exécution de requêtes PUT au point de terminaison `/datasets/{DATASET_ID}/labels`. Pour plus d&#39;informations sur l&#39;utilisation de l&#39;en-tête requis, consultez la section [appendice](#if-match).

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
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
| `optionalLabels` | Liste de tous les champs individuels du jeu de données auxquels vous souhaitez ajouter des étiquettes. Chaque élément de ce tableau doit avoir les propriétés suivantes : <br/><br/>`option` : Objet contenant les attributs [!DNL Experience Data Model] (XDM) du champ. Les trois propriétés suivantes sont requises :<ul><li>id</code>: Valeur URI $id</code> du schéma associé au champ.</li><li>contentType</code>: Type de contenu et numéro de version du schéma. Il doit s’agir de l’un des en-têtes <a href="../../xdm/api/getting-started.md#accept">Accepter</a> valides pour une demande de recherche XDM.</li><li>schemaPath</code>: Chemin d’accès au champ dans le schéma du jeu de données.</li></ul>`labels`: Liste d’étiquettes d’utilisation des données que vous souhaitez ajouter au champ. |

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

## Supprimer des étiquettes d&#39;un jeu de données {#remove}

Vous pouvez supprimer les étiquettes appliquées à un jeu de données en envoyant une requête de DELETE à l&#39;API [!DNL Dataset Service].

**Format d’API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur `id` unique du jeu de données dont vous souhaitez supprimer les étiquettes. |

**Requête**

La demande suivante supprime les étiquettes du jeu de données spécifié dans le chemin d’accès.

>[!IMPORTANT]
>
>Un en-tête `If-Match` valide doit être fourni lors de l&#39;exécution de requêtes DELETE au point de terminaison `/datasets/{DATASET_ID}/labels`. Pour plus d&#39;informations sur l&#39;utilisation de l&#39;en-tête requis, consultez la section [appendice](#if-match).

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**Réponse**

Réponse réussie : état HTTP 200 (OK), indiquant que les étiquettes ont été supprimées. Vous pouvez [rechercher les étiquettes existantes](#look-up) pour le jeu de données dans un appel distinct pour le confirmer.

## Étapes suivantes

En lisant ce document, vous avez appris à gérer les étiquettes d&#39;utilisation des données pour les jeux de données et les champs à l&#39;aide de l&#39;API [!DNL Dataset Service].

Une fois que vous avez ajouté des étiquettes d&#39;utilisation de données au niveau du jeu de données et du champ, vous pouvez commencer à assimiler des données dans [!DNL Experience Platform]. Pour en savoir plus, commencez par lire la [documentation sur l’ingestion de données](../../ingestion/home.md).

Désormais, vous pouvez également définir des stratégies d’utilisation des données en fonction des libellés que vous avez appliqués. Pour plus d’informations, consultez la [présentation des stratégies d’utilisation des données](../policies/overview.md).

Pour plus d&#39;informations sur la gestion des jeux de données dans [!DNL Experience Platform], consultez l&#39;[aperçu des jeux de données](../../catalog/datasets/overview.md).

## Annexe {#appendix}

La section suivante contient des informations supplémentaires sur l’utilisation des étiquettes à l’aide de l’API Service de dataset.

### En-tête [!DNL If-Match]{#if-match}

Lors d’appels d’API mettant à jour les étiquettes existantes d’un jeu de données (PUT et DELETE), un en-tête `If-Match` indiquant la version actuelle de l’entité de libellé de jeu de données dans le service de jeux de données doit être inclus. Afin d’éviter les collisions de données, le service ne mettra à jour l’entité de jeu de données que si la chaîne `If-Match` incluse correspond à la dernière balise de version générée par le système pour ce jeu de données.

>[!NOTE]
>
>S&#39;il n&#39;existe actuellement aucune étiquette pour le jeu de données en question, de nouvelles étiquettes ne peuvent être ajoutées que par le biais d&#39;une demande de POST, qui ne nécessite pas d&#39;en-tête `If-Match`. Une fois que des étiquettes ont été ajoutées à un jeu de données, une valeur `etag` est affectée, qui peut être utilisée pour mettre à jour ou supprimer les étiquettes ultérieurement.

Pour récupérer la version la plus récente de l&#39;entité de libellé de jeu de données, faites une demande de GET [](#look-up) au point de terminaison `/datasets/{DATASET_ID}/labels`. La valeur actuelle est renvoyée dans la réponse sous un en-tête `etag`. Lors de la mise à jour des libellés de jeux de données existants, il est recommandé d&#39;effectuer d&#39;abord une requête de recherche pour le jeu de données afin de récupérer sa dernière valeur `etag` avant d&#39;utiliser cette valeur dans l&#39;en-tête `If-Match` de votre demande de PUT ou de DELETE ultérieure.

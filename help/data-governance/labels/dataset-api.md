---
keywords: Experience Platform;accueil;rubriques populaires;api jeu de données;gestion de lʼutilisation des données;api utilisation des données
solution: Experience Platform
title: Gestion des étiquettes dʼutilisation des données pour les jeux de données à lʼaide dʼAPI
description: LʼAPI Dataset Service vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI Catalog Service qui gère les métadonnées du jeu de données.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 91%

---

# Gestion des étiquettes dʼutilisation des données pour les jeux de données à lʼaide dʼAPI

[[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI [!DNL Catalog Service] qui gère les métadonnées du jeu de données.

>[!IMPORTANT]
>
>L’application d’étiquettes au niveau du jeu de données est uniquement prise en charge pour les cas d’utilisation de la gouvernance des données. Si vous essayez de créer des stratégies d’accès pour les données, vous devez [appliquer des libellés au schéma ;](../../xdm/tutorials/labels.md) sur lequel le jeu de données est basé. Consultez la présentation sur [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md) pour plus d’informations.

Ce document explique la gestion des étiquettes pour les jeux de données et les champs à lʼaide de [!DNL Dataset Service API]. Pour obtenir des instructions sur la gestion des étiquettes dʼutilisation des données elles-mêmes à lʼaide dʼappels API, consultez le [guide de point d’entrée des étiquettes](../api/labels.md) pour [!DNL Policy Service API].

## Prise en main

Avant de lire ce guide, suivez les étapes décrites dans la [section Prise en main](../../catalog/api/getting-started.md) du guide de développement de Catalogue pour rassembler les informations dʼidentification nécessaires afin de réaliser des appels aux API de [!DNL Platform].

Pour réaliser des appels vers les points d’entrée décrits dans ce document, vous devez disposer de la valeur `id` unique pour un jeu de données spécifique. Si vous ne possédez pas cette valeur, consultez le guide qui [répertorie les objets de Catalogue](../../catalog/api/list-objects.md) afin de trouver les identifiants de vos jeux de données existants.

## Recherche dʼétiquettes pour un jeu de données {#look-up}

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
| `optionalLabels` | Liste de champs individuels au sein du jeu de données auxquels sont appliquées des étiquettes dʼutilisation de données. |

## Application dʼétiquettes à un jeu de données {#apply}

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

La requête PUT suivante met à jour les libellés existants pour un jeu de données, ainsi quʼun champ spécifique dans ce jeu de données. Les champs fournis dans la payload sont identiques à ceux requis pour une requête POST. 

Lors dʼappels API mettant à jour les libellés existants dʼun jeu de données (PUT), un en-tête `If-Match` indiquant la version actuelle de lʼentité libellé-jeu de données dans Dataset Service doit être inclus. Afin dʼéviter les collisions de données, le service ne mettra à jour lʼentité jeu de données que si la chaîne `If-Match` incluse correspond à la dernière balise de version générée par le système pour ce jeu de données.

>[!NOTE]
>
>Si aucune étiquette nʼexiste actuellement pour le jeu de données en question, de nouvelles étiquettes ne peuvent être ajoutées que par le biais dʼune requête POST, qui ne nécessite pas un en-tête `If-Match`. Une fois que des étiquettes ont été ajoutées à un jeu de données, une valeur `etag` est attribuée qui peut être utilisée pour mettre à jour ou supprimer les étiquettes ultérieurement.

Pour récupérer la version la plus récente de lʼentité étiquette-jeu de données, envoyez une [requête GET](#look-up) au point d’entrée `/datasets/{DATASET_ID}/labels`. La valeur actuelle est renvoyée dans la réponse sous un en-tête `etag`. Lors de la mise à jour de libellés de jeux de données existants, il est recommandé dʼeffectuer dʼabord une requête de recherche pour le jeu de données afin de récupérer sa valeur `etag` la plus récente avant dʼutiliser cette valeur dans lʼen-tête `If-Match` de votre requête PUT ultérieure. 

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `labels` | Liste dʼétiquettes dʼutilisation des données que vous souhaitez ajouter au jeu de données. |
| `optionalLabels` | Liste de tous les champs individuels dans le jeu de données auxquels vous souhaitez ajouter des étiquettes. Chaque élément de ce tableau doit avoir les propriétés suivantes :<br/><br/>`option`objet contenant les attributs [!DNL Experience Data Model] (XDM) du champ. Les trois propriétés suivantes sont requises :<ul><li>id</code> : valeur URI $id</code> du schéma associé au champ.</li><li>contentType</code> : type de contenu et numéro de version du schéma. Cela doit prendre la forme dʼun des <a href="../../xdm/api/getting-started.md#accept">en-têtes « Accept »</a> valides pour une demande de recherche XDM.</li><li>schemaPath</code> : chemin dʼaccès au champ dans le schéma du jeu de données.</li></ul>`labels` : liste dʼétiquettes dʼutilisation des données que vous souhaitez ajouter au champ. |

**Réponse**

Une réponse réussie renvoie le jeu de libellés mis à jour pour le jeu de données. 

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

## Étapes suivantes

En lisant ce document, vous avez appris la gestion des étiquettes dʼutilisation des données pour les jeux de données et les champs à lʼaide de lʼAPI [!DNL Dataset Service]. Vous pouvez maintenant définir [stratégies d’utilisation des données](../policies/overview.md) et [stratégies de contrôle d’accès](../../access-control/abac/ui/policies.md) selon les libellés que vous avez appliqués.

Pour plus dʼinformations sur la gestion des jeux de données dans [!DNL Experience Platform], consultez la [présentation des jeux de données](../../catalog/datasets/overview.md).

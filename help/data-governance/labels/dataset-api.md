---
keywords: Experience Platform;accueil;rubriques populaires;api jeu de données;gestion de lʼutilisation des données;api utilisation des données
solution: Experience Platform
title: Gestion des étiquettes dʼutilisation des données pour les jeux de données à lʼaide dʼAPI
description: LʼAPI Dataset Service vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI Catalog Service qui gère les métadonnées du jeu de données.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 8db484e4a65516058d701ca972fcbcb6b73abb31
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 93%

---

# Gestion des étiquettes dʼutilisation des données pour les jeux de données à lʼaide dʼAPI

[[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI [!DNL Catalog Service] qui gère les métadonnées du jeu de données.

>[!IMPORTANT]
>
>L’application de libellés au niveau du jeu de données est uniquement prise en charge pour les cas d’utilisation de la gouvernance des données. Si vous essayez de créer des politiques d’accès pour les données, vous devez [appliquer des libellés au schéma](../../xdm/tutorials/labels.md) sur lequel le jeu de données est basé. Consultez la présentation du [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md) pour plus d’informations.

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

## Appliquer des libellés à un jeu de données {#apply}

Vous pouvez appliquer un ensemble de libellés pour un jeu de données entier en les fournissant dans la payload dʼune requête POST ou PUT à lʼAPI [!DNL Dataset Service]. Le corps de la requête est le même pour les deux appels. Vous ne pouvez pas ajouter de libellés à des champs de jeu de données individuels.

**Format d’API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur `id` unique du jeu de données pour lequel vous créez des étiquettes. |

**Requête**

L’exemple de requête POST ci-dessous met à jour l’ensemble du jeu de données avec un libellé `C1`. Les champs fournis dans la payload sont identiques à ceux requis pour une requête PUT.

Lors dʼappels API mettant à jour les libellés existants dʼun jeu de données (PUT), un en-tête `If-Match` indiquant la version actuelle de lʼentité libellé-jeu de données dans Dataset Service doit être inclus. Afin dʼéviter les collisions de données, le service ne mettra à jour lʼentité jeu de données que si la chaîne `If-Match` incluse correspond à la dernière balise de version générée par le système pour ce jeu de données.

>[!NOTE]
>
>Si des libellés existent actuellement pour le jeu de données en question, de nouveaux libellés ne peuvent être ajoutés que par le biais dʼune requête PUT, qui ne nécessite pas d’en-tête `If-Match`. Une fois que des libellés ont été ajoutés à un jeu de données, la valeur `etag` la plus récente est requise pour mettre à jour ou supprimer les libellés ultérieurement<br>Avant d’exécuter la méthode du PUT, vous devez effectuer une requête de GET sur les libellés du jeu de données. Veillez à ne mettre à jour que les champs spécifiques destinés à être modifiés dans la requête, en laissant le reste inchangé. De plus, assurez-vous que l’appel de PUT conserve les mêmes entités parentes que l’appel de GET. Toute incohérence provoquerait une erreur pour le client.

Pour récupérer la version la plus récente de lʼentité étiquette-jeu de données, envoyez une [requête GET](#look-up) au point d’entrée `/datasets/{DATASET_ID}/labels`. La valeur actuelle est renvoyée dans la réponse sous un en-tête `etag`. Lors de la mise à jour de libellés de jeux de données existants, il est recommandé dʼeffectuer dʼabord une requête de recherche pour le jeu de données afin de récupérer sa valeur `etag` la plus récente avant dʼutiliser cette valeur dans lʼen-tête `If-Match` de votre requête PUT ultérieure. 

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": []
      } '
```

| Propriété | Description |
| --- | --- |
| `entityId` | Permet d’identifier l’entité spécifique du jeu de données à mettre à jour. |
| `entityId.namespace` | Permet d’éviter les collisions d’identifiants. L’`namespace` est `AEP`. |
| `entityId.id` | L’identifiant de la ressource mise à jour. Cela fait référence à `datasetId`. |
| `entityId.type` | Le type de ressource mis à jour. Il s’agit toujours de `dataset`. |
| `labels` | Liste de libellés dʼutilisation des données que vous souhaitez ajouter au jeu de données entier. |
| `parents` | Le tableau `parents` contient une liste de `entityId` dont ce jeu de données héritera des libellés. Les jeux de données peuvent hériter des libellés des schémas et/ou des jeux de données. |

**Réponse**

Une réponse réussie renvoie le jeu de libellés mis à jour pour le jeu de données. 

>[!IMPORTANT]
>
>L’utilisation de la propriété `optionalLabels` dans les requêtes POST a été abandonnée. Il n’est plus possible d’ajouter des étiquettes de données aux champs du jeu de données. L’opération POST renvoie une erreur si une valeur `optionalLabel` est présente. Cependant, vous pouvez supprimer des libellés de champs individuels à l’aide d’une requête PUT et de la propriété `optionalLabels`. Pour plus d’informations, consultez la section consacrée à la [suppression de libellés d’un jeu de données](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## Suppression des étiquettes dʼun jeu de données {#remove}

Pour supprimer des libellés du champ précédemment appliqués, mettez à jour la ou les valeurs `optionalLabels` existantes avec un sous-ensemble des libellés du champ existants ou une liste vide pour les supprimer entièrement. Envoyez une requête PUT à l’API [!DNL Dataset Service] pour mettre à jour ou supprimer les libellés précédemment appliqués.

**Format d’API**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Valeur `id` unique du jeu de données pour lequel vous créez des étiquettes. |

**Requête**

Dans le jeu de données ci-dessous sur lequel l’opération PUT est appliquée, le paramètre optionalLabel possède la valeur C1 dans le champ propriétés/personne/propriétés/addresse et le paramètre optionalLabels possède les valeurs C1 et C2 dans le champ /propriétés/personne/propriétés/nom/propriétés/NomComplet. Suite à l’opération PUT, le premier champ n’a pas de libellé (le libellé C1 a été supprimé) et le second champ n’a qu’un libellé C1 (le libellé C2 a été supprimé).

Dans l’exemple de scénario ci-dessous, une requête PUT est envoyée pour supprimer les libellés ajoutés à des champs individuels. Avant que la demande ne soit effectuée, le champ `fullName` disposait des libellés `C1` et `C2` et le champ `address` possédait déjà un libellé `C1`. La requête PUT remplace les libellés `C1, C2` existants du champ `fullName` par un libellé `C1` à l’aide du paramètre `optionalLabels.labels`. La requête remplace également le libellé `C1` du champ `address` par un ensemble vide de libellés de champ.

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
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| Paramètre | Description |
| --- | --- |
| `entityId` | Permet d’identifier l’entité spécifique du jeu de données à mettre à jour. Le paramètre `entityId` doit inclure les trois valeurs suivantes : <br/><br/>`namespace` : permet d’éviter les collisions d’identifiants. La valeur de `namespace` est `AEP`.<br/>`id` : l’identifiant de la ressource mise à jour. Fait référence au paramètre `datasetId`.<br/>`type` : le type de ressource mise à jour. Il s’agit toujours de `dataset`. |
| `labels` | Liste de libellés dʼutilisation des données que vous souhaitez ajouter au jeu de données entier. |
| `parents` | Le tableau `parents` contient une liste de `entityId` dont ce jeu de données héritera des libellés. Les jeux de données peuvent hériter des libellés des schémas et/ou des jeux de données. |
| `optionalLabels` | Ce paramètre permet de supprimer les libellés précédemment appliqués à un champ de jeu de données. Liste de tous les champs individuels dans le jeu de données desquels vous souhaitez supprimer des libellés. Chaque élément de ce tableau doit avoir les propriétés suivantes :<br/><br/>`option`objet contenant les attributs [!DNL Experience Data Model] (XDM) du champ. Les trois propriétés suivantes sont requises :<ul><li><code>identifiant</code>: la valeur URI <code>$id</code> du schéma associé au champ.</li><li><code>contentType</code> : type de contenu et numéro de version du schéma. Cela doit prendre la forme dʼun des <a href="../../xdm/api/getting-started.md#accept">en-têtes « Accept »</a> valides pour une demande de recherche XDM.</li><li><code>schemaPath</code> : chemin dʼaccès au champ dans le schéma du jeu de données.</li></ul>`labels` : cette valeur doit contenir un sous-ensemble des libellés de champ existants appliqués ou être vide pour supprimer tous les libellés de champ existants. Les méthodes de PUT ou de POST renvoient désormais une erreur si le champ `optionalLabels` contient des libellés nouveaux ou modifiés. |

**Réponse**

Une réponse réussie renvoie le jeu de libellés mis à jour pour le jeu de données. 

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## Étapes suivantes

En lisant ce document, vous avez appris la gestion des libellés dʼutilisation des données pour les jeux de données et les champs à lʼaide de lʼAPI [!DNL Dataset Service]. Vous pouvez maintenant définir les [politiques d’utilisation des données](../policies/overview.md) et les [politiques de contrôle d’accès](../../access-control/abac/ui/policies.md) selon les libellés que vous avez appliqués.

Pour plus dʼinformations sur la gestion des jeux de données dans [!DNL Experience Platform], consultez la [présentation des jeux de données](../../catalog/datasets/overview.md).

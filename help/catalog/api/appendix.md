---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de catalogue;api de catalogue;annexe
solution: Experience Platform
title: Annexe du guide de l’API Catalog Service
description: Ce document contient des informations supplémentaires pour vous aider à utiliser l’API Catalog dans Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 76%

---

# [!DNL Catalog Service] annexe du guide de l’API

Ce document contient des informations supplémentaires pour vous aider à travailler avec l’API [!DNL Catalog].

## Affichage d’objets interconnectés {#view-interrelated-objects}

Certains objets [!DNL Catalog] peuvent être interconnectés avec d’autres objets [!DNL Catalog]. Tout champ précédé du préfixe `@` dans les payloads de réponse indique les objets associés. Les valeurs de ces champs prennent la forme d’un URI qui peut être utilisé dans une requête GET distincte pour récupérer les objets associés qu’ils représentent.

L’exemple de jeu de données renvoyé dans le document sur la [recherche d’un jeu de données spécifique](look-up-object.md) contient un champ `files` avec la valeur URI suivante : `"@/datasetFiles?datasetId={DATASET_ID}"`. Le contenu du champ `files` peut être visualisé en utilisant cet URI comme chemin d’accès à une nouvelle requête GET.

**Format d’API**

```http
GET {OBJECT_URI}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_URI}` | L’URI fourni par le champ d’objet interconnecté (hors symbole `@`). |

**Requête**

La requête suivante utilise l’URI fourni dans la propriété `files` de l’exemple de jeu de données pour récupérer une liste des fichiers associés au jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’objets associés. Dans cet exemple, une liste de fichiers de jeux de données est renvoyé.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## En-têtes de requête supplémentaires

[!DNL Catalog] fournit plusieurs conventions d’en-tête pour vous aider à maintenir l’intégrité de vos données lors des mises à jour.

### If-Match

Il est recommandé d’utiliser le contrôle de version d’objet pour éviter le type de corruption de données qui se produit lorsqu’un objet est enregistré presque simultanément par plusieurs utilisateurs.

Lors de la mise à jour d’un objet, il est recommandé d’effectuer d’abord un appel API pour afficher (GET) l’objet à mettre à jour. Un en-tête `E-Tag` contenant la version de l’objet est contenu dans la réponse (et dans tout appel de réponse contenant un objet unique). L’ajout de la version d’objet en tant qu’en-tête de requête nommé `If-Match` dans vos appels de mise à jour (PUT ou PATCH) entraîne la réussite de la mise à jour seulement si la version est toujours la même, ce qui permet d’éviter les collisions de données.

Si les versions ne correspondent pas (l’objet a été modifié par un autre processus depuis que vous l’avez récupéré), vous recevrez un état HTTP 412 (Precondition Failed) indiquant que l’accès à la ressource cible a été refusé.

### Pragma

Il peut arriver que vous souhaitiez valider un objet sans enregistrer les informations. L’utilisation de l’en-tête `Pragma` avec la valeur `validate-only` permet d’envoyer des requêtes POST ou PUT à des fins de validation uniquement, ce qui empêche la persistance de toute modification des données.

## Compactage des données

Compaction est un service [!DNL Experience Platform] qui fusionne les données de petits fichiers en fichiers plus volumineux sans modifier les données. Pour des raisons de performances, il est parfois bénéfique de combiner un ensemble de petits fichiers en fichiers plus volumineux afin de fournir un accès plus rapide aux données lors de l’interrogation.

Lorsque les fichiers d’un lot ingéré ont été compactés, son objet [!DNL Catalog] associé est mis à jour à des fins de surveillance.

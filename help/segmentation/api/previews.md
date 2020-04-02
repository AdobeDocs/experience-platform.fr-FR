---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Previews
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Guide du développeur des 

intro

- Création d’un  de
- Récupération de résultats  d’un spécifique
- Annuler ou supprimer un spécifique 

## Prise en main

Les points de fin d’API utilisés dans ce guide font partie de l’API de segmentation. Avant de poursuivre, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [de](./getting-started.md#getting-started) prise en main du guide du développeur de segmentation comprend des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le  du et des informations importantes concernant les en-têtes requis nécessaires pour effectuer des appels à une API de plateforme d’expérience.

## Création d’un  de

Vous pouvez créer un nouveau  en envoyant une requête POST au point de `/preview` fin.

**Format API**

```http
POST /preview
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

body info

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) avec les détails de votre  nouvellement créé.

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

information de réponse, x-location n’existe pas.

## Récupération de résultats  d’un spécifique

Vous pouvez récupérer des informations détaillées sur un spécifique en envoyant une requête GET au point de `/preview` `id` fin et en indiquant la valeur de l’ de dans le chemin d’accès à la requête.

**Format API**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: La `id` valeur du à récupérer.

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur le  spécifié.

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## Annuler ou supprimer un spécifique 

Vous pouvez supprimer un spécifique en faisant une requête DELETE au point de `/preview` `id` fin et en fournissant la valeur de  de dans le chemin d’accès de la requête.

**Format API**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` La `id` valeur du à supprimer.

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec le message suivant :

```json
{
  "status": true,
  "message": "KILLED"
}
```

## Étapes suivantes

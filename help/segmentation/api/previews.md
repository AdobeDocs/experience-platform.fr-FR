---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Prévisualisations
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---


# Guide du développeur de Prévisualisations

intro

- Créer une prévisualisation
- Récupération de résultats spécifiques à une prévisualisation
- Annuler ou supprimer une prévisualisation spécifique

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API de segmentation. Avant de continuer, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [Prise en main de la](./getting-started.md#getting-started) sectiondu guide du développeur de segmentation contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API de plateforme d’expérience.

## Créer une prévisualisation

Vous pouvez créer une prévisualisation en envoyant une requête POST au point de `/preview` terminaison.

**Format d’API**

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

Une réponse réussie renvoie l’état HTTP 201 (Créé) avec les détails de votre nouvelle prévisualisation créée.

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

information de réponse, x-location n&#39;existe pas.

## Récupération de résultats spécifiques à une prévisualisation

Vous pouvez récupérer des informations détaillées sur une prévisualisation spécifique en envoyant une requête GET au point de `/preview` terminaison et en indiquant la valeur de la prévisualisation `id` dans le chemin de la requête.

**Format d’API**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: Valeur `id` de la prévisualisation à récupérer.

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur la prévisualisation spécifiée.

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

## Annuler ou supprimer une prévisualisation spécifique

Vous pouvez supprimer une prévisualisation spécifique en envoyant une requête DELETE au point de `/preview` terminaison et en indiquant la valeur de la prévisualisation `id` dans le chemin de la requête.

**Format d’API**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` Valeur `id` de la prévisualisation à supprimer.

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

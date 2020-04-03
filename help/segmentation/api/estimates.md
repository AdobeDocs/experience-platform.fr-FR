---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Estimations
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# Estimations

intro

- Récupérer les résultats d’une tâche d’estimation spécifique

## Prise en main

Les points de fin d’API utilisés dans ce guide font partie de l’API de segmentation. Avant de poursuivre, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [de](./getting-started.md#getting-started) prise en main du guide du développeur de segmentation comprend des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le  du et des informations importantes concernant les en-têtes requis nécessaires pour effectuer des appels à une API de plateforme d’expérience.

## Récupérer les résultats d’une tâche d’estimation spécifique

Vous pouvez récupérer les détails d’une tâche d’estimation spécifique en envoyant une requête GET au point de `/estimate` fin et en indiquant la `id` valeur de la tâche d’estimation dans le chemin de requête.

**Format API**

```http
GET /estimate/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: La `id` valeur de la tâche d’estimation que vous souhaitez récupérer.

**Requête**

La requête suivante récupère les résultats d’une tâche d’estimation spécifique.

//Besoin d&#39;obtenir un ID de 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/{PREVIEW_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails de la tâche d’estimation.

```json
{
  "estimatedSize": 0,
  "numRowsToRead": 1,
  "state": "RESULT_READY",
  "profilesReadSoFar": 1,
  "standardError": 0,
  "error": {
    "description": "",
    "traceback": ""
  },
  "profilesMatchedSoFar": 0,
  "totalRows": 1,
  "confidenceInterval": "95%",
  "_links": {
    "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
  }
}
```

## Étapes suivantes

Maintenant que vous savez comment récupérer les résultats des tâches d&#39;estimation, vous pouvez mieux
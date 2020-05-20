---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Estimations
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---


# Estimations

intro

- Récupérer les résultats d&#39;une tâche d&#39;estimation spécifique

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API de segmentation. Avant de continuer, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [Prise en main de la](./getting-started.md#getting-started) sectiondu guide du développeur de segmentation contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API de plateforme d’expérience.

## Récupérer les résultats d&#39;une tâche d&#39;estimation spécifique

Vous pouvez récupérer les détails d’une tâche d’estimation spécifique en envoyant une requête GET au point de `/estimate` terminaison et en indiquant la `id` valeur de la tâche d’estimation dans le chemin de requête.

**Format d’API**

```http
GET /estimate/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: La `id` valeur de la tâche d&#39;estimation que vous souhaitez récupérer.

**Requête**

La requête suivante récupère les résultats d&#39;une tâche d&#39;estimation spécifique.

//besoin d&#39;obtenir un ID de prévisualisation

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

Maintenant que vous savez comment récupérer les résultats d&#39;estimation des tâches, vous pouvez mieux
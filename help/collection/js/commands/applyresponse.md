---
title: applyResponse
description: Utiliser une réponse d'Edge Network pour initialiser le SDK Web.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

La commande `applyResponse` vous permet d’effectuer différentes actions en fonction d’une réponse d’Edge Network. Il est généralement utilisé dans les déploiements hybrides où le serveur effectue un appel initial à l’Edge Network. Cette commande prend la réponse de cet appel et initialise le SDK Web dans le navigateur.

Exécutez la commande `applyResponse` lors de l’appel de votre instance configurée de Web SDK. L’objet contenant les options de configuration prend en charge les champs suivants :

* **`renderDecisions`** : une valeur booléenne qui force le SDK Web à effectuer le rendu de tout contenu personnalisé éligible au rendu automatique. Identique à [`renderDecisions`](sendevent/renderdecisions.md) dans la commande [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`** : mappage des noms des en-têtes de chaîne aux valeurs des en-têtes de chaîne.
* **`responseBody`** : obligatoire. Un corps de réponse JSON de l’appel au serveur vers Edge Network.
* **`personalization.sendDisplayEvent`** : une valeur booléenne qui fonctionne de manière identique à [`personalization.sendDisplayEvent`](sendevent/personalization.md) dans la commande `sendEvent`.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`propositions`** : tableau de propositions renvoyé par l’Edge Network. Les propositions dont le rendu est automatique incluent l’indicateur `renderAttempted` défini sur `true`.
* **`inferences`** : tableau d’objets d’inférence contenant des informations de machine learning sur cet utilisateur.
* **`destinations`** : tableau d’objets de destination renvoyés par Edge Network.

## Application d’une réponse à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente à cette commande est l’action [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md).

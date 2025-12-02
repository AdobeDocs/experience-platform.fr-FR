---
title: sendEvent
description: Envoyez les données à Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

La commande `sendEvent` est la principale méthode d’envoi de données à Adobe. Son objet de réponse est le principal moyen de récupérer du contenu personnalisé, des identités et des destinations d’audience. Utilisez l’objet [`xdm`](xdm.md) pour envoyer des données qui correspondent à votre schéma Adobe Experience Platform. Utilisez l’objet [`data`](data.md) pour envoyer des données non XDM. La limite maximale de la payload lors de l’envoi de données à Adobe est de 64 Ko.

Exécutez la commande `sendEvent` lors de l’appel de votre instance configurée de Web SDK. Veillez à appeler la commande [`configure`](../configure/overview.md) avant d&#39;appeler la commande `sendEvent`.

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](../command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`propositions`** : tableau de propositions renvoyé par l’Edge Network. Les propositions dont le rendu est automatique incluent l’indicateur `renderAttempted` défini sur `true`.
* **`inferences`** : tableau d’objets d’inférence contenant des informations de machine learning sur cet utilisateur.
* **`destinations`** : tableau d’objets de destination renvoyés par Edge Network.

## Envoi d’un événement à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente à cette commande est l’action [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields).

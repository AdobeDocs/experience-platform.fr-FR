---
title: sendEvent
description: Envoyez les données à Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
TQID: https://experienceleague.adobe.com/47eXICo3e7d2v3Qge6kjRYGA0wRgOnYSCK0uRNrM3AU
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: eadea719-cf89-469b-a6fd-a236a7138047id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 179
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

L’extension de balise Web SDK équivalente à cette commande est l’action [**[!UICONTROL Envoyer l’événement]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields).

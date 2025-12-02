---
title: Gestion des réponses aux commandes
description: Gérez les réponses des commandes à l’aide des promesses JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Gestion des réponses aux commandes

Certaines commandes Web SDK peuvent renvoyer un objet contenant des données potentiellement utiles à votre organisation. Vous pouvez choisir l’utilisation de ces données, si vous le souhaitez. Les réponses des commandes sont utiles pour les propositions et les destinations, car elles nécessitent des données Edge Network pour fonctionner efficacement.

Les réponses de commande utilisent JavaScript [promesses](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise), agissant comme proxy pour une valeur qui n’est pas connue lors de la création de la promesse. Une fois la valeur connue, la promesse est « résolue » avec la valeur .

Utilisez les méthodes `then` et `catch` pour déterminer le moment où une commande réussit ou échoue. Vous pouvez omettre les `then` ou les `catch` si leurs objectifs ne sont pas importants pour votre implémentation.

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

Toutes les promesses renvoyées par les commandes utilisent un objet `result`. Par exemple, vous pouvez obtenir des informations sur la bibliothèque à partir de l’objet `result` à l’aide de la commande [`getLibraryInfo`](getlibraryinfo.md) :

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Le contenu de cet objet `result` dépend de la combinaison de la commande que vous utilisez et du consentement de l’utilisateur. Si un utilisateur n’a pas donné son consentement à une fin particulière, l’objet de réponse contient uniquement des informations qui peuvent être fournies dans le contexte de ce à quoi l’utilisateur a consenti.

## Réponses aux commandes utilisant l’extension de balise Web SDK

L’extension de balise Web SDK équivalente aux réponses de commande est une règle qui s’abonne à l’événement [**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete). Vous pouvez ensuite inclure des actions telles que des [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) ou des [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) à cette règle.

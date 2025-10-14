---
title: Gestion des réponses de commande
description: Gérez les réponses à partir de commandes à l’aide de promesses JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Gestion des réponses de commande

Certaines commandes du SDK Web peuvent renvoyer un objet contenant des données potentiellement utiles à votre entreprise. Si vous le souhaitez, vous pouvez choisir ce que vous souhaitez faire avec ces données. Les réponses de commande sont utiles pour les propositions et les destinations, car elles nécessitent des données Edge Network pour fonctionner efficacement.

Les réponses de commande utilisent JavaScript [&#x200B; &lbrace;promesses](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise), agissant comme un proxy pour une valeur inconnue lors de la création de la promesse. Une fois la valeur connue, la promesse est &quot;résolue&quot; avec la valeur .

## Gestion des réponses de commande à l’aide de l’extension de balise SDK Web

Créez une règle qui s’abonne à l’événement **[!UICONTROL Send event complete]** dans le cadre d’une règle.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Events], sélectionnez un événement existant ou créez un événement.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’événement] sur **[!UICONTROL Envoyer l’événement terminé]**.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

Vous pouvez ensuite inclure les actions **[!UICONTROL Appliquer les propositions]** ou **[!UICONTROL Appliquer la réponse]** à cette règle.

1. Lors de l’affichage de la règle créée ou modifiée ci-dessus, sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Appliquer les propositions]** ou **[!UICONTROL Appliquer la réponse]**, en fonction du comportement souhaité.
1. Définissez les champs de votre choix, puis cliquez sur **[!UICONTROL Conserver les modifications]**.

## Gestion des réponses de commande à l’aide de la bibliothèque JavaScript SDK Web

Utilisez les méthodes `then` et `catch` pour déterminer quand une commande réussit ou échoue. Vous pouvez omettre `then` ou `catch` si leurs objectifs ne sont pas importants pour votre mise en oeuvre.

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

Toutes les promesses renvoyées par les commandes utilisent un objet `result`. Par exemple, vous pouvez obtenir des informations sur la bibliothèque de l’objet `result` à l’aide de la commande [`getLibraryInfo`](getlibraryinfo.md) :

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Le contenu de cet objet `result` dépend d’une combinaison de la commande que vous utilisez et du consentement de l’utilisateur. Si un utilisateur n’a pas donné son consentement dans un but particulier, l’objet de réponse contient uniquement des informations qui peuvent être fournies dans le contexte de ce à quoi l’utilisateur a consenti.

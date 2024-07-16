---
title: onBeforeEventSend
description: Découvrez comment configurer le SDK Web pour enregistrer une fonction JavaScript qui peut modifier les données que vous envoyez juste avant l’envoi de ces données à Adobe.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# `onBeforeEventSend`

Le rappel `onBeforeEventSend` vous permet d’enregistrer une fonction JavaScript qui peut modifier les données que vous envoyez juste avant l’envoi de ces données à Adobe. Ce rappel vous permet de manipuler l’objet `xdm` ou `data`, y compris la possibilité d’ajouter, de modifier ou de supprimer des éléments. Vous pouvez également annuler de manière conditionnelle l’envoi de données, par exemple avec le trafic de robots côté client détecté.

>[!WARNING]
>
>Ce rappel permet l’utilisation de code personnalisé. Si un code que vous incluez dans le rappel renvoie une exception non interceptée, le traitement de l’événement est interrompu. Les données ne sont pas envoyées à Adobe.

## Configurez avant le rappel de l’envoi des événements à l’aide de l’extension de balise SDK Web. {#tag-extension}

Sélectionnez le bouton **[!UICONTROL Fournir avant l’envoi de l’événement le code de rappel]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Ce bouton ouvre une fenêtre modale dans laquelle vous pouvez insérer le code de votre choix.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Collecte de données], puis sélectionnez le bouton **[!UICONTROL Fournir avant le code de rappel d’envoi d’événement]**.
1. Ce bouton ouvre une fenêtre modale avec un éditeur de code. Insérez le code de votre choix, puis cliquez sur **[!UICONTROL Enregistrer]** pour fermer la fenêtre modale.
1. Cliquez sur **[!UICONTROL Enregistrer]** sous les paramètres d’extension, puis publiez vos modifications.

Dans l’éditeur de code, vous avez accès aux variables suivantes :

* **`content.xdm`** : charge utile [XDM](../sendevent/xdm.md) pour l’événement.
* **`content.data`** : charge utile de l’objet [data](../sendevent/data.md) pour l’événement.
* **`return true`** : Quittez immédiatement le rappel et envoyez les données à l’Adobe avec les valeurs actuelles dans l’objet `content`.
* **`return false`** : Quittez immédiatement le rappel et abandonnez l’envoi de données à Adobe.

Toutes les variables définies en dehors de `content` peuvent être utilisées, mais ne sont pas incluses dans la payload envoyée à Adobe.

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Évitez de renvoyer `false` lors du premier événement sur une page. Le renvoi de `false` au premier événement peut avoir une incidence négative sur la personnalisation.

## Configurez avant le rappel de l’envoi d’événement à l’aide de la bibliothèque JavaScript du SDK Web {#library}

Enregistrez le rappel `onBeforeEventSend` lors de l’exécution de la commande `configure`. Vous pouvez remplacer le nom de la variable `content` par toute valeur souhaitée en modifiant la variable de paramètre dans la fonction intégrée.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

Vous pouvez également enregistrer votre propre fonction au lieu d’une fonction intégrée.

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```

---
title: onBeforeEventSend
description: Rappel qui s’exécute juste avant l’envoi des données.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# `onBeforeEventSend`

La variable `onBeforeEventSend` callback vous permet d’enregistrer une fonction JavaScript qui peut modifier les données que vous envoyez juste avant que les données ne soient envoyées à Adobe. Ce rappel vous permet de manipuler la variable `xdm` ou `data` , y compris la possibilité d’ajouter, de modifier ou de supprimer des éléments. Vous pouvez également annuler de manière conditionnelle l’envoi de données, par exemple avec le trafic de robots côté client détecté.

>[!WARNING]
>
>Ce rappel permet l’utilisation de code personnalisé. Si un code que vous incluez dans le rappel renvoie une exception non interceptée, le traitement de l’événement est interrompu. Les données ne sont pas envoyées à Adobe.

## Activé avant le rappel de l’envoi d’événement à l’aide de l’extension de balise SDK Web

Sélectionnez la variable **[!UICONTROL Fournir avant le code de rappel d’envoi d’événement]** lorsque [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Ce bouton ouvre une fenêtre modale dans laquelle vous pouvez insérer le code de votre choix.

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Collecte de données] , puis cliquez sur le bouton **[!UICONTROL Fournir avant le code de rappel d’envoi d’événement]**.
1. Ce bouton ouvre une fenêtre modale avec un éditeur de code. Insérez le code souhaité, puis cliquez sur **[!UICONTROL Enregistrer]** pour fermer la fenêtre modale.
1. Cliquez sur **[!UICONTROL Enregistrer]** sous paramètres d’extension, puis publiez vos modifications.

Dans l’éditeur de code, vous pouvez ajouter, modifier ou supprimer des éléments dans le `content` . Cet objet contient la payload envoyée à Adobe. Vous n’avez pas besoin de définir la variable `content` ou placer tout code dans une fonction. Toute variable définie en dehors de `content` peuvent être utilisées, mais ne sont pas incluses dans la payload envoyée à Adobe.

>[!TIP]
>
>Les objets `content.xdm` et `content.data` sont toujours définis dans ce contexte. Il n’est donc pas nécessaire de vérifier s’ils existent. Certaines variables de ces objets dépendent de votre mise en oeuvre et de votre couche de données. Adobe recommande de rechercher les valeurs non définies dans ces objets afin d’éviter les erreurs JavaScript.

Par exemple, si vous souhaitez :

* Ajout de l’élément XDM `xdm.commerce.order.purchaseID`
* Forcer tous les caractères dans `xdm.marketing.trackingCode` en minuscules
* Supprimez `xdm.environment.operatingSystemVersion`.
* Si un type d’événement est un clic sur les liens, envoyez immédiatement des données, quel que soit le code sous-jacent.
* Annuler l’envoi des données à Adobe si un robot est détecté

Le code équivalent dans la fenêtre modale serait le suivant :

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

>[!NOTE]
>
>Éviter le renvoi `false` lors du premier événement d’une page. Renvoi `false` le premier événement peut avoir un impact négatif sur la personnalisation.

## Activé avant le rappel de l’envoi d’événement à l’aide de la bibliothèque JavaScript du SDK Web

Enregistrez le `onBeforeEventSend` rappel lors de l’exécution de la fonction `configure` . Vous pouvez modifier la variable `content` nom de la variable à n’importe quelle valeur en modifiant la variable de paramètre dans la fonction intégrée.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```

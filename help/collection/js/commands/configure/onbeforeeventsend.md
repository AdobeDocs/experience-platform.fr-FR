---
title: onBeforeEventSend
description: Découvrez comment configurer Web SDK pour enregistrer une fonction JavaScript qui peut modifier les données que vous envoyez juste avant que ces données ne soient envoyées à Adobe.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
TQID: https://experienceleague.adobe.com/v-IDNkSGDKx7Bkv8ciUc5pf3bELnfGAFoWp7m6ofdu4
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 190
ht-degree: 0%

---

# `onBeforeEventSend`

Le rappel `onBeforeEventSend` vous permet d’enregistrer une fonction JavaScript qui peut modifier les données que vous envoyez juste avant que ces données ne soient envoyées à Adobe. Ce rappel vous permet de manipuler l’objet `xdm` ou `data`, notamment d’ajouter, de modifier ou de supprimer des éléments. Vous pouvez également annuler de manière conditionnelle l’envoi de données, par exemple avec le trafic de robots côté client détecté.

>[!WARNING]
>
>Ce rappel permet d’utiliser du code personnalisé. Si un code que vous incluez dans le rappel renvoie une exception non interceptée, le traitement de l’événement s’arrête et **les données ne sont pas envoyées à Adobe.**

Enregistrez le rappel `onBeforeEventSend` lors de l’exécution de la commande `configure`. Vous pouvez remplacer le nom de la variable `content` par n’importe quelle valeur en modifiant la variable de paramètre dans la fonction intégrée.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```

## Configuration de sur avant le rappel d’envoi d’événement à l’aide de l’extension de balise Web SDK

Ces paramètres peuvent être configurés dans l’extension de balise Web SDK à l’aide des [&#x200B; Paramètres de configuration de la collecte de données &#x200B;](/help/tags/extensions/client/web-sdk/configure/data-collection.md#on-before-event-send-callback).

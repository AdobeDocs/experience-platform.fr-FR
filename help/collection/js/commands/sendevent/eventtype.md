---
title: eventType
description: Définissez le type d’événement pour un appel sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

La propriété `eventType` vous permet de définir le type d’événement que vous envoyez à l’aide du SDK Web. Ce champ renseigne finalement le champ `xdm.eventType`. Il s’avère utile lorsque vous souhaitez différencier les types d’événements que vous envoyez à Adobe.

Adobe fournit certains types d’événements prédéfinis que vous pouvez utiliser. Consultez [ Valeurs disponibles pour `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) dans le guide d’utilisation XDM pour obtenir une liste complète des valeurs prédéfinies. Vous pouvez également utiliser vos propres valeurs si vous le souhaitez.

Si vous définissez les deux `type` ici et `xdm.eventType` dans l’objet [`xdm`](xdm.md), la valeur de ce champ est prioritaire.

Définissez la propriété de chaîne `eventType` lors de l’exécution de la commande `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## Type d’événement utilisant l’extension de balise Web SDK

L’équivalent de l’extension de balise Web SDK de cette propriété est le menu déroulant [**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) lors de la configuration d’une action « [!UICONTROL Send event] ».

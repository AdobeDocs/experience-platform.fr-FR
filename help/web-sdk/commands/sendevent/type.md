---
title: eventType
description: Définissez le type d’événement pour un appel sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

La propriété `eventType` vous permet de définir le type d’événement que vous envoyez à l’aide du SDK Web. Ce champ renseigne finalement le champ `xdm.eventType`. Il est utile lorsque vous souhaitez différencier les types d’événements que vous envoyez à Adobe.

Adobe fournit certains types d’événements prédéfinis que vous pouvez utiliser. Voir [Valeurs disponibles pour `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) dans le guide d’utilisation XDM pour obtenir une liste complète des valeurs prédéfinies. Vous pouvez également utiliser vos propres valeurs si vous le souhaitez.

Si vous définissez `type` ici et `xdm.eventType` dans l’objet [`xdm`](xdm.md), la valeur de ce champ est prioritaire.

## Configuration du type d’événement à l’aide de l’extension de balise SDK Web

Définissez le champ déroulant **[!UICONTROL Type]** dans les actions d’une règle de balise.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Envoyer l’événement]**.
1. Utilisez la liste déroulante sous le champ **[!UICONTROL Type]** ou saisissez votre propre valeur.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

## Configuration du type d’événement à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la propriété de chaîne `eventType` lors de l’exécution de la commande `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

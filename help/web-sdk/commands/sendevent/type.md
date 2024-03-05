---
title: eventType
description: Définissez le type d’événement pour un appel sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

La variable `eventType` vous permet de définir le type d’événement que vous envoyez à l’aide du SDK Web. Ce champ renseigne finalement la variable `xdm.eventType` champ . Il est utile lorsque vous souhaitez différencier les types d’événements que vous envoyez à Adobe.

Adobe fournit certains types d’événements prédéfinis que vous pouvez utiliser. Voir [Valeurs disponibles pour `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) dans le guide d’utilisation XDM pour obtenir une liste complète des valeurs prédéfinies. Vous pouvez également utiliser vos propres valeurs si vous le souhaitez.

Si vous définissez les `type` ici et `xdm.eventType` dans le [`xdm`](xdm.md) , la valeur de ce champ est prioritaire.

## Configuration du type d’événement à l’aide de l’extension de balise SDK Web

Définissez la variable **[!UICONTROL Type]** de la liste déroulante dans les actions d’une règle de balise.

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Envoyer un événement]**.
1. Utilisez le menu déroulant sous le **[!UICONTROL Type]** ou saisissez votre propre valeur.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

## Configuration du type d’événement à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `eventType` propriété de chaîne lors de l’exécution de la propriété `sendEvent` .

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

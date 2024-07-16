---
title: sendEvent
description: Envoyez des données à l’Edge Network Adobe Experience Platform.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `sendEvent`

La commande `sendEvent` est le principal moyen d’envoyer des données à Adobe, afin de récupérer du contenu personnalisé, des identités et des destinations d’audience. Utilisez l’objet [`xdm`](xdm.md) pour envoyer des données qui correspondent à votre schéma Adobe Experience Platform. Utilisez l’objet [`data`](data.md) pour envoyer des données non XDM. Vous pouvez utiliser le mappeur de flux de données pour aligner les données de cet objet sur les champs de schéma.

## Envoi de données d’événement à l’aide de l’extension de balise SDK Web

L’envoi de données d’événement est effectué sous la forme d’une action au sein d’une règle dans l’interface des balises de collecte de données Adobe Experience Platform.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Envoyer l’événement]**.
1. Définissez les champs de votre choix, cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

## Envoi de données d’événement à l’aide de la bibliothèque JavaScript du SDK Web

Exécutez la commande `sendEvent` lors de l’appel de votre instance configurée du SDK Web. Assurez-vous d’appeler la commande [`configure`](../configure/overview.md) avant d’appeler la commande `sendEvent`.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](../command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`propositions`** : un tableau de propositions renvoyé par l’Edge Network. Les propositions automatiquement rendues incluent l’indicateur `renderAttempted` défini sur `true`.
* **`inferences`** : un tableau d’objets inférences, qui contient des informations d’apprentissage automatique sur cet utilisateur.
* **`destinations`** : un tableau d’objets de destination renvoyés par l’Edge Network.

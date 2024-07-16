---
title: applyResponse
description: Utilisez une réponse de l’Edge Network pour initialiser le SDK Web.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

La commande `applyResponse` vous permet d’effectuer diverses actions en fonction d’une réponse de l’Edge Network. Il est généralement utilisé dans les déploiements hybrides où le serveur effectue un appel initial vers l’Edge Network. Cette commande récupère la réponse de cet appel et initialise le SDK Web dans le navigateur.

## Application d’une réponse à l’aide de l’extension de balise SDK Web

L’application des réponses est effectuée sous la forme d’une action au sein d’une règle dans l’interface des balises de collecte de données Adobe Experience Platform.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Appliquer la réponse]**.
1. Définissez les champs de votre choix à droite.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

## Application d’une réponse à l’aide de la bibliothèque JavaScript SDK Web

Exécutez la commande `applyResponse` lors de l’appel de votre instance configurée du SDK Web. L’objet contenant des options de configuration prend en charge les champs suivants :

* **`renderDecisions`** : valeur booléenne qui force le SDK Web à effectuer le rendu de tout contenu personnalisé éligible au rendu automatique. Identique à [`renderDecisions`](sendevent/renderdecisions.md) dans la commande [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`** : mappage des noms d’en-tête de chaîne aux valeurs d’en-tête de chaîne.
* **`responseBody`** : obligatoire. Corps de réponse JSON de l’appel du serveur à l’Edge Network.
* **`personalization.sendDisplayEvent`** : valeur booléenne qui fonctionne de manière identique à [`personalization.sendDisplayEvent`](sendevent/personalization.md) dans la commande `sendEvent`.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`propositions`** : un tableau de propositions renvoyé par l’Edge Network. Les propositions automatiquement rendues incluent l’indicateur `renderAttempted` défini sur `true`.
* **`inferences`** : un tableau d’objets inférences, qui contient des informations d’apprentissage automatique sur cet utilisateur.
* **`destinations`** : un tableau d’objets de destination renvoyés par l’Edge Network.

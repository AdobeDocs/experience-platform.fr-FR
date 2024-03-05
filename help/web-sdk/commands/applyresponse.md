---
title: applyResponse
description: Utilisez une réponse du réseau Edge pour initialiser le SDK Web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

La variable `applyResponse` vous permet d’effectuer diverses actions en fonction d’une réponse du réseau Edge. Il est généralement utilisé dans les déploiements hybrides où le serveur effectue un appel initial vers le réseau Edge. Cette commande récupère la réponse de cet appel et initialise le SDK Web dans le navigateur.

## Application d’une réponse à l’aide de l’extension de balise SDK Web

L’application des réponses est effectuée sous la forme d’une action au sein d’une règle dans l’interface des balises de collecte de données Adobe Experience Platform.

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Appliquer la réponse]**.
1. Définissez les champs de votre choix à droite.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

## Application d’une réponse à l’aide de la bibliothèque JavaScript SDK Web

Exécutez la variable `applyResponse` lors de l’appel de votre instance configurée du SDK Web. L’objet contenant des options de configuration prend en charge les champs suivants :

* **`renderDecisions`**: valeur booléenne qui force le SDK Web à effectuer le rendu de tout contenu personnalisé éligible au rendu automatique. Identique à [`renderDecisions`](sendevent/renderdecisions.md) dans le [`sendEvent`](sendevent/overview.md) .
* **`responseHeaders`**: mappage des noms d’en-tête de chaîne aux valeurs d’en-tête de chaîne.
* **`responseBody`** : obligatoire. Corps de réponse JSON de l’appel du serveur au réseau Edge.
* **`personalization.sendDisplayEvent`**: une valeur booléenne qui fonctionne de la même manière que [`personalization.sendDisplayEvent`](sendevent/personalization.md) dans le `sendEvent` .

```js
allow("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Objet de réponse

Si vous décidez [gérer les réponses](command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`propositions`**: un tableau de propositions renvoyé par le réseau Edge. Les propositions automatiquement générées incluent l’indicateur `renderAttempted` défini sur `true`.
* **`inferences`**: un tableau d’objets d’inférence, qui contient des informations d’apprentissage automatique sur cet utilisateur.
* **`destinations`**: un tableau d’objets de destination renvoyés par le réseau Edge.

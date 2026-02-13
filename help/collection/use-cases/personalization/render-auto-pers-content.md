---
title: Rendre automatiquement les propositions d’action DOM
description: Utilisez Web SDK pour effectuer automatiquement le rendu des propositions d’action DOM éligibles et gérer les scénarios de rendu de SPA courants.
keywords: personnalisation;renderDecisions;dom-action;sendEvent;applyPropositions;application sur une seule page;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Rendu automatique des propositions d’action DOM

Utilisez ce modèle lorsque votre réponse de personnalisation inclut des éléments de proposition avec le schéma :

**`https://ns.adobe.com/personalization/dom-action`**

Ces éléments incluent généralement un sélecteur et un type d’action (par exemple, `setHtml`) que le SDK Web peut appliquer automatiquement lorsque le `renderDecisions` est activé.

## &#x200B;1. Gestion du scintillement (facultatif)

Si vous devez empêcher le scintillement lors de l’application de contenu personnalisé, utilisez l’approche de gestion du scintillement recommandée pour votre mise en œuvre. Voir [Gérer le scintillement](manage-flicker.md) pour connaître les options disponibles.

## &#x200B;2. Demander et rendre des décisions notées pour le rendu automatique

Définissez `renderDecisions` sur `true` lors de l’appel de la commande `sendEvent`. La propriété `renderDecisions` est définie par défaut sur false lorsqu’elle est omise.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

Si vous devez demander des emplacements spécifiques, vous pouvez inclure les `personalization.decisionScopes` suivantes :

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

Voir l’objet [`personalization`](/help/collection/js/commands/sendevent/personalization.md) dans la commande [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) pour plus d’informations.

## &#x200B;3. Afficher les événements

Si vous définissez `renderDecisions` sur `true` et que vous définissez `personalization.sendDisplayEvent` sur `true` ou que vous l’omettez, le SDK Web envoie des événements d’affichage immédiatement après le rendu de la personnalisation.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

Consultez [Gérer les événements d’affichage](display-events.md) pour d’autres options qui répondent aux besoins de votre implémentation, comme l’utilisation d’[événements de page supérieure et inférieure](top-bottom-page-events.md).

## &#x200B;4. Modifications de l’affichage SPA et nouveau rendu

Pour les applications d’une seule page, incluez une `viewName` sur les événements qui modifient la vue.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

Si votre SPA effectue un nouveau rendu de l’interface utilisateur pour la même vue sans nouvelle récupération de décision, vous pouvez appliquer à nouveau les propositions précédemment renvoyées :

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

Voir [`applyPropositions`](/help/collection/js/commands/applypropositions.md) pour plus d’informations.

>[!NOTE]
>
>La commande `applyPropositions` n’envoie pas automatiquement d’événements d’affichage. Si vous devez enregistrer « display » pour des scénarios de nouveau rendu, reportez-vous à la section [ Gérer les événements d’affichage ](display-events.md).

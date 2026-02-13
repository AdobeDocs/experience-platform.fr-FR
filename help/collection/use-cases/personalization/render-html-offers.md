---
title: Rendu des offres HTML sans sélecteurs
description: Effectuez le rendu des éléments de proposition HTML qui n’incluent pas de sélecteurs en fournissant des métadonnées à applyPropositions, puis enregistrez les événements d’affichage.
keywords: personnalisation;applyPropositions;métadonnées;actionType;decisionScopes;afficher des événements;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Rendu des offres HTML sans sélecteurs

Utilisez ce modèle lorsque vos propositions incluent du contenu HTML, mais que vous devez indiquer où l’appliquer (sélecteur) et comment l’appliquer (type d’action). Pour ce faire, appelez [`applyPropositions`](/help/collection/js/commands/applypropositions.md) avec un objet `metadata` indexé par la portée. Les valeurs `actionType` prises en charge sont `setHtml`, `replaceHtml` et `appendHtml`.

## &#x200B;1. Gestion du scintillement (facultatif)

Si vous masquez le contenu lors du rendu, vous êtes responsable de sa révélation une fois le rendu terminé. Voir [Gérer le scintillement](manage-flicker.md) pour plus d’informations.

## &#x200B;2. Propositions de requête pour les portées que vous avez l’intention de rendre

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Voir [`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md) pour plus d’informations.

## &#x200B;3. Rendu des offres avec des métadonnées `applyPropositions`

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## &#x200B;4. Enregistrer les événements d’affichage pour les propositions rendues

Les événements d’affichage ne sont pas automatiquement envoyés lors de l’appel de `applyPropositions`. Une fois le rendu terminé, utilisez un appel `sendEvent` qui référence les propositions rendues :

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

Voir [Gérer les événements d’affichage](display-events.md) pour plus d’informations.

>[!TIP]
>
>Si vous utilisez des événements [Page supérieure et page inférieure](top-bottom-page-events.md), cet appel d’« affichage des enregistrements » est généralement implémenté dans l’appel d’`sendEvent` inférieure.

## &#x200B;5. Rendu

Si votre implémentation nécessite un nouveau rendu ultérieurement (par exemple dans les applications monopages), appelez-`applyPropositions` de nouveau avec les mêmes propositions et métadonnées :

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

Si vous devez enregistrer un événement d’affichage pour ce nouveau rendu, voir [Gérer les événements d’affichage](display-events.md).

---
title: Effectuer le rendu manuel des propositions
description: Effectuez le rendu du contenu de proposition à l’aide de votre propre logique d’interface utilisateur (HTML, JSON ou schémas personnalisés), puis enregistrez les événements d’affichage.
keywords: personnalisation;propositions;rendu manuel;sendEvent;decisionScopes;afficher les événements;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Effectuer le rendu manuel des propositions

Utilisez ce modèle lorsque vous avez besoin d&#39;un contrôle total sur la manière dont les éléments de proposition sont appliqués. Par exemple, vous composez une interface utilisateur complexe à partir de contenu JSON ou vous souhaitez appliquer des règles métier personnalisées avant le rendu.

## &#x200B;1. Propositions de requête

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Voir l’objet [`personalization`](/help/collection/js/commands/sendevent/personalization.md) dans la commande [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) pour plus d’informations.

## &#x200B;2. Rendu des éléments de proposition (exemple)

Lors du rendu manuel de propositions, elles peuvent prendre de nombreuses formes différentes. Voici un exemple minimal qui détecte une proposition par portée, puis applique le premier élément de contenu HTML détecté.

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>Si vous effectuez le rendu d’HTML, assurez-vous qu’il est sûr pour votre environnement. Traitez le rendu du contenu comme une limite de sécurité (assainissement, sources approuvées et considérations relatives à la CSP).

## &#x200B;3. Enregistrer les événements d’affichage pour ce que vous avez rendu

Pour les propositions rendues manuellement, les événements d’affichage sont enregistrés par le biais d’appels `sendEvent` qui font référence aux propositions rendues.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

Voir [Gérer les événements d’affichage](display-events.md) pour plus d’informations.

## &#x200B;4. Rendu

Lorsque les modifications de l’interface utilisateur nécessitent un nouveau rendu, réexécutez votre logique de rendu manuel par rapport aux données de proposition que vous avez mises en cache (ou récupérez à nouveau, si nécessaire). Si vous devez enregistrer un affichage pour les scénarios de nouveau rendu, voir [Gérer les événements d’affichage](display-events.md).

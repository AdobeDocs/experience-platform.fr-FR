---
title: Gestion des événements d’affichage dans le SDK Web
description: Décrit ce que sont les événements d’affichage et comment les utiliser dans le SDK Web.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: personnalisation;événements d’affichage;sendEvent;renderDecisions;applyPropositions;propositions;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Gestion des événements d’affichage dans le SDK Web

Les événements d’affichage indiquent aux services de personnalisation ou d’analyse qu’un élément spécifique de contenu personnalisé a été affiché pour l’utilisateur. L’envoi d’événements d’affichage améliore la précision des rapports en aidant les systèmes en aval à faire la distinction entre le contenu *demandé* et le contenu *réellement affiché*.

## Envoyer automatiquement des événements d’affichage

Les événements d’affichage automatique sont généralement l’option la plus simple. Elles sont envoyées immédiatement après que Web SDK a terminé le rendu du contenu éligible à partir de la réponse `sendEvent`, ce qui peut améliorer la précision des rapports.

Pour envoyer automatiquement des événements d’affichage, utilisez un appel `sendEvent` qui définit `renderDecisions` sur `true` et `personalization.sendDisplayEvent` sur `true` (ou omettez-le, car `true` est la valeur par défaut) :

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>Les événements d’affichage automatiques dépendent du rendu géré par SDK. Si vous effectuez le rendu manuel du contenu (y compris à l’aide de `applyPropositions`), vous devez envoyer des événements d’affichage explicitement à l’aide de `sendEvent`.

## Envoi d’événements d’affichage dans les appels de `sendEvent` suivants

L’inclusion d’événements d’affichage dans un appel de `sendEvent` ultérieur est utile lorsque vous souhaitez joindre des données de chargement de page supplémentaires qui ne sont pas disponibles lors de la demande de personnalisation. Elle est généralement utilisée lors de l’implémentation d’[événements de page supérieure et inférieure](/help/collection/use-cases/personalization/top-bottom-page-events.md). Cette implémentation correcte des événements d’affichage permet d’éviter les problèmes liés au [Taux de rebond](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/bounce-rate) dans Adobe Analytics.

1. Lors de l’appel `sendEvent` initial (souvent en haut de la page), demandez et effectuez le rendu du contenu, mais supprimez les événements d’affichage automatique en définissant `renderDecisions` sur `true` et `personalization.sendDisplayEvent` sur `false` :

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. Plus tard (souvent au bas de la page), appelez `sendEvent` avec une payload XDM qui inclut des événements d’affichage pour les propositions rendues depuis la requête précédente en définissant [`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md) sur `true` :

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>Seules les propositions rendues automatiquement dont l’affichage était supprimé sont incluses lors de l’utilisation de `includeRenderedPropositions`.

## Envoi d’événements d’affichage pour les propositions générées manuellement

Si vous effectuez le rendu du contenu vous-même (rendu entièrement manuel ou à l’aide de `applyPropositions`), vous devez envoyer explicitement les événements d’affichage à l’aide de la commande `sendEvent` . Appelez `sendEvent` avec une payload XDM qui inclut les propriétés suivantes :

* `_experience.decisioning.propositions` contenant les `id`, `scope` et `scopeDetails` des propositions rendues
* `_experience.decisioning.propositionEventType.display` défini sur `1`

Les deux exemples suivants utilisent cette fonction d’assistance pour créer la payload XDM de l’événement d’affichage :

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

L’exemple suivant utilise le rendu manuel avec des événements d’affichage :

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

L’exemple suivant utilise la commande `applyPropositions` avec des événements d’affichage. Il enchaîne `sendEvent`, `applyPropositions`, puis un autre `sendEvent` :

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## Erreurs courantes à éviter

* **Envoyer des événements d’affichage avant la fin du rendu** : envoyez des événements d’affichage une fois le rendu automatique terminé, une fois le `applyPropositions` résolu ou une fois votre logique de rendu manuel terminée.
* **Envoyez des événements d’affichage pour les propositions que vous n’avez pas rendues** : incluez uniquement les propositions qui ont été réellement affichées pour l’utilisateur.
* **Suppression de`scopeDetails`** : incluez les `scopeDetails` de l’objet de proposition lors de l’envoi d’événements d’affichage.

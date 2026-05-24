---
title: Gestion des événements d’affichage dans le SDK Web
description: Décrit ce que sont les événements d’affichage et comment les utiliser dans le SDK Web.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: personnalisation;événements d’affichage;sendEvent;renderDecisions;applyPropositions;propositions;
TQID: https://experienceleague.adobe.com/JCQ7B8nsvKMsG1vRmIM-Cm9HmqPW9Y7-tIZ5lbtr43Q
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 421
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

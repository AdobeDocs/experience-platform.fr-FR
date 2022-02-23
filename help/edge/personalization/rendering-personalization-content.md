---
title: Rendu de contenu personnalisé à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web de Adobe Experience Platform.
keywords: personnalisation;renderDecisions;sendEvent;décisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 6ba563db7fd31084813426ffbb0c35be9d7fe4bb
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 3%

---

# Rendu de contenu personnalisé

Le SDK Web de Adobe Experience Platform prend en charge la récupération de contenu personnalisé à partir des solutions de personnalisation d’Adobe, y compris [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) et [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=fr).

En outre, le SDK Web offre des fonctionnalités de personnalisation de même page et page suivante par le biais de destinations de personnalisation Adobe Experience Platform, telles que [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) et le [connexion à la personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md). Pour savoir comment configurer Experience Platform pour la personnalisation de la même page et de la page suivante, reportez-vous à la section [guide dédié](../../destinations/ui/configure-personalization-destinations.md).

Contenu créé dans Adobe Target [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) peut être récupéré et rendu automatiquement par le SDK. Contenu créé dans Adobe Target [Compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) ou Offer decisioning ne peut pas être rendu automatiquement par le SDK. Vous devez plutôt demander ce contenu à l’aide du SDK, puis effectuer vous-même le rendu manuel du contenu.

## Rendu automatique du contenu

Lors de l’envoi d’événements au serveur, vous pouvez définir la variable `renderDecisions` option à `true`. Cela oblige le SDK à effectuer automatiquement le rendu de tout contenu personnalisé éligible au rendu automatique.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Le rendu du contenu personnalisé est asynchrone. Vous ne devez donc pas faire d’hypothèses sur le moment où un élément de contenu particulier aura terminé le rendu.

## Rendu manuel du contenu

Pour accéder à tout contenu de personnalisation, vous pouvez fournir une fonction de rappel qui sera appelée une fois que le SDK aura reçu une réponse réussie du serveur. Votre rappel reçoit une `result` , qui peut contenir un objet `propositions` contenant tout contenu de personnalisation renvoyé. Vous trouverez ci-dessous un exemple de la manière dont vous fournissez une fonction de rappel lors de l’envoi d’un événement.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Dans cet exemple, `result.propositions`, s’il existe, est un tableau contenant des propositions de personnalisation liées à l’événement. Par défaut, elle ne comprend que les propositions éligibles au rendu automatique.

Le `propositions` tableau peut ressembler à cet exemple :

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

Dans l’exemple, la variable `renderDecisions` n’était pas définie sur `true` lorsque la variable `sendEvent` a été exécutée, de sorte que le SDK n’a pas tenté d’afficher automatiquement le contenu. Le SDK a toutefois récupéré automatiquement le contenu éligible au rendu automatique et vous l’a fourni pour effectuer un rendu manuel si vous le souhaitez. Notez que chaque objet de proposition a son `renderAttempted` définie sur `false`.

Si vous avez plutôt défini la variable `renderDecisions` option à `true` lors de l’envoi de l’événement, le SDK aurait tenté d’effectuer le rendu de toutes les propositions éligibles pour le rendu automatique (comme décrit précédemment). Par conséquent, chaque objet de proposition aurait sa `renderAttempted` définie sur `true`. Dans ce cas, il n’est pas nécessaire d’effectuer le rendu manuel de ces propositions.

Jusqu’à présent, nous n’avons parlé que du contenu de personnalisation éligible au rendu automatique (c’est-à-dire de tout contenu créé dans le compositeur d’expérience visuelle Adobe Target). Pour récupérer un contenu de personnalisation _not_ éligible au rendu automatique, vous devez demander le contenu en renseignant la variable `decisionScopes` lors de l’envoi de l’événement. Une portée est une chaîne qui identifie une proposition particulière que vous souhaitez récupérer du serveur.

Voici un exemple :

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Dans cet exemple, si des propositions sont trouvées sur le serveur correspondant au `salutation` ou `discount` , elles sont renvoyées et incluses dans la variable `result.propositions` tableau. Gardez à l’esprit que les propositions admissibles au rendu automatique continueront à être incluses dans la variable `propositions` , quelle que soit la manière dont vous configurez `renderDecisions` ou `decisionScopes` options. Le `propositions` dans ce cas, le tableau ressemble à l’exemple suivant :

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

À ce stade, vous pouvez générer le contenu des propositions à votre gré. Dans cet exemple, la proposition correspondant au `discount` scope est une proposition de HTML créée à l’aide du compositeur d’expérience d’après les formulaires Adobe Target. En supposant que votre page comporte un élément avec l’identifiant de `daily-special` et souhaitez effectuer le rendu du contenu à partir du `discount` dans la `daily-special` effectuez les opérations suivantes :

1. Extraire les propositions des `result` .
1. Parcourez chaque proposition, en recherchant la proposition avec un périmètre de `discount`.
1. Si vous trouvez une proposition, passez en boucle chaque élément de la proposition, recherchant l’élément qui est le contenu HTML. (Mieux vaut vérifier que supposer.)
1. Si vous trouvez un élément contenant du contenu de HTML, recherchez la variable `daily-special` sur la page et remplacez son HTML par le contenu personnalisé.
1. Une fois le contenu rendu, envoyez une `display` .

Votre code se présenterait comme suit :

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Si vous utilisez Adobe Target, les portées correspondent aux mbox sur le serveur, sauf qu’elles sont toutes demandées à la fois et non individuellement. La mbox globale est toujours renvoyée.

### Gestion du scintillement

Le SDK fournit des fonctionnalités pour les éléments suivants : [gérer le scintillement](../personalization/manage-flicker.md) pendant le processus de personnalisation.

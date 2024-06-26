---
title: Rendu de contenu personnalisé à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web de Adobe Experience Platform.
keywords: personnalisation;renderDecisions;sendEvent;décisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 6841a6f777d18845ce36e3503fbdb9698ece84bb
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 1%

---

# Rendu de contenu personnalisé

Le SDK Web de Adobe Experience Platform prend en charge la récupération de contenu personnalisé à partir des solutions de personnalisation d’Adobe, y compris [Adobe Target](https://business.adobe.com/fr/products/target/adobe-target.html), [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=fr) et [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=fr).

En outre, le SDK Web offre des fonctionnalités de personnalisation de même page et page suivante par le biais de destinations de personnalisation Adobe Experience Platform, telles que [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) et la variable [connexion à la personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md). Pour savoir comment configurer Experience Platform pour la personnalisation de la même page et de la page suivante, reportez-vous à la section [guide dédié](../../destinations/ui/activate-edge-personalization-destinations.md).

Contenu créé dans Adobe Target [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) et Adobe Journey Optimizer [Interface utilisateur de Campaign web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) peut être récupéré et rendu automatiquement par le SDK. Contenu créé dans Adobe Target [Compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr), ADOBE JOURNEY OPTIMIZER [Canal d’expérience basé sur le code](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based) ou Offer decisioning ne peut pas être rendu automatiquement par le SDK. Vous devez plutôt demander ce contenu à l’aide du SDK, puis effectuer vous-même le rendu manuel du contenu.

## Rendu automatique du contenu {#automatic}

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

## Rendu manuel du contenu {#manual}

Pour accéder à tout contenu de personnalisation, vous pouvez fournir une fonction de rappel qui sera appelée une fois que le SDK aura reçu une réponse réussie du serveur. Votre rappel reçoit une `result` , qui peut contenir un objet `propositions` contenant tout contenu de personnalisation renvoyé. Vous trouverez ci-dessous un exemple de la manière dont vous fournissez une fonction de rappel lors de l’envoi d’un événement.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Dans cet exemple, `result.propositions`, s’il existe, est un tableau contenant des propositions de personnalisation liées à l’événement. Par défaut, elle ne comprend que les propositions éligibles au rendu automatique.

La variable `propositions` tableau peut ressembler à cet exemple :

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

Si vous avez plutôt défini la variable `renderDecisions` option à `true` lors de l’envoi de l’événement, le SDK aurait tenté d’effectuer le rendu de toutes les propositions éligibles pour le rendu automatique (comme décrit précédemment). Par conséquent, chaque objet de proposition aurait sa `renderAttempted` définie sur `true`. Dans ce cas, il n’est pas nécessaire de générer manuellement ces propositions.

Jusqu’à présent, nous n’avons parlé que du contenu de personnalisation éligible au rendu automatique (c’est-à-dire tout contenu créé dans le compositeur d’expérience visuelle Adobe Target ou l’interface utilisateur de Adobe Journey Optimizer Web Campaign). Pour récupérer un contenu de personnalisation _not_ éligible au rendu automatique, vous devez demander le contenu en renseignant la variable `decisionScopes` lors de l’envoi de l’événement. Une portée est une chaîne qui identifie une proposition particulière que vous souhaitez récupérer du serveur.

Voici un exemple :

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Dans cet exemple, si des propositions sont trouvées sur le serveur correspondant au `salutation` ou `discount` , elles sont renvoyées et incluses dans la variable `result.propositions` tableau. Gardez à l’esprit que les propositions admissibles au rendu automatique continueront à être incluses dans la variable `propositions` , quelle que soit la manière dont vous configurez `renderDecisions` ou `decisionScopes` options. La variable `propositions` dans ce cas, le tableau ressemble à l’exemple suivant :

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

À ce stade, vous pouvez générer le contenu des propositions à votre gré. Dans cet exemple, la proposition correspondant au `discount` scope est une proposition de HTML créée à l’aide du compositeur d’expérience d’après les formulaires Adobe Target. En supposant que votre page comporte un élément avec l’identifiant de `daily-special` et souhaitez effectuer le rendu du contenu à partir de la fonction `discount` dans la `daily-special` effectuez les opérations suivantes :

1. Extraire les propositions des `result` .
1. Parcourez chaque proposition, en recherchant la proposition avec un périmètre de `discount`.
1. Si vous trouvez une proposition, passez en boucle chaque élément de la proposition, recherchant l’élément qui est le contenu HTML. (Mieux vaut vérifier que supposer.)
1. Si vous trouvez un élément contenant du contenu de HTML, recherchez la variable `daily-special` sur la page et remplacez son HTML par le contenu personnalisé.
1. Une fois le contenu rendu, envoyez une `display` .

Votre code se présenterait comme suit :

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
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

Le SDK fournit des fonctionnalités pour [gérer le scintillement](../personalization/manage-flicker.md) pendant le processus de personnalisation.

## Rendu des propositions dans des applications d’une seule page sans incrémenter de mesures {#applypropositions}

La variable `applyPropositions` vous permet de générer ou d’exécuter un tableau de propositions à partir de [!DNL Target] ou Adobe Journey Optimizer en applications d’une seule page, sans incrémenter la variable [!DNL Analytics] et [!DNL Target] mesures. Cela augmente la précision des rapports.

>[!IMPORTANT]
>
>Si des propositions pour la `__view__` la portée (ou une surface web) étaient rendues au chargement de la page, leurs `renderAttempted` L’indicateur sera défini sur `true`. La variable `applyPropositions` ne restituera pas à nouveau la variable `__view__` propositions de portée (ou de surface web) qui ont la variable `renderAttempted: true` Indicateur.

### Cas d’utilisation 1 : rendu des propositions de vue d’application d’une seule page

Le cas d’utilisation décrit dans l’exemple ci-dessous restitue à nouveau les propositions d’affichage de panier récupérées et rendues précédemment sans envoyer de notifications d’affichage.

Dans l’exemple ci-dessous, la variable `sendEvent` est déclenchée lors d’un changement d’affichage et enregistre l’objet résultant dans une constante.

Ensuite, lorsque l’affichage ou un composant est mis à jour, la variable `applyPropositions` est appelée, avec les propositions de la précédente `sendEvent` pour effectuer le rendu des propositions d’affichage.

```js
var cartPropositions = alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
        "web": {
            "webPageDetails": {
                "viewName": "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    "propositions": cartPropositions
});
```

### Cas d’utilisation 2 : Rendu des propositions qui ne comportent pas de sélecteur

Ce cas pratique s’applique aux expériences créées à l’aide de la méthode [!DNL Target Form-based Experience Composer] ou Adobe Journey Optimizer [Canal d’expérience basé sur le code](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based).

Vous devez fournir le sélecteur, l’action et la portée dans la variable `applyPropositions` appelez .

Pris en charge `actionTypes` sont :

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
            "salutation": {
                "selector": "#first-form-based-offer",
                "actionType": "setHtml"
            },
            "discount": {
                "selector": "#second-form-based-offer",
                "actionType": "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        function sendDisplayEvent(proposition) {
            const {
                id,
                scope,
                scopeDetails = {}
            } = proposition;

            alloy("sendEvent", {
                xdm: {
                    eventType: "decisioning.propositionDisplay",
                    _experience: {
                        decisioning: {
                            propositions: [{
                                id: id,
                                scope: scope,
                                scopeDetails: scopeDetails,
                            }, ],
                            propositionEventType: {
                                display: 1
                            },
                        },
                    },
                },
            });
        }
    });
});
```

Si vous ne fournissez aucune métadonnée pour la portée d’une décision, les propositions associées ne seront pas générées.

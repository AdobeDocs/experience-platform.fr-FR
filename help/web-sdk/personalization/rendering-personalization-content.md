---
title: Rendu de contenu personnalisé à l’aide de Adobe Experience Platform Web SDK
description: Découvrez comment effectuer le rendu du contenu personnalisé avec Adobe Experience Platform Web SDK.
keywords: personnalisation;renderDecisions;sendEvent;decisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 2%

---

# Rendu de contenu personnalisé

Adobe Experience Platform Web SDK prend en charge la récupération de contenu personnalisé à partir de solutions de personnalisation Adobe, notamment [Adobe Target](https://business.adobe.com/fr/products/target/adobe-target.html), [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=fr) et [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=fr).

En outre, le SDK Web alimente les fonctionnalités de personnalisation de la même page et de la page suivante via les destinations de personnalisation Adobe Experience Platform, telles que [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) et la [connexion de personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md). Pour savoir comment configurer Experience Platform pour la personnalisation de la même page et de la page suivante, consultez le [&#x200B; guide dédié &#x200B;](../../destinations/ui/activate-edge-personalization-destinations.md).

Le contenu créé dans Adobe Target [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr) et Adobe Journey Optimizer [interface utilisateur de Web Campaign](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=fr) peut être récupéré et rendu automatiquement par SDK. Le contenu créé dans Adobe Target [Compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr), Adobe Journey Optimizer [Canal d’expérience d’après le code](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/code-based-experience/get-started-code-based) ou Offer Decisioning ne peut pas être rendu automatiquement par SDK. Vous devez plutôt demander ce contenu à l’aide du SDK, puis effectuer manuellement le rendu du contenu.

## Rendu automatique du contenu {#automatic}

Lors de l’envoi d’événements au serveur, vous pouvez définir l’option `renderDecisions` sur `true`. Cela force le SDK à effectuer automatiquement le rendu de tout contenu personnalisé éligible au rendu automatique.

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

Le rendu du contenu personnalisé est asynchrone. Vous ne devez donc pas émettre d’hypothèses sur le moment où un élément de contenu particulier aura terminé le rendu.

## Rendu manuel du contenu {#manual}

Pour accéder au contenu de personnalisation, vous pouvez fournir une fonction de rappel, qui sera appelée une fois que le SDK aura reçu une réponse réussie du serveur. Votre rappel est fourni avec un objet `result` , qui peut contenir une propriété `propositions` contenant tout contenu de personnalisation renvoyé. Vous trouverez ci-dessous un exemple de la manière dont vous pouvez fournir une fonction de rappel lors de l’envoi d’un événement.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Dans cet exemple, `result.propositions`, s’il existe, est un tableau contenant des propositions de personnalisation liées à l’événement. Par défaut, elle inclut uniquement les propositions éligibles au rendu automatique.

Le tableau `propositions` peut ressembler à cet exemple :

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

Dans cet exemple, l’option `renderDecisions` n’était pas définie sur `true` lors de l’exécution de la commande `sendEvent`. Par conséquent, le SDK n’a pas tenté d’effectuer automatiquement le rendu d’un contenu. Cependant, le SDK a toujours récupéré automatiquement le contenu éligible au rendu automatique et vous a fourni ceci pour effectuer manuellement le rendu si vous le souhaitez. Notez que la propriété `renderAttempted` de chaque objet de proposition est définie sur `false`.

Si, à la place, vous aviez défini l’option `renderDecisions` sur `true` lors de l’envoi de l’événement, le SDK aurait tenté de rendre toutes les propositions éligibles au rendu automatique (comme décrit précédemment). Par conséquent, la propriété `renderAttempted` de chacun des objets de proposition est définie sur `true`. Dans ce cas, il n’est pas nécessaire d’effectuer manuellement le rendu de ces propositions.

Jusqu’à présent, nous n’avons parlé que du contenu de personnalisation éligible au rendu automatique (c’est-à-dire tout contenu créé dans le compositeur d’expérience visuelle d’Adobe Target ou l’interface utilisateur de Campaign Web de Adobe Journey Optimizer). Pour récupérer un contenu de personnalisation _non éligible_ pour le rendu automatique, vous devez demander le contenu en renseignant l’option `decisionScopes` lors de l’envoi de l’événement. Une portée est une chaîne qui identifie une proposition particulière que vous souhaitez récupérer à partir du serveur.

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

Dans cet exemple, si des propositions sont trouvées sur le serveur correspondant à la portée `salutation` ou `discount`, elles sont renvoyées et incluses dans le tableau `result.propositions` . N’oubliez pas que les propositions qui remplissent les critères du rendu automatique continueront à être incluses dans le tableau `propositions`, quelle que soit la manière dont vous configurez les options `renderDecisions` ou `decisionScopes`. Le tableau `propositions`, dans ce cas, ressemble à cet exemple :

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

À ce stade, vous pouvez effectuer le rendu du contenu de proposition comme vous le souhaitez. Dans cet exemple, la proposition correspondant à la portée `discount` est une proposition HTML créée à l’aide du compositeur d’expérience d’après les formulaires d’Adobe Target. En supposant que votre page comporte un élément avec l’ID de `daily-special` et que vous souhaitiez effectuer le rendu du contenu de la proposition de `discount` dans l’élément de `daily-special`, procédez comme suit :

1. Extrayez des propositions de l’objet `result`.
1. Parcourez chaque proposition en recherchant la proposition avec une portée de `discount`.
1. Si vous trouvez une proposition, parcourez chaque élément de la proposition, en recherchant l’élément correspondant au contenu HTML. (Mieux vaut vérifier que supposer.)
1. Si vous trouvez un élément contenant du contenu HTML, recherchez l’élément `daily-special` sur la page et remplacez son HTML par le contenu personnalisé.
1. Une fois le contenu rendu, envoyez un événement `display`.

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
    // Rather than assuming there is a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
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
            ],
            "propositionEventType": {
              "display": 1
            }
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Si vous utilisez Adobe Target, les portées correspondent aux mBox sur le serveur, sauf qu’elles sont toutes demandées en même temps et non individuellement. La mbox globale est toujours renvoyée.

### Gestion du scintillement

Le SDK permet de [gérer le scintillement](../personalization/manage-flicker.md) pendant le processus de personnalisation.

## Propositions de rendu dans les applications monopages sans incrémenter de mesures {#applypropositions}

La commande `applyPropositions` vous permet de générer ou d’exécuter un tableau de propositions à partir de [!DNL Target] ou Adobe Journey Optimizer dans des applications d’une seule page, sans incrémenter les mesures [!DNL Analytics] et [!DNL Target]. Cela augmente la précision des rapports.

>[!IMPORTANT]
>
>Si des propositions pour la portée de la `__view__` (ou une surface web) ont été rendues au chargement de la page, leur indicateur de `renderAttempted` est défini sur `true`. La commande `applyPropositions` n’effectue pas le rendu des propositions de portée `__view__` (ou de surface web) qui ont l’indicateur `renderAttempted: true`.

### Cas d’utilisation 1 : Restituer des propositions d’affichage d’application monopage

Le cas d’utilisation décrit dans l’exemple ci-dessous effectue un nouveau rendu des propositions d’affichage de panier récupérées et rendues précédemment sans envoyer de notifications d’affichage.

Dans l’exemple ci-dessous, la commande `sendEvent` est déclenchée lors d’un changement d’affichage et enregistre l’objet résultant dans une constante.

Ensuite, lorsque la vue ou un composant est mis à jour, la commande `applyPropositions` est appelée, avec les propositions de la commande `sendEvent` précédente, pour effectuer à nouveau le rendu des propositions de vue.

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

### Cas d’utilisation 2 : propositions de rendu sans sélecteur

Ce cas pratique s’applique aux expériences créées à l’aide du canal d’expérience basé sur le code [!DNL Target Form-based Experience Composer] ou Adobe Journey Optimizer [code](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/code-based-experience/get-started-code-based).

Vous devez fournir le sélecteur, l’action et la portée dans l’appel `applyPropositions`.

Les `actionTypes` pris en charge sont les suivants :

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
                "xdm": {
                    "eventType": "decisioning.propositionDisplay",
                    "_experience": {
                        "decisioning": {
                            "propositions": [{
                              	"id": id,
                                "scope": scope,
                              	"scopeDetails": scopeDetails
                            }],
                            "propositionEventType": {
                                "display": 1
                            }
                        }
                    }
                }
            });
        }
    });
});
```

Si vous ne fournissez aucune métadonnée pour une portée de décision, les propositions associées ne seront pas rendues.

---
title: Comparaison d’at.js au SDK Web Experience Platform
description: Découvrez comment comparer les fonctionnalités d’at.js au SDK Web Experience Platform
keywords: target;adobe target;activity.id;experience.id;renderDecisions;champ de décision;fragment de code de masquage préalable;vec;compositeur d’expérience d’après les formulaires;xdm;audiences;décisions;portée;schéma;schéma;diagramme système;diagramme
source-git-commit: 6efb40e90cb8c29a0141bb0db6e20cec23f2be9a
workflow-type: tm+mt
source-wordcount: '2277'
ht-degree: 7%

---

# Comparaison de la bibliothèque at.js avec le SDK Web

## Présentation

Cet article présente un aperçu des différences entre les `at.js` et le SDK Web d’Experience Platform.

## Installation des bibliothèques

### Installation d’at.js

Nous autorisons nos clients à télécharger la bibliothèque directement depuis l’onglet Mise en oeuvre de Adobe Experience Cloud. La bibliothèque at.js est personnalisée avec les paramètres suivants du client : clientCode, imsOrgId, etc.

### Installation du SDK Web

La version prédéfinie est disponible sur un CDN. Vous pouvez référencer la bibliothèque sur le réseau de diffusion de contenu directement sur votre page, ou la télécharger et l’héberger sur votre propre infrastructure. Il est disponible dans des formats minimisés et non minimisés. La version non minimisée est utile à des fins de débogage.

Structure de l’URL : https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OU alloy.js pour la version non minimisée.

Par exemple :

* Minified : [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Non minimisé : [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)

[En savoir plus](../../fundamentals/installing-the-sdk.md)

## Configuration des bibliothèques

### Configuration d’at.js

À la fin de chaque fichier at.js, vous trouverez une section dans laquelle nous instancions et transmettons un objet de paramètre. Il est personnalisable. Au téléchargement, nous renseignons cette section avec les paramètres client actuels.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)


### Configuration du SDK Web

La configuration du SDK est effectuée à l’aide de la commande `configure`.

>[!IMPORTANT]
>
>`configure` is *always* la première commande appelée.

Exemple :

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

De nombreuses options peuvent être définies lors de la configuration. Vous trouverez ci-dessous toutes les options regroupées par catégorie.

[En savoir plus](../../fundamentals/configuring-the-sdk.md)


## Comment demander et générer automatiquement des offres Target de chargement de page

### Utilisation d’at.js

Utilisation d’at.js 2.x, si vous activez le paramètre `pageLoadEnabled`, la bibliothèque déclenche un appel à Target Edge avec `execute -> pageLoad`. Si tous les paramètres sont définis sur les valeurs par défaut, aucun codage personnalisé n’est nécessaire. Une fois at.js ajouté à la page et chargé par le navigateur, un appel Target Edge est exécuté.

### Utilisation du SDK Web

Contenu créé dans Adobe Target [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) peut être récupéré et rendu automatiquement par le SDK.

Pour demander et générer automatiquement des offres Target, utilisez la méthode `sendEvent` et définissez `renderDecisions` option à `true`. Cela oblige le SDK à effectuer automatiquement le rendu de tout contenu personnalisé éligible au rendu automatique.

Exemple :

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

Le SDK Web Experience Platform envoie automatiquement une notification avec les offres qui ont été exécutées par le SDK WEB. Voici un exemple de l’aspect d’une payload de requête de notification :

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[En savoir plus](../rendering-personalization-content.md)

## Comment demander et NE PAS générer automatiquement des offres Target de chargement de page

### Utilisation d’at.js

Il existe deux façons de déclencher un appel à Target Edge qui récupérera les offres pour le chargement de la page.

Exemple 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Exemple 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)

### Utilisation du SDK Web

Exécuter une `sendEvent` avec une portée spéciale sous `decisionScopes`: `__view__`. Nous utilisons cette portée comme signal pour récupérer toutes les activités de chargement de page de Target et prérécupérer toutes les vues. Le SDK Web tente également d’évaluer toutes les activités basées sur les vues du VEC. La désactivation de la prérécupération des vues n’est actuellement pas prise en charge dans le SDK Web.

Pour accéder à tout contenu de personnalisation, vous pouvez fournir une fonction de rappel qui sera appelée une fois que le SDK aura reçu une réponse réussie du serveur. Votre rappel reçoit un objet result qui peut contenir la propriété de proposition contenant tout contenu de personnalisation renvoyé.

Exemple :

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[En savoir plus](../rendering-personalization-content.md#manually-rendering-content)


## Comment demander des mbox Target spécifiques basées sur un formulaire


### Utilisation d’at.js

Vous pouvez récupérer les activités du compositeur d’après les formulaires à l’aide de la fonction `getOffer` function:

Exemple 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Exemple 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)


### Utilisation du SDK Web

Vous pouvez récupérer les activités basées sur le compositeur d’après les formulaires à l’aide de la fonction `sendEvent` et transmission des noms de mbox sous le `decisionScopes` . Le `sendEvent` renvoie une promesse résolue avec un objet contenant les activités/propositions demandées : Voici comment la variable `propositions` tableau se présente comme suit :

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Exemple :

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[En savoir plus](../rendering-personalization-content.md#manually-rendering-content)

## Comment appliquer les activités Target

### Utilisation d’at.js

Vous pouvez appliquer les activités Target à l’aide de la variable `applyOffers` function: `adobe.target.applyOffer(options)`

Exemple :

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=en)

### Utilisation du SDK Web

Cette fonctionnalité n’est actuellement pas prise en charge dans le SDK Web.

## Suivi des événements

### Utilisation d’at.js

Vous pouvez effectuer le suivi des événements à l’aide de la variable `trackEvent` fonction ou utilisation `sendNotifications`.

Cette fonction déclenche une requête pour signaler les actions de l’utilisateur, telles que les clics et les conversions. Elle ne fournit pas d’activités dans la réponse.


**Exemple 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Exemple 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=en)

### Utilisation du SDK Web

Vous pouvez effectuer le suivi des événements et des actions de l’utilisateur en appelant le `sendEvent` , renseigner la variable `_experience.decisioning.propositions` Groupe de champs XDM et définition de la variable `eventType` à l’une des deux valeurs suivantes :

* `decisioning.propositionDisplay`: Indique le rendu de l’activité Target.
* `decisioning.propositionInteract`: Indique une interaction de l’utilisateur avec l’activité, comme un clic de souris.

Le `_experience.decisioning.propositions` Le groupe de champs XDM est un tableau d’objets. Les propriétés de chaque objet sont dérivées de la propriété `result.propositions` qui est renvoyé dans la variable `sendEvent` command : `{ id, scope, scopeDetails }`

**Exemple 1 - Suivi d’une `decisioning.propositionDisplay` événement après le rendu d’une activité**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
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

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
      // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
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

**Exemple 2 - Suivi d’une `decisioning.propositionInteract` événement après qu’une mesure de clic a eu lieu**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[En savoir plus](../rendering-personalization-content.md#manually-rendering-content)

## Comment déclencher un changement d’affichage dans une application d’une seule page

### Utilisation d’at.js

Utilisez la variable `adobe.target.triggerView` fonction . Cette fonction peut être appelée à chaque chargement d’une nouvelle page ou lorsqu’un composant fait l’objet d’un nouveau rendu sur une page. La fonction adobe.target.triggerView() doit être implémentée pour les applications d’une seule page (SPA) afin d’utiliser le compositeur d’expérience visuelle (VEC) pour créer des activités de tests A/B et de ciblage d’expérience (XT). Si adobe.target.triggerView() n’est pas implémenté sur le site, le VEC ne peut pas être utilisé pour SPA.

**Exemple**

```javascript
adobe.target.triggerView("homeView")
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=en)


### Utilisation du SDK Web

Pour déclencher ou signaler un changement d’affichage d’application d’une seule page, définissez la variable `web.webPageDetails.viewName` sous la propriété `xdm` de l’option `sendEvent` . Le SDK Web vérifie le cache des vues, s’il existe des offres pour la variable `viewName` spécifié dans `sendEvent` il les exécute et envoie un événement de notification d’affichage.

**Exemple**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[En savoir plus](./spa-implementation.md#implementing-xdm-views)

## Comment tirer parti des jetons de réponse

Le contenu de personnalisation renvoyé par Adobe Target inclut [jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), qui sont des détails sur l’activité, l’offre, l’expérience, le profil utilisateur, les informations géographiques, etc. Ces détails peuvent être partagés avec des outils tiers ou utilisés pour le débogage. Les jetons de réponse peuvent être configurés dans l’interface utilisateur d’Adobe Target.

### Utilisation d’at.js

Utilisez les événements personnalisés at.js pour écouter la réponse Target et lire les jetons de réponse.

**Exemple**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)


### Utilisation du SDK Web

>[!IMPORTANT]
>
>Assurez-vous que vous utilisez la version 2.6.0 ou ultérieure du SDK Web Platform.

Les jetons de réponse sont renvoyés dans le cadre de la fonction `propositions` qui sont exposées dans le résultat de la fonction `sendEvent` . Chaque proposition contient un tableau de `items`, et chaque élément aura une `meta` renseigné avec des jetons de réponse s’ils sont activés dans l’interface utilisateur d’administration de Target. [En savoir plus](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)

**Exemple**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[En savoir plus](./accessing-response-tokens.md)

## Comment gérer le scintillement

### Utilisation d’at.js

Avec at.js, vous pouvez gérer le scintillement en définissant `bodyHidingEnabled: true` ainsi, at.js est celui qui prend soin de pré-masquer les conteneurs personnalisés avant de récupérer et d’appliquer les modifications du DOM.
Les sections de page qui contiennent du contenu personnalisé peuvent être pré-masquées en remplaçant at.js. `bodyHiddenStyle`.
Par défaut `bodyHiddenStyle` masque tout le HTML `body`.
Les deux paramètres peuvent être remplacés à l’aide de `window.targetGlobalSettings`. `window.targetGlobalSettings` doit être placé avant le chargement d’at.js.

### Utilisation du SDK Web

Avec le SDK Web, le client peut configurer son style de prémasquage dans la commande de configuration, comme dans l’exemple ci-dessous :

```javascript
alloy("configure", {
  edgeConfigId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Lors du chargement du SDK Web asynchrone, il est recommandé d’injecter le fragment de code suivant dans la page avant d’injecter le SDK Web :

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## Comment A4T est-il géré ?

### Utilisation d’at.js

Il existe deux types de journalisation A4T pris en charge à l’aide d’at.js :

* Journalisation côté client d’Analytics
* Journalisation côté serveur Analytics

#### Journalisation côté client d’Analytics

**Exemple 1 : Utilisation du paramètre global de Target**

La journalisation côté client Analytics peut être activée en définissant `analyticsLogging: client_side` dans les paramètres at.js ou en remplaçant la variable `window.targetglobalSettings` .
Lorsque cette option est configurée, le format de la payload renvoyé ressemble à ce qui suit :

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

La payload peut ensuite être transmise à Analytics via l’API d’insertion de données.

Exemple 2 : Le configurer dans chaque `getOffers` function:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

Voici à quoi ressemble la payload de réponse :

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

Charge utile Analytics (`tnta` ) doit être inclus dans l’accès Analytics à l’aide de la fonction [API d’insertion de données](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### Journalisation côté serveur Analytics

La journalisation côté serveur Analytics peut être activée en définissant `analyticsLogging: server_side` dans les paramètres at.js ou en remplaçant la variable `window.targetglobalSettings` .
Ensuite, les données s’enchaînent comme suit :

![](assets/a4t-server-side-atjs.png)

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=en)

### Utilisation du SDK Web

Le SDK Web prend également en charge :

* Journalisation côté client d’Analytics
* Journalisation côté serveur Analytics

#### Journalisation côté client d’Analytics

La journalisation côté client d’Analytics est activée lorsqu’Adobe Analytics est désactivé pour cette configuration de DataStream.

![](assets/analytics-disabled-datastream-config.png)

Le client a accès au jeton Analytics (`tnta`) qui doivent être partagées avec Analytics à l’aide de [API d’insertion de données](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
en enchaînant la variable `sendEvent` et effectuez une itération sur le tableau propositions obtenu.

**Exemple**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Voici un diagramme qui montre comment les données circulent lorsque Analytics côté client est activé :

![](assets/analytics-client-side-logging.png)

#### Journalisation côté serveur Analytics

La journalisation côté serveur d’Analytics est activée lorsqu’Analytics est activé pour cette configuration de DataStream.

![](assets/analytics-enabled-datastream-config.png)

Lorsque la journalisation Analytics côté serveur est activée, la charge utile A4T qui doit être partagée avec Analytics afin que les rapports Analytics présentent les impressions et conversions correctes soient partagées au niveau Experience Edge, de sorte que le client n’ait pas à effectuer de traitement supplémentaire.

Voici comment les données s’enchaînent dans nos systèmes lorsque la journalisation Analytics côté serveur est activée :

![](assets/analytics-server-side-logging.png)

## Comment définir les paramètres globaux de Target

### Utilisation d’at.js

Vous pouvez remplacer les paramètres de la Bibliothèque at.js en utilisant `window.targetGlobalSettings` au lieu de configurer les paramètres dans l’interface utilisateur de Target Standard / Premium, ou d’utiliser des API REST.

Le remplacement doit être défini avant le chargement du fichier at.js ou dans Administration > Mise en oeuvre > Modifier les paramètres at.js > Paramètres du code > En-tête de bibliothèque.

Exemple :

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)

### Utilisation du SDK Web

Cette fonctionnalité n’est pas prise en charge dans le SDK Web.

## Comment mettre à jour les attributs de profil Target

### Utilisation d’at.js

**Exemple 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Exemple 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### Utilisation du SDK Web

Pour mettre à jour un profil Target, utilisez le `sendEvent` et définissez `data.__adobe.target` , préfixe les noms des clés à l’aide de `profile`.

**Exemple**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Comment utiliser Target Recommendations

### Utilisation d’at.js

**Exemple 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.productName": "T-shirt",
     "entity.productId": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Exemple 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.productName": "T-shirt",
            "entity.productId": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=en)


### Utilisation du SDK Web

Pour envoyer des données de recommandation, utilisez la méthode `sendEvent` et définissez `data.__adobe.target` , préfixe les noms des clés à l’aide de `entity`.

**Exemple**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.productName": "T-shirt",
        "entity.productId": "1234"
      }
    }
  }
});
```

## Comment utiliser des identifiants tiers

### Utilisation d’at.js

Il existe plusieurs façons d’envoyer at.js `mbox3rdPartyId`, à l’aide de `getOffer` ou `getOffers`:

**Exemple 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Exemple 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

Ou il existe un moyen de configurer la variable `mbox3rdPartyId` dans `targetPageParams` ou `targetPageParamsAll`.
Lors de sa définition dans `targetPageParams`, il sera envoyé dans les demandes pour `target-global-mbox` également connu sous le nom `pag-lLoad`.
La recommandation doit être définie à l’aide de `targetPageParamsAll` car il sera envoyé dans chaque requête cible.
L’avantage de l’utilisation de `targetPageParamsAll` est que vous pouvez définir la variable `mbox3rdPartyId` sur la page une fois, ce qui garantit que toutes les requêtes cibles ont le droit `mbox3rdPartyId`.

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[En savoir plus](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=en)

### Utilisation du SDK Web

Le SDK Web prend en charge l’identifiant tiers Target. Toutefois, cela nécessite quelques étapes supplémentaires. Avant de nous plonger dans la solution, nous devrions parler un peu `identityMap`.
La carte des identités permet aux clients d’envoyer plusieurs identités. Toutes les identités sont des espaces de noms. Chaque espace de noms peut avoir une ou plusieurs identités. Une identité particulière peut être marquée comme Principale.
En gardant ces connaissances à l’esprit, nous pouvons voir quelles sont les étapes nécessaires pour configurer le sdk web afin d’utiliser l’identifiant tiers Target.

1. Configurez l’espace de noms qui contiendra l’identifiant tiers Target dans la vue Configuration du flux de données :

![](assets/mbox-3-party-id-setup.png)

1. Envoyez cet espace de noms d’identité dans chaque commande sendEvent comme suit :

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## Comment définir les jetons de propriété

### Utilisation d’at.js

Il existe deux façons de configurer les jetons de propriété à l’aide d’at.js : `targetPageParams` ou `targetPageParamsAll`. Utilisation `targetPageParams` ajoute le jeton de propriété à la propriété `target-global-mbox` appelez, mais en utilisant `targetPageParamsAll` ajoute le jeton à tous les appels cible :

**Exemple 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Exemple 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### Utilisation du SDK Web

Avec le SDK Web, les clients peuvent configurer la propriété à un niveau supérieur, lors de la configuration du flux de données, sous l’espace de noms Adobe Target :
![](assets/at-property-setup.png)
Cela signifie que chaque appel Target pour cette configuration de flux de données spécifique va contenir ce jeton de propriété.

## Comment prérécupérer les mbox

### Utilisation d’at.js

Cette fonctionnalité est disponible uniquement dans at.js 2.x. at.js 2.x comporte une nouvelle fonction nommée `getOffers`. `getOffers` permettent aux clients de prérécupérer du contenu pour une ou plusieurs mbox. Voici un exemple :

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

REMARQUE : Il est vivement conseillé de s’assurer que la variable `mbox` dans le `mboxes` a son propre index. Généralement, la première mbox comporte `index=0`, le suivant `index=1`, etc.

### Utilisation du SDK Web

Cette fonctionnalité n’est actuellement pas prise en charge dans le SDK Web.

## Comment déboguer ma mise en oeuvre Target

### Utilisation d’at.js

at.js expose les fonctionnalités de débogage suivantes :

* Mbox Disable : désactivez Target pour vérifier si la page est rompue sans interactions Target.
* Débogage de mbox : at.js consigne chaque action.
* Target Trace : avec un jeton de suivi de mbox généré dans Bullseye, un objet trace avec les détails qui ont participé au processus de prise de décision est disponible sous `window.___target_trace` objet

Remarque : Toutes ces fonctions de débogage sont disponibles avec des fonctionnalités améliorées dans [Débogueur Adobe Experience Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### Utilisation du SDK Web

Vous disposez de plusieurs fonctionnalités de débogage lors de l’utilisation du SDK Web :

* Utilisation [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon)
* [Débogage du SDK Web activé](../../../edge/fundamentals/debugging.md)
* Utilisation [Hooks de surveillance du SDK Web](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Utilisation [Débogueur Adobe Experience Platform](https://experienceleague.adobe.com/docs/debugger/using-v2/experience-cloud-debugger.html?lang=en)
* Target Trace

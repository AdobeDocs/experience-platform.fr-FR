---
title: Journalisation côté client des données A4T dans le SDK Web Platform
description: Découvrez comment activer la journalisation côté client pour Adobe Analytics for Target (A4T) à l’aide du SDK Web Experience Platform.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;journalisation;sdk web;expérience;plateforme;
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 1%

---

# Journalisation côté client des données A4T dans le SDK Web Platform

## Vue d’ensemble {#overview}

Le SDK Web de Adobe Experience Platform vous permet de collecter des données [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr) données du côté client de votre application web.

La journalisation côté client signifie que [!DNL Target] Les données sont renvoyées côté client, ce qui vous permet de les collecter et de les partager avec Analytics. Cette option doit être activée si vous envisagez d’envoyer manuellement des données à Analytics à l’aide de la variable [API d’insertion de données](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Méthode d’exécution utilisée pour [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=fr) est actuellement en cours de développement et sera disponible dans un avenir proche.

Ce document décrit les étapes de configuration de la journalisation A4T côté client pour le SDK Web et fournit quelques exemples de mise en oeuvre pour les cas d’utilisation courants.

## Conditions préalables {#prerequisites}

Ce tutoriel suppose que vous connaissez les concepts et processus fondamentaux liés à l’utilisation du SDK Web à des fins de personnalisation. Si vous avez besoin d’une introduction, veuillez consulter la documentation suivante :

* [Configuration du SDK Web](/help/web-sdk/commands/configure/overview.md)
* [Envoi d’événements](/help/web-sdk/commands/sendevent/overview.md)
* [Rendu du contenu de personnalisation](../../rendering-personalization-content.md)

## Configuration de la journalisation côté client d’Analytics {#set-up-client-side-logging}

Les sous-sections suivantes expliquent comment activer la journalisation côté client d’Analytics pour votre mise en oeuvre du SDK Web.

### Activation de la journalisation côté client d’Analytics {#enable-analytics-client-side-logging}

Pour que la journalisation côté client Analytics soit activée pour votre mise en oeuvre, vous devez désactiver la configuration Adobe Analytics dans votre [datastream](../../../../datastreams/overview.md).

![Configuration de la banque de données Analytics désactivée](../assets/disable-analytics-datastream.png)

### Récupération [!DNL A4T] données du SDK et les envoyer à Analytics {#a4t-to-analytics}

Pour que cette méthode de création de rapports fonctionne correctement, vous devez envoyer la variable [!DNL A4T] données associées extraites du [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) dans l’accès Analytics.

Lorsque Target Edge calcule une réponse de proposition, il vérifie si la journalisation côté client Analytics est activée (c’est-à-dire si Analytics est désactivé dans votre flux de données). Si la journalisation côté client est activée, le système ajoute un jeton Analytics à chaque proposition de la réponse.

Le flux ressemble à ceci :

![Flux de journalisation côté client](../assets/analytics-client-side-logging.png)

Voici un exemple d’une `interact` réponse lorsque la journalisation côté client Analytics est activée. Si la proposition concerne une activité qui possède un rapport Analytics, elle aura une `scopeDetails.characteristics.analyticsToken` .

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Les propositions pour les activités du compositeur d’expérience d’après les formulaires peuvent contenir à la fois du contenu et des éléments de mesure de clic sous la même proposition. Par conséquent, au lieu d’avoir un seul jeton d’analyse pour l’affichage du contenu dans `scopeDetails.characteristics.analyticsToken` , un jeton d’analyse des clics et un jeton d’affichage peuvent être spécifiés dans la propriété `scopeDetails.characteristics.analyticsDisplayToken` et `scopeDetails.characteristics.analyticsClickToken` propriétés, en conséquence.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Toutes les valeurs de `scopeDetails.characteristics.analyticsToken`, ainsi que `scopeDetails.characteristics.analyticsDisplayToken` (pour le contenu affiché) et `scopeDetails.characteristics.analyticsClickToken` (pour les mesures des clics) sont les payloads A4T qui doivent être collectées et incluses comme `tnta` dans la balise [API d’insertion de données](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) appelez .

>[!IMPORTANT]
>
>La variable `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` Les propriétés peuvent contenir plusieurs jetons, concaténés en une seule chaîne délimitée par des virgules.
>
>Dans les exemples d’implémentation fournis dans la section suivante, plusieurs jetons Analytics sont collectés de manière itérative. Pour concaténer un tableau de jetons Analytics, utilisez une fonction similaire à celle-ci :
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Exemples d’implémentation {#implementation-examples}

Les sous-sections suivantes montrent comment mettre en oeuvre la journalisation côté client d’Analytics pour les cas d’utilisation courants.

### Activités du compositeur d’expérience d’après les formulaires {#form-based-composer}

Vous pouvez utiliser le SDK Web pour contrôler l’exécution des propositions depuis [Compositeur d’expérience d’après les formulaires Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr) activités.

Lorsque vous demandez des propositions pour une portée de décision spécifique, la proposition renvoyée contient son jeton Analytics approprié. La bonne pratique consiste à enchaîner le SDK Web de Platform. `sendEvent` et effectuer une itération sur les propositions renvoyées afin de les exécuter lors de la collecte simultanée des jetons Analytics.

Vous pouvez déclencher une `sendEvent` pour une portée d’activité du compositeur d’expérience d’après les formulaires telle que celle-ci :

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

À partir de là, vous devez implémenter du code pour exécuter les propositions et construire une payload qui sera finalement envoyée à Analytics. Voici un exemple de ce que `results.propositions` peut contenir :

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

Pour extraire le jeton Analytics d’une proposition avec des éléments de contenu, vous pouvez implémenter une fonction similaire à celle-ci :

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Une proposition peut avoir différents types d&#39;éléments, comme indiqué par le `schema` de l’élément en question. Quatre schémas d’éléments de proposition sont pris en charge pour les activités du compositeur d’expérience d’après les formulaires :

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` et `JSON_SCHEMA` sont les schémas qui reflètent le type de l’offre, tandis que `MEASUREMENT_SCHEMA` reflète les mesures qui doivent être jointes à un élément DOM.

Les payloads Analytics pour les mesures de clics doivent être collectées et envoyées à Analytics séparément des éléments de contenu, au moment où le visiteur clique réellement sur le contenu affiché précédemment.

La fonction d’assistance suivante pour obtenir les payloads de mesure de clics A4T s’avère pratique dans ce cas :

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Résumé de l’implémentation {#implementation-summary}

En résumé, les étapes suivantes doivent être exécutées lors de l’application d’activités du compositeur d’expérience d’après les formulaires avec le SDK Web Platform :

1. Envoyez un événement qui récupère les offres d’activité du compositeur d’expérience d’après les formulaires ;
1. appliquer les modifications de contenu à la page ;
1. Envoyez la variable `decisioning.propositionDisplay` événement de notification ;
1. Collectez les jetons d’affichage Analytics à partir de la réponse du SDK et créez un payload pour l’accès Analytics ;
1. Envoyez la payload à Analytics à l’aide de la variable [API d’insertion de données](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. S’il existe des mesures de clics dans les propositions diffusées, les écouteurs de clics doivent être configurés de sorte que lorsqu’un clic est effectué, l’événement envoie la variable `decisioning.propositionInteract` événement de notification . La variable `onBeforeEventSend` Le gestionnaire doit être configuré de sorte que lors de l’interception `decisioning.propositionInteract` , les actions suivantes se produisent :
   1. Collecte des jetons Analytics de clic `xdm._experience.decisioning.propositions`
   1. Envoi de l’accès de clic Analytics avec la charge utile Analytics collectée via [API d’insertion de données](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Activités du compositeur d’expérience visuelle {#visual-experience-composer-acitivties}

Le SDK Web vous permet de gérer les offres qui ont été créées à l’aide de [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>Les étapes de mise en oeuvre de ce cas pratique sont très similaires aux étapes de la [Activités du compositeur d’expérience d’après les formulaires](#form-based-composer). Veuillez consulter la section précédente pour plus de détails.

Lorsque le rendu automatique est activé, vous pouvez collecter les jetons Analytics à partir des propositions qui ont été exécutées sur la page. La bonne pratique consiste à enchaîner le SDK Web de Platform. `sendEvent` et effectuer une itération sur les propositions renvoyées afin de filtrer celles que le SDK Web a tenté d’effectuer.

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Utilisation `onBeforeEventSend` pour gérer les mesures de page {#using-onbeforeeventsend}

À l’aide des activités Adobe Target, vous pouvez configurer différentes mesures sur la page, soit associées manuellement au DOM, soit associées automatiquement au DOM (activités créées par le VEC). Les deux types sont une interaction différée entre l’utilisateur final et la page web.

Pour en tenir compte, la bonne pratique consiste à collecter les charges utiles Analytics à l’aide de la variable `onBeforeEventSend` crochet du SDK Web de Adobe Experience Platform. La variable `onBeforeEventSend` hook doit être configuré à l’aide de la variable `configure` et seront reflétés dans tous les événements envoyés par le biais du flux de données.

Voici un exemple de la manière dont `onBeforeEventSent` peut être configuré pour déclencher des accès Analytics :

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Étapes suivantes {#next-steps}

Ce guide décrit la journalisation côté client des données A4T dans le SDK Web. Consultez le guide sur la [journalisation côté serveur](server-side.md) pour plus d’informations sur la gestion des données A4T sur le réseau Edge.

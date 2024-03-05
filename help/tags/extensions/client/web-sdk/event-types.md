---
title: Types d’événement dans l’extension SDK Web Adobe Experience Platform
description: Découvrez comment utiliser les types d’événements fournis par l’extension SDK Web Adobe Experience Platform dans Adobe Experience Platform Launch.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# Types d’événements 

Cette page décrit les types d’événements Adobe Experience Platform fournis par l’extension de balise du SDK Web de Adobe Experience Platform. Ils sont utilisés pour [règles de création](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) et ne doit pas être confondu avec la variable `eventType` dans le champ [`xdm` objet](/help/web-sdk/commands/sendevent/xdm.md).

## [!UICONTROL Envoi de l’événement terminé]

En règle générale, votre propriété comporte une ou plusieurs règles utilisant la variable [[!UICONTROL Envoyer un événement] action](action-types.md#send-event) pour envoyer des événements à Adobe Experience Platform Edge Network. Chaque fois qu’un événement est envoyé à Edge Network, une réponse est renvoyée au navigateur avec des données utiles. Sans le [!UICONTROL Envoi de l’événement terminé] type d’événement , vous n’auriez pas accès à ces données renvoyées.

Pour accéder aux données renvoyées, créez une règle distincte, puis ajoutez une [!UICONTROL Envoi de l’événement terminé] à la règle. Cette règle est déclenchée chaque fois qu’une réponse réussie est reçue du serveur suite à une [!UICONTROL Envoyer un événement] action.

Lorsqu’une [!UICONTROL Envoi de l’événement terminé] déclenche une règle, il fournit les données renvoyées par le serveur qui peuvent s’avérer utiles pour accomplir certaines tâches. En règle générale, vous ajouterez une [!UICONTROL Code personnalisé] (de l’objet [!UICONTROL Core] ) à la même règle que celle qui contient la variable [!UICONTROL Envoi de l’événement terminé] . Dans le [!UICONTROL Code personnalisé] , votre code personnalisé aura accès à une variable nommée `event`. Ceci `event` contient les données renvoyées par le serveur.

Votre règle de gestion des données renvoyées par Edge Network peut ressembler à ceci :

![](assets/send-event-complete.png)

Vous trouverez ci-dessous quelques exemples d’exécution de certaines tâches à l’aide de la fonction [!UICONTROL Code personnalisé] dans cette règle.

### Rendu manuel du contenu personnalisé

Dans l’action Custom Code (Code personnalisé) de la règle pour le traitement des données de réponse, vous pouvez accéder aux propositions de personnalisation renvoyées par le serveur. Pour ce faire, saisissez le code personnalisé suivant :

```javascript
var propositions = event.propositions;
```

If `event.propositions` existe, il s’agit d’un tableau contenant des objets de proposition de personnalisation. Les propositions incluses dans le tableau sont déterminées, en grande partie, par la manière dont l’événement a été envoyé au serveur.

Pour ce premier scénario, supposons que vous n’ayez pas coché la variable [!UICONTROL Rendu des décisions] , mais n’ont fourni aucun [!UICONTROL portées de décision] dans la variable [!UICONTROL Envoyer un événement] l’action responsable de l’envoi de l’événement.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

Dans cet exemple, la variable `propositions` contient uniquement les propositions relatives à l’événement qui peuvent faire l’objet d’un rendu automatique.

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
    "renderAttempted": false
  }
]
```

Lors de l’envoi de l’événement, la variable [!UICONTROL Rendu des décisions] n’étant pas cochée, le SDK n’a pas tenté d’afficher automatiquement le contenu. Cependant, le SDK a toujours récupéré automatiquement le contenu éligible au rendu automatique et vous a fourni le rendu manuel si vous le souhaitez. Notez que chaque objet de proposition a son `renderAttempted` définie sur `false`.

Si vous avez plutôt coché la variable [!UICONTROL Rendu des décisions] lors de l’envoi de l’événement, le SDK aurait tenté d’effectuer le rendu de toutes les propositions éligibles pour le rendu automatique. Par conséquent, chaque objet de proposition aurait sa `renderAttempted` définie sur `true`. Dans ce cas, il n’est pas nécessaire de générer manuellement ces propositions.

Jusqu’à présent, vous n’avez examiné que le contenu de personnalisation éligible au rendu automatique (par exemple, tout contenu créé dans le compositeur d’expérience visuelle Adobe Target). Pour récupérer un contenu de personnalisation _not_ éligible au rendu automatique, demandez le contenu en fournissant des portées de décision à l’aide de la variable [!UICONTROL Portées de décision] dans le champ [!UICONTROL Envoyer un événement] action. Une portée est une chaîne qui identifie une proposition particulière que vous souhaitez récupérer du serveur.

La variable [!UICONTROL Envoyer un événement] L’action se présenterait comme suit :

![img.png](assets/send-event-render-unchecked-with-scopes.png)

Dans cet exemple, si des propositions sont trouvées sur le serveur correspondant au `salutation` ou `discount` , elles sont renvoyées et incluses dans la variable `propositions` tableau. Gardez à l’esprit que les propositions admissibles au rendu automatique continueront à être incluses dans la variable `propositions` , quelle que soit la manière dont vous configurez la variable [!UICONTROL Rendu des décisions] ou [!UICONTROL Portées de décision] dans le champ [!UICONTROL Envoyer un événement] action. La variable `propositions` dans ce cas, le tableau ressemble à l’exemple suivant :

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
    "renderAttempted": false
  }
]
```

À ce stade, vous pouvez générer le contenu des propositions à votre gré. Dans cet exemple, la proposition correspondant au `discount` scope est une proposition de HTML créée à l’aide du compositeur d’expérience d’après les formulaires Adobe Target. Supposons que votre page comporte un élément avec l’identifiant de `daily-special` et souhaitez effectuer le rendu du contenu à partir de la fonction `discount` dans la `daily-special` élément . Procédez comme suit :

1. Extraire les propositions des `event` .
1. Parcourez chaque proposition, en recherchant la proposition avec un périmètre de `discount`.
1. Si vous trouvez une proposition, passez en boucle chaque élément de la proposition, recherchant l’élément qui est le contenu HTML. (Mieux vaut vérifier que supposer.)
1. Si vous trouvez un élément contenant du contenu de HTML, recherchez la variable `daily-special` sur la page et remplacez son HTML par le contenu personnalisé.

Votre code personnalisé dans le [!UICONTROL Code personnalisé] peut se présenter comme suit :

```javascript
var propositions = event.propositions;

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
      break;
    }
  }
}

if (discountHtml) {
  // Discount HTML exists. Time to render it.
  var dailySpecialElement = document.getElementById("daily-special");
  dailySpecialElement.innerHTML = discountHtml;
}
```

### Accès aux jetons de réponse Adobe Target

Le contenu de personnalisation renvoyé par Adobe Target inclut [jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), qui sont des détails sur l’activité, l’offre, l’expérience, le profil utilisateur, les informations géographiques, etc. Ces détails peuvent être partagés avec des outils tiers ou utilisés pour le débogage. Les jetons de réponse peuvent être configurés dans l’interface utilisateur d’Adobe Target.

Dans l’action Custom Code (Code personnalisé) de la règle pour le traitement des données de réponse, vous pouvez accéder aux propositions de personnalisation renvoyées par le serveur. Pour ce faire, saisissez le code personnalisé suivant :

```javascript
var propositions = event.propositions;
```

If `event.propositions` existe, il s’agit d’un tableau contenant des objets de proposition de personnalisation. Voir [Rendu manuel du contenu personnalisé](#manually-render-personalized-content) pour plus d’informations sur le contenu de `result.propositions`.

Supposons que vous souhaitiez rassembler tous les noms d’activité de toutes les propositions automatiquement générées par le SDK web et les pousser dans un seul tableau. Vous pouvez ensuite envoyer le tableau unique à un tiers. Dans ce cas, écrivez du code personnalisé dans le [!UICONTROL Code personnalisé] Action vers :

1. Extraire les propositions des `event` .
1. Passez en revue chaque proposition.
1. Déterminez si le SDK a rendu la proposition.
1. Si tel est le cas, passez en boucle chaque élément de la proposition.
1. Récupérez le nom de l’activité à partir du `meta` , qui est un objet contenant des jetons de réponse.
1. Envoyez le nom de l’activité dans un tableau.
1. Envoyez les noms des activités à un tiers.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```

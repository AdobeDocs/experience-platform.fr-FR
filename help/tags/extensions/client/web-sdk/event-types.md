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

Cette page décrit les types d’événements Adobe Experience Platform fournis par l’extension de balise du SDK Web de Adobe Experience Platform. Ils sont utilisés pour [créer des règles](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html?lang=fr) et ne doivent pas être confondus avec le champ `eventType` de l’objet [`xdm`](/help/web-sdk/commands/sendevent/xdm.md).

## [!UICONTROL Envoyer l’événement terminé]

En règle générale, votre propriété comporte une ou plusieurs règles à l’aide de l’action [[!UICONTROL Envoyer l’événement]](action-types.md#send-event) pour envoyer des événements à l’Edge Network Adobe Experience Platform. Chaque fois qu’un événement est envoyé à l’Edge Network, une réponse est renvoyée au navigateur avec des données utiles. Sans le type d’événement [!UICONTROL Send event complete] , vous n’auriez pas accès à ces données renvoyées.

Pour accéder aux données renvoyées, créez une règle distincte, puis ajoutez un événement [!UICONTROL Send event complete] à la règle. Cette règle est déclenchée chaque fois qu’une réponse réussie est reçue du serveur suite à une action [!UICONTROL Send event].

Lorsqu’un événement [!UICONTROL Send event complete] déclenche une règle, il fournit les données renvoyées par le serveur qui peuvent s’avérer utiles pour accomplir certaines tâches. En règle générale, vous ajouterez une action [!UICONTROL Custom code] (de l’extension [!UICONTROL Core]) à la même règle qui contient l’événement [!UICONTROL Send event complete]. Dans l’action [!UICONTROL Custom code], votre code personnalisé aura accès à une variable nommée `event`. Cette variable `event` contiendra les données renvoyées par le serveur.

Votre règle de gestion des données renvoyées par l’Edge Network peut ressembler à ceci :

![](assets/send-event-complete.png)

Vous trouverez ci-dessous quelques exemples d’exécution de certaines tâches à l’aide de l’action [!UICONTROL Custom code] dans cette règle.

### Rendu manuel du contenu personnalisé

Dans l’action Custom Code (Code personnalisé) de la règle pour le traitement des données de réponse, vous pouvez accéder aux propositions de personnalisation renvoyées par le serveur. Pour ce faire, saisissez le code personnalisé suivant :

```javascript
var propositions = event.propositions;
```

Si `event.propositions` existe, il s’agit d’un tableau contenant des objets de proposition de personnalisation. Les propositions incluses dans le tableau sont déterminées, en grande partie, par la manière dont l’événement a été envoyé au serveur.

Pour ce premier scénario, supposons que vous n’ayez pas coché la case [!UICONTROL Render Decisions] et n’ayez fourni aucune [!UICONTROL portée de décision] dans l’action [!UICONTROL Envoyer l’événement] responsable de l’envoi de l’événement.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

Dans cet exemple, le tableau `propositions` contient uniquement les propositions liées à l’événement qui peuvent faire l’objet d’un rendu automatique.

Le tableau `propositions` peut ressembler à l’exemple suivant :

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

Lors de l’envoi de l’événement, la case à cocher [!UICONTROL Render Decisions] n’était pas cochée. Le SDK n’a donc pas tenté d’afficher automatiquement le contenu. Cependant, le SDK a toujours récupéré automatiquement le contenu éligible au rendu automatique et vous a fourni le rendu manuel si vous le souhaitez. Notez que la propriété `renderAttempted` de chaque objet de proposition est définie sur `false`.

Si vous aviez coché la case [!UICONTROL Render Decisions] lors de l’envoi de l’événement à la place, le SDK aurait tenté d’afficher toutes les propositions admissibles au rendu automatique. Par conséquent, la propriété `renderAttempted` de chaque objet de proposition est définie sur `true`. Dans ce cas, il n’est pas nécessaire de générer manuellement ces propositions.

Jusqu’à présent, vous n’avez examiné que le contenu de personnalisation éligible au rendu automatique (par exemple, tout contenu créé dans le compositeur d’expérience visuelle Adobe Target). Pour récupérer tout contenu de personnalisation _non_ éligible pour le rendu automatique, demandez le contenu en fournissant des portées de décision à l’aide du champ [!UICONTROL Portées de décision] dans l’action [!UICONTROL Envoyer l’événement]. Une portée est une chaîne qui identifie une proposition particulière que vous souhaitez récupérer du serveur.

L’action [!UICONTROL Envoyer l’événement] se présenterait comme suit :

![img.png](assets/send-event-render-unchecked-with-scopes.png)

Dans cet exemple, si des propositions sont trouvées sur le serveur correspondant à la portée `salutation` ou `discount`, elles sont renvoyées et incluses dans le tableau `propositions`. Gardez à l’esprit que les propositions admissibles au rendu automatique continueront à être incluses dans le tableau `propositions`, quelle que soit la manière dont vous configurez les champs [!UICONTROL Render Decisions] ou [!UICONTROL Decision scopes] dans l’action [!UICONTROL Envoyer l’événement]. Le tableau `propositions`, dans ce cas, ressemblerait à cet exemple :

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

À ce stade, vous pouvez générer le contenu des propositions à votre gré. Dans cet exemple, la proposition correspondant à la portée `discount` est une proposition d’HTML créée à l’aide du compositeur d’expérience d’après les formulaires Adobe Target. Supposons que vous ayez un élément sur votre page avec l’identifiant `daily-special` et que vous souhaitiez effectuer le rendu du contenu de la proposition `discount` vers l’élément `daily-special`. Procédez comme suit :

1. Extrayez les propositions de l’objet `event`.
1. Explorez chaque proposition, en recherchant la proposition dont la portée est de `discount`.
1. Si vous trouvez une proposition, passez en boucle chaque élément de la proposition, recherchant l’élément qui est le contenu HTML. (Mieux vaut vérifier que supposer.)
1. Si vous trouvez un élément contenant du contenu HTML, recherchez l’élément `daily-special` sur la page et remplacez son HTML par le contenu personnalisé.

Votre code personnalisé dans l&#39;action [!UICONTROL Custom code] peut se présenter comme suit :

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

Le contenu Personalization renvoyé par Adobe Target comprend des [jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), qui sont des détails sur l’activité, l’offre, l’expérience, le profil utilisateur, des informations géographiques, etc. Ces détails peuvent être partagés avec des outils tiers ou utilisés pour le débogage. Les jetons de réponse peuvent être configurés dans l’interface utilisateur d’Adobe Target.

Dans l’action Custom Code (Code personnalisé) de la règle pour le traitement des données de réponse, vous pouvez accéder aux propositions de personnalisation renvoyées par le serveur. Pour ce faire, saisissez le code personnalisé suivant :

```javascript
var propositions = event.propositions;
```

Si `event.propositions` existe, il s’agit d’un tableau contenant des objets de proposition de personnalisation. Pour plus d’informations sur le contenu de `result.propositions`, voir [Rendu manuel du contenu personnalisé](#manually-render-personalized-content) .

Supposons que vous souhaitiez rassembler tous les noms d’activité de toutes les propositions automatiquement générées par le SDK web et les pousser dans un seul tableau. Vous pouvez ensuite envoyer le tableau unique à un tiers. Dans ce cas, écrivez du code personnalisé dans l’action [!UICONTROL Custom code] pour :

1. Extrayez les propositions de l’objet `event`.
1. Passez en revue chaque proposition.
1. Déterminez si le SDK a rendu la proposition.
1. Si tel est le cas, passez en boucle chaque élément de la proposition.
1. Récupérez le nom de l’activité à partir de la propriété `meta`, qui est un objet contenant des jetons de réponse.
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

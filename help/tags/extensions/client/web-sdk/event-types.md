---
title: Types d’événements dans l’extension Adobe Experience Platform Web SDK
description: Découvrez comment utiliser les types d’événements fournis par l’extension Adobe Experience Platform Web SDK dans Adobe Experience Platform Launch.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 0%

---

# Types d’événements 

Cette page décrit les types d’événements Adobe Experience Platform fournis par l’extension de balise Adobe Experience Platform Web SDK. Ils sont utilisés pour [créer des règles](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html?lang=fr) et ne doivent pas être confondus avec le champ `eventType` dans l’objet [`xdm`](/help/collection/js/commands/sendevent/xdm.md).

## Déclenchement du hook de surveillance {#monitoring-hook-triggered}

Adobe Experience Platform Web SDK comprend des hooks de surveillance que vous pouvez utiliser pour surveiller divers événements système. Ces outils sont utiles pour développer vos propres outils de débogage et pour capturer les journaux Web SDK.

Pour plus d’informations sur les paramètres contenus dans chaque événement de hook de surveillance, consultez la documentation [Web SDK Monitoring Hooks](/help/collection/js/monitoring-hooks.md).

![Image de l’interface utilisateur des balises montrant le type d’événement de hook de surveillance](assets/monitoring-hook-triggered.png)

L’extension de balise Web SDK prend en charge les hooks de surveillance suivants :

* **[!UICONTROL onInstanceCreated]** : cet événement de hook de surveillance est déclenché lorsque vous avez réussi à créer une instance de Web SDK.
* **[!UICONTROL onInstanceConfigured]** : cet événement de hook de surveillance est déclenché par le Web SDK lorsque la commande [`configure`](/help/collection/js/commands/configure/overview.md) est résolue avec succès
* **[!UICONTROL onBeforeCommand]** : cet événement de hook de surveillance est déclenché par Web SDK avant l’exécution de toute autre commande. Vous pouvez utiliser ce hook de surveillance pour récupérer les options de configuration d’une commande spécifique.
* **[!UICONTROL onCommandResolved]** : cet événement de hook de surveillance est déclenché avant la résolution de la promesse de commande. Vous pouvez utiliser cette fonction pour afficher les options de commande et le résultat.
* **[!UICONTROL onCommandRejected]** : cet événement de hook de surveillance est déclenché lorsqu’une promesse de commande est rejetée et qu’il contient des informations sur la cause de l’erreur.
* **[!UICONTROL onBeforeNetworkRequest]** : cet événement de hook de surveillance est déclenché avant l&#39;exécution d&#39;une requête réseau.
* **[!UICONTROL onNetworkResponse]** : cet événement de hook de surveillance est déclenché lorsque le navigateur reçoit une réponse.
* **[!UICONTROL onNetworkError]** : cet événement de crochet de surveillance est déclenché lorsque la requête réseau a échoué.
* **[!UICONTROL onBeforeLog]** : cet événement de hook de surveillance est déclenché avant que le Web SDK ne consigne quoi que ce soit dans la console.
* **[!UICONTROL onContentRendering]** : cet événement de hook de surveillance est déclenché par le composant `personalization` et vous aide à déboguer le rendu du contenu de personnalisation. Cet événement peut avoir différents statuts :
   * `rendering-started` : indique que le Web SDK est sur le point de rendre des propositions. Avant que le SDK Web ne commence à effectuer le rendu d&#39;une portée de décision ou d&#39;une vue, dans l&#39;objet `data`, vous pouvez voir les propositions qui sont sur le point d&#39;être effectuées par le composant `personalization` et le nom de la portée.
   * `no-offers` : indique qu&#39;aucune payload n&#39;a été reçue pour les paramètres demandés.
   * `rendering-failed` : indique que Web SDK n’a pas réussi à effectuer le rendu d’une proposition.
   * `rendering-succeeded` : indique que le rendu est terminé pour une portée de décision.
   * `rendering-redirect` : indique que Web SDK va exécuter une proposition de redirection.
* **[!UICONTROL onContentHiding]** : cet événement de crochet de surveillance est déclenché lorsqu’un style de masquage préalable est appliqué ou supprimé.


## [!UICONTROL Send event complete]

En règle générale, votre propriété comporte une ou plusieurs règles utilisant l’action [[!UICONTROL Send event]](actions/send-event.md) pour envoyer des événements à Adobe Experience Platform Edge Network. Chaque fois qu’un événement est envoyé à Edge Network, une réponse est renvoyée au navigateur avec des données utiles. Sans le type d’événement [!UICONTROL Send event complete], vous n’auriez pas accès à ces données renvoyées.

Pour accéder aux données renvoyées, créez une règle distincte, puis ajoutez un événement [!UICONTROL Send event complete] à la règle. Cette règle est déclenchée chaque fois qu’une réponse réussie est reçue du serveur à la suite d’une action [!UICONTROL Send event].

Lorsqu’un événement [!UICONTROL Send event complete] déclenche une règle, il fournit des données renvoyées par le serveur qui peuvent être utiles pour accomplir certaines tâches. En règle générale, vous ajoutez une action [!UICONTROL Custom code] (à partir de l’extension [!UICONTROL Core]) à la même règle que celle qui contient l’événement [!UICONTROL Send event complete]. Dans l’action [!UICONTROL Custom code], votre code personnalisé aura accès à une variable nommée `event`. Cette variable `event` contiendra les données renvoyées par le serveur.

Voici à quoi pourrait ressembler votre règle de gestion des données renvoyées par Edge Network :

![](assets/send-event-complete.png)

Vous trouverez ci-dessous quelques exemples d’exécution de certaines tâches à l’aide de l’action [!UICONTROL Custom code] dans cette règle.

### Rendu manuel de contenu personnalisé

Dans l’action Code personnalisé, qui se trouve dans la règle de gestion des données de réponse, vous pouvez accéder aux propositions de personnalisation renvoyées par le serveur. Pour ce faire, vous devez saisir le code personnalisé suivant :

```javascript
var propositions = event.propositions;
```

Si `event.propositions` existe, il s’agit d’un tableau contenant des objets de proposition de personnalisation. Les propositions incluses dans le tableau sont déterminées, en grande partie, par la manière dont l’événement a été envoyé au serveur.

Pour ce premier scénario, supposons que vous n’ayez pas coché la case [!UICONTROL Render decisions] et que vous n’ayez fourni aucune [!UICONTROL decision scopes] dans l’action [!UICONTROL Send event] responsable de l’envoi de l’événement.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

Dans cet exemple, le tableau `propositions` ne contient que des propositions liées à l’événement qui sont éligibles au rendu automatique.

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

Lors de l’envoi de l’événement, la case à cocher [!UICONTROL Render decisions] n’était pas cochée. Par conséquent, le SDK n’a pas tenté d’effectuer automatiquement le rendu d’un contenu. Cependant, le SDK a toujours récupéré automatiquement le contenu éligible au rendu automatique et vous l’a fourni pour qu’il soit rendu manuellement si vous le souhaitez. Notez que la propriété `renderAttempted` de chaque objet de proposition est définie sur `false`.

Si, à la place, vous aviez coché la case [!UICONTROL Render decisions] lors de l’envoi de l’événement, le SDK aurait tenté de rendre toutes les propositions éligibles au rendu automatique. Par conséquent, la propriété `renderAttempted` de chacun des objets de proposition est définie sur `true`. Dans ce cas, il n’est pas nécessaire d’effectuer manuellement le rendu de ces propositions.

Jusqu’à présent, vous n’avez examiné que le contenu de personnalisation éligible au rendu automatique (par exemple, tout contenu créé dans le compositeur d’expérience visuelle d’Adobe Target). Pour récupérer un contenu de personnalisation _non éligible_ au rendu automatique, demandez le contenu en fournissant des portées de décision à l’aide du champ [!UICONTROL Decision scopes] dans l’action [!UICONTROL Send event]. Une portée est une chaîne qui identifie une proposition particulière que vous souhaitez récupérer à partir du serveur.

L’action [!UICONTROL Send event] se présenterait comme suit :

![img.png](assets/send-event-render-unchecked-with-scopes.png)

Dans cet exemple, si des propositions sont trouvées sur le serveur correspondant à la portée `salutation` ou `discount`, elles sont renvoyées et incluses dans le tableau `propositions` . N’oubliez pas que les propositions qui remplissent les critères du rendu automatique continueront à être incluses dans le tableau `propositions`, quelle que soit la manière dont vous configurez les champs [!UICONTROL Render decisions] ou [!UICONTROL Decision scopes] dans l’action [!UICONTROL Send event]. Le tableau `propositions`, dans ce cas, ressemble à cet exemple :

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

À ce stade, vous pouvez effectuer le rendu du contenu de proposition comme vous le souhaitez. Dans cet exemple, la proposition correspondant à la portée `discount` est une proposition HTML créée à l’aide du compositeur d’expérience d’après les formulaires d’Adobe Target. Supposons que vous ayez un élément sur votre page avec l’identifiant de `daily-special` et que vous souhaitiez effectuer le rendu du contenu de la proposition de `discount` dans l’élément de `daily-special`. Procédez comme suit :

1. Extrayez des propositions de l’objet `event`.
1. Parcourez chaque proposition en recherchant la proposition avec une portée de `discount`.
1. Si vous trouvez une proposition, parcourez chaque élément de la proposition, en recherchant l’élément correspondant au contenu HTML. (Mieux vaut vérifier que supposer.)
1. Si vous trouvez un élément contenant du contenu HTML, recherchez l’élément `daily-special` sur la page et remplacez son HTML par le contenu personnalisé.

Votre code personnalisé dans l’action [!UICONTROL Custom code] peut se présenter comme suit :

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

Le contenu Personalization renvoyé par Adobe Target comprend des [jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), qui sont des détails sur l’activité, l’offre, l’expérience, le profil utilisateur, les informations géographiques, etc. Ces informations peuvent être partagées avec des outils tiers ou utilisées à des fins de débogage. Les jetons de réponse peuvent être configurés dans l’interface utilisateur d’Adobe Target.

Dans l’action Code personnalisé, qui se trouve dans la règle de gestion des données de réponse, vous pouvez accéder aux propositions de personnalisation renvoyées par le serveur. Pour ce faire, saisissez le code personnalisé suivant :

```javascript
var propositions = event.propositions;
```

Si `event.propositions` existe, il s’agit d’un tableau contenant des objets de proposition de personnalisation. Voir [Rendu manuel de contenu personnalisé](#manually-render-personalized-content) pour plus d’informations sur le contenu des `result.propositions`.

Supposons que vous souhaitiez rassembler tous les noms d’activité de toutes les propositions qui ont été automatiquement rendues par le SDK web et les pousser dans un seul tableau. Vous pouvez ensuite envoyer le tableau unique à un tiers. Dans ce cas, écrivez du code personnalisé dans l’action [!UICONTROL Custom code] pour :

1. Extrayez des propositions de l’objet `event`.
1. Parcourez chaque proposition en boucle.
1. Déterminez si le SDK a rendu la proposition.
1. Si tel est le cas, parcourez chaque élément de la proposition.
1. Récupérez le nom de l’activité à partir de la propriété `meta` , qui est un objet contenant des jetons de réponse.
1. Placez le nom de l’activité dans un tableau.
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

## [!UICONTROL Subscribe ruleset items] {#subscribe-ruleset-items}

Le type d’événement **[!UICONTROL Subscribe ruleset items]** vous permet de vous abonner à des cartes de contenu Adobe Journey Optimizer pour une surface. Chaque fois que les ensembles de règles sont évalués, le rappel fourni à cette commande reçoit un objet de résultat avec des propositions qui contiennent les données de la carte de contenu.

![Image de l’interface utilisateur des balises Experience Platform affichant le type d’événement d’éléments d’ensemble de règles S’abonner.](assets/subscribe-ruleset-items.png)

Ce type d’événement prend en charge les propriétés configurables suivantes :

* **[!UICONTROL Schemas]** : tableau de schémas pour lesquels vous souhaitez vous abonner aux cartes de contenu. Vous pouvez saisir les schémas manuellement ou en fournissant un élément de données.
* **[!UICONTROL Surfaces]** : tableau de surfaces pour lesquelles vous souhaitez vous abonner à des cartes de contenu. Vous pouvez saisir les surfaces manuellement ou en fournissant un élément de données.

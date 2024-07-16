---
title: Accès aux jetons de réponse à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment accéder aux jetons de réponse à l’aide du SDK Web de Adobe Experience Platform.
keywords: personnalisation;target;adobe target;renderDecisions;sendEvent;décisionScopes;result.requests,jetons de réponse;
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---

# Accès aux jetons de réponse

Le contenu Personalization renvoyé par Adobe Target comprend des [jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), qui sont des détails sur l’activité, l’offre, l’expérience, le profil utilisateur, des informations géographiques, etc. Ces détails peuvent être partagés avec des outils tiers ou utilisés pour le débogage. Les jetons de réponse peuvent être configurés dans l’interface utilisateur d’Adobe Target.

Pour accéder à tout contenu de personnalisation, fournissez une fonction de rappel lors de l’envoi d’un événement. Ce rappel sera appelé une fois que le SDK aura reçu une réponse réussie du serveur. Votre rappel reçoit un objet `result` qui peut contenir une propriété `propositions` contenant tout contenu de personnalisation renvoyé. Vous trouverez ci-dessous un exemple de fonction de rappel.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

Dans cet exemple, `result.propositions`, s&#39;il existe, est un tableau contenant des propositions de personnalisation liées à l&#39;événement. Pour plus d’informations sur le contenu de `result.propositions`, voir [Rendering personalization content](../rendering-personalization-content.md) .

Supposons que vous souhaitiez rassembler tous les noms d’activité de toutes les propositions automatiquement générées par le SDK web et les placer dans un seul tableau. Vous pouvez ensuite envoyer le tableau unique à un tiers. Dans ce cas :

1. Extrayez les propositions de l’objet `result`.
1. Passez en revue chaque proposition.
1. Déterminez si le SDK a rendu la proposition.
1. Si tel est le cas, passez en boucle chaque élément de la proposition.
1. Récupérez le nom de l’activité à partir de la propriété `meta`, qui est un objet contenant des jetons de réponse.
1. Envoyez le nom de l’activité dans un tableau.
1. Envoyez les noms des activités à un tiers.

Votre code se présenterait comme suit :

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
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
  });
```

---
title: ' de suivi'
seo-title: 'Suivi du SDK Web d’Adobe Experience Platform '
description: 'Découvrez comment effectuer le suivi du SDK Web de la plateforme d’expérience '
seo-description: 'Découvrez comment effectuer le suivi du SDK Web de la plateforme d’expérience '
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


#  de suivi

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Pour envoyer des données  à Adobe Experience Cloud, utilisez la `event` commande. La `event` commande est le principal moyen d’envoyer des données à Experience Cloud et de récupérer le contenu personnalisé, les identités et les  destinations  du.

Les données envoyées à Adobe Experience Cloud se répartissent en deux  :

* Données XDM
* Données non XDM (actuellement non prises en charge)

## Envoi de données XDM

Les données XDM sont un objet dont le contenu et la structure correspondent à un que vous avez créé dans Adobe Experience Platform. [En savoir plus sur la création d’un  de.](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md)

Les données XDM que vous souhaitez intégrer à vos analyses, à votre personnalisation, à vos  ou à vos destinations doivent être envoyées à l’aide de l’ `xdm` option.

```javascript
alloy("event", {
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

### Envoi de données non XDM

Actuellement, l’envoi de données qui ne correspondent pas à une  XDM n’est pas pris en charge. Le soutien est prévu pour une date ultérieure.

### Paramètre `eventType`

Dans un  d’expérience XDM, il existe un `eventType` champ. Il contient le  principal pour l’enregistrement. Vous pouvez le transmettre dans le cadre de l’ `xdm` option.

```javascript
alloy("event", {
  "xdm": {
    "eventType": "commerce.purchases",
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

Vous pouvez également `eventType` transmettre la commande  à l’aide de l’ `type` option. En arrière-plan, ceci est ajouté aux données XDM. L’option `type` as permet de définir plus facilement le `eventType` sans avoir à modifier la charge utile XDM.

```javascript
var myXDMData = { ... };

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Démarrage d’un 

Lorsqu’un a démarré, il est important d’en informer le SDK en le définissant `viewStart` sur `true` la `event` commande. Cela indique, entre autres, que le kit SDK doit récupérer et générer du contenu personnalisé. Même si vous n’utilisez pas la personnalisation actuellement, elle simplifie considérablement l’activation de la personnalisation ou d’autres fonctionnalités ultérieurement, car vous n’aurez pas à modifier le code de la page. En outre, le suivi des  de est bénéfique lors de l’affichage des rapports d’analyse une fois les données collectées.

La définition d’un  peut dépendre du contexte.

* Sur un site Web ordinaire, chaque page Web est généralement considérée comme un  unique. Dans ce cas, un dont la `viewStart` valeur est `true` doit être exécuté le plus tôt possible en haut de la page.
* Dans une application \(SPA\) d’une seule page, un  de est moins défini. Cela signifie généralement que l’utilisateur a navigué dans l’application et que la plupart du contenu a changé. Pour ceux qui connaissent bien les fondements techniques des applications d’une seule page, c’est généralement le cas lorsque l’application charge une nouvelle route. Chaque fois qu’un utilisateur se rend dans un nouveau, quelle que soit la manière dont vous choisissez de définir un __ de, un `viewStart` avec `true` défini sur doit être exécuté.

Le  avec `viewStart` défini sur `true` est le mécanisme principal pour envoyer des données à Adobe Experience Cloud et demander du contenu à Adobe Experience Cloud. Voici comment vous  un de  :

```javascript
alloy("event", {
  "viewStart": true,
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

Une fois les données envoyées, le serveur répond par un contenu personnalisé, entre autres. Ce contenu personnalisé est automatiquement rendu dans votre  de. Les gestionnaires de liens sont également automatiquement associés au nouveau contenu  du.

## Utilisation de l’API sendBeacon

Il peut s’avérer difficile d’envoyer des données  juste avant que l’utilisateur de la page Web ne s’en soit éloigné. Si la requête prend trop de temps, le navigateur peut annuler la requête. Certains navigateurs ont mis en oeuvre une API standard Web appelée `sendBeacon` pour permettre la collecte plus facile des données pendant cette période. Lors de `sendBeacon`l’utilisation, le navigateur effectue la requête Web dans le contexte de navigation globale. Cela signifie que le navigateur effectue la demande de balise en arrière-plan et ne maintient pas la navigation dans la page. Pour indiquer au SDK Web d’Adobe Experience Platform de l’utiliser `sendBeacon`, ajoutez l’option `"documentUnloading": true` à la commande  du.  Voici un exemple :

```javascript
alloy("event", {
  "documentUnloading": true,
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

Les navigateurs ont imposé des limites à la quantité de données pouvant être envoyées `sendBeacon` simultanément. Dans de nombreux navigateurs, la limite est de 64 Ko. Si le navigateur rejette l’ du fait que la charge utile est trop importante, le SDK Web d’Adobe Experience Platform revient à utiliser sa méthode de transport normale (par exemple, récupérer).

## Gestion des réponses des 

Si vous souhaitez gérer une réponse d’un , vous pouvez être averti d’un succès ou d’un échec comme suit :

```javascript
alloy("event", {
  "viewStart": true,
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
}).then(function() {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Modification des  de globalement {#modifying-events-globally}

Si vous souhaitez ajouter, supprimer ou modifier des champs du  global, vous pouvez configurer un `onBeforeEventSend` rappel.  Ce rappel est appelé chaque fois qu’un est envoyé.  Ce rappel est transmis dans un objet  avec un `xdm` champ.  Modifiez `event.xdm` les données envoyées dans le  du.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` sont définis dans l’ordre suivant :

1. Valeurs transmises sous forme d’options à la commande `alloy("event", { xdm: ... });`
2. Valeurs collectées automatiquement.  (voir Informations [](../reference/automatic-information.md)automatiques).
3. Modifications apportées dans le `onBeforeEventSend` rappel.

Si le `onBeforeEventSend` rappel renvoie une exception, le  du est toujours envoyé ; toutefois, aucune des modifications apportées dans le rappel n’est appliquée au  final du.

## Erreurs exploitables potentielles

Lors de l’envoi d’un , une erreur peut être générée si les données envoyées sont trop volumineuses (plus de 32 Ko pour la requête complète). Dans ce cas, vous devez réduire la quantité de données envoyées.

Lorsque le débogage est activé, le serveur valide de manière synchrone  données envoyées par rapport au XDM configuré. Si les données ne correspondent pas à la  du, les détails sur la non-correspondance sont renvoyés par le serveur et une erreur est générée. Dans ce cas, modifiez les données pour qu’elles correspondent au  du. Lorsque le débogage n’est pas activé, le serveur valide les données de manière asynchrone et, par conséquent, aucune erreur correspondante n’est générée.

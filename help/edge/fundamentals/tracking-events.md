---
title: Suivi des événements
seo-title: Suivi des événements du SDK Web d’Adobe Experience Platform
description: Découvrez la procédure de suivi des événements du SDK Web d’Experience Platform
seo-description: Découvrez la procédure de suivi des événements du SDK Web d’Experience Platform
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 97%

---


# Suivi des événements

Pour envoyer des données d’événement à Adobe Experience Cloud, utilisez la commande `event`. La commande `event` constitue le principal moyen pour envoyer des données à Experience Cloud et pour récupérer du contenu personnalisé, des identités et des destinations d’audience.

Les données envoyées à Adobe Experience Cloud entrent dans deux catégories :

* Données XDM
* Données autres que XDM (actuellement non prises en charge)

## Envoi de données XDM

Les données XDM sont un objet dont le contenu et la structure correspondent à un schéma que vous avez créé dans Adobe Experience Platform. [En savoir plus sur la création d’un schéma.](../../xdm/tutorials/create-schema-ui.md)

Les données XDM que vous souhaitez intégrer à vos analyses, à votre personnalisation, à vos audiences ou à vos destinations doivent être envoyées à l’aide de l’option `xdm`.

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

>[!NOTE]
>Les données pouvant être envoyées dans chaque événement du champ XDM sont limitées à 32 Ko.

### Envoi de données autres que XDM

Actuellement, l’envoi de données qui ne correspondent pas à un schéma XDM n’est pas pris en charge. La prise en charge est prévue pour une date ultérieure.

### Définition de `eventType`

Dans un événement d’expérience XDM, il existe un champ `eventType`. Il contient le type d’événement principal pour l’enregistrement. Vous pouvez le transmettre comme faisant partie de l’option `xdm`.

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

Vous pouvez également transmettre `eventType` dans la commande d’événement à l’aide de l’option `type`. Cela est ajouté aux données XDM en arrière-plan. Disposer de `type` comme option permet de définir plus facilement `eventType` sans avoir à modifier la charge utile XDM.

```javascript
var myXDMData = { ... };

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

## Utilisation de l’API sendBeacon

Il peut s’avérer difficile d’envoyer des données d’événement juste avant que l’utilisateur ne quitte une page web. Si la requête prend trop de temps, le navigateur peut l’annuler. Certains navigateurs ont implémenté une API web appelée `sendBeacon` pour faciliter la collecte des données pendant cette période. Lors de l’utilisation de `sendBeacon`, le navigateur effectue la demande web dans le contexte de navigation globale. Cela signifie que le navigateur effectue la demande de balise en arrière-plan et n’interrompt pas la navigation dans la page. Pour indiquer au SDK Web d’Adobe Experience Platform d’utiliser `sendBeacon`, ajoutez l’option `"documentUnloading": true` à la commande d’événement.  Voici un exemple :

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

Les navigateurs ont imposé des limites à la quantité de données pouvant être simultanément envoyées avec `sendBeacon`. Dans de nombreux navigateurs, la limite est de 64 Ko. Si le navigateur rejette l’événement parce que la charge utile est trop importante, le SDK Web d’Adobe Experience Platform recommence à utiliser sa méthode de transport normale (par exemple, la récupération).

## Gestion des réponses d’événements

Si vous souhaitez gérer une réponse d’un événement, vous pouvez être averti d’un succès ou d’un échec de la manière suivante :

```javascript
alloy("event", {
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
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Modification globale des événements {#modifying-events-globally}

Si vous souhaitez ajouter, supprimer ou modifier des champs d’événements globalement, vous pouvez configurer un rappel `onBeforeEventSend`.  Ce rappel est appelé chaque fois qu’un événement est envoyé.  Il est transmis dans un objet d’événement avec un champ `xdm`.  Modifiez `event.xdm` pour changer les données envoyées dans l’événement.

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

Les champs `xdm` sont définis dans l’ordre suivant :

1. Valeurs transmises sous forme d’options à la commande d’événement `alloy("event", { xdm: ... });`
2. Valeurs collectées automatiquement  (voir [Informations automatiques](../reference/automatic-information.md))
3. Modifications apportées dans le rappel `onBeforeEventSend`

Si le rappel `onBeforeEventSend` renvoie une exception, l’événement est toujours envoyé ; toutefois, aucune des modifications apportées dans le rappel n’est appliquée à l’événement final.

## Erreurs potentielles

Lors de l’envoi d’un événement, une erreur peut être générée si les données envoyées sont trop volumineuses (plus de 32 Ko pour la requête complète). Dans ce cas, vous devez réduire la quantité de données envoyées.

Lorsque le débogage est activé, le serveur valide de manière synchrone les données d’événement envoyées par rapport au schéma XDM configuré. Si les données ne correspondent pas au schéma, les détails sur la discordance sont renvoyés par le serveur et une erreur est générée. Dans ce cas, modifiez les données pour qu’elles correspondent au schéma. Lorsque le débogage n’est pas activé, le serveur valide les données de manière asynchrone et, par conséquent, aucune erreur correspondante n’est générée.

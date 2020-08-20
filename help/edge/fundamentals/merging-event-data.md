---
title: Fusion de données d’événement
seo-title: Fusion des données d’événement du SDK Web d’Adobe Experience Platform
description: Découvrez comment fusionner les données d’événement du SDK Web d’Experience Platform
seo-description: Découvrez comment fusionner les données d’événement du SDK Web d’Experience Platform
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 42%

---


# Fusion de données d’événement

>[!IMPORTANT]
>
>Cette fonctionnalité est encore en cours de développement. Toutes les solutions ne pourront pas fusionner les données de événement comme décrit sur cette page.

Parfois, toutes les données ne sont pas disponibles lorsqu’un événement se produit. Vous souhaiterez peut-être capturer les données que vous _possédez_ afin qu’elles ne soient pas perdues si, par exemple, l’utilisateur ferme le navigateur. D’un autre côté, vous pouvez également inclure toutes les données qui seront disponibles ultérieurement.

Dans ce cas, vous pouvez fusionner les données avec des événements précédents en transmettant `eventMergeId` comme option aux commandes `event` de la manière suivante :

```javascript
alloy("sendEvent", {
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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  }
  "eventMergeId": "ABC123"
});
```

By passing the same `eventMergeID` value to both event commands in this example, the data in the second event command is augmented to data previously sent on the first event command. A record for each event command is created in the [!DNL Experience Data Platform], but during reporting the records are joined together using the `eventMergeID` and appear as a single event.

If you are sending data about a particular event to third-party providers, you can include the same `eventMergeID` with that data as well. Later, if you choose to import the third-party data into the Adobe Experience Platform, `eventMergeID` will be used to merge together all data that was collected as a result of the discrete event that occurred on your webpage.

## Génération d’une `eventMergeID`

The `eventMergeID` value can be any string you choose, but remember that all events sent using the same ID are reported as a single event, so be careful to enforce uniqueness when events should not be merged. If you would like the SDK to generate a unique `eventMergeID` on your behalf (following the widely-adopted [UUID v4 specification](https://www.ietf.org/rfc/rfc4122.txt)), you can use the `createEventMergeId` command to do so.

Comme pour toutes les commandes, une promesse est renvoyée, car vous pouvez exécuter la commande avant que le SDK ne soit chargé. The promise will be resolved with a unique `eventMergeID` as soon as possible. Vous pouvez attendre que la promesse soit résolue avant d’envoyer les données au serveur de la manière suivante :

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
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
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    }
    "mergeId": results.eventMergeId
  });
});
```

Follow this same pattern if you would like access to the `eventMergeID` for other reasons (for example, to send it to a third-party provider):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Remarque sur le format XDM

Dans la commande d’événement, `mergeId` est ajouté à la charge utile `xdm`.  Si vous le souhaitez, `mergeId` peut être envoyé comme faisant partie de l’option xdm, de la manière suivante :

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    },
    "eventMergeId": "ABC123"
  }
});
```

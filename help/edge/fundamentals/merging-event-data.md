---
title: Fusion de données d’événement
seo-title: Fusion des données d’événement du SDK Web d’Adobe Experience Platform
description: Découvrez comment fusionner les données d’événement du SDK Web d’Experience Platform
seo-description: Découvrez comment fusionner les données d’événement du SDK Web d’Experience Platform
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 95%

---


# Fusion de données d’événement

>[!IMPORTANT]
>
>Cette fonctionnalité est encore en cours de développement et toutes les solutions ne pourront donc pas fusionner ces données.

Parfois, toutes les données ne sont pas disponibles lorsqu’un événement se produit. Vous souhaiterez peut-être capturer les données que vous _possédez_ afin qu’elles ne soient pas perdues si, par exemple, l’utilisateur ferme le navigateur. D’un autre côté, vous pouvez également inclure toutes les données qui seront disponibles ultérieurement.

Dans ce cas, vous pouvez fusionner les données avec des événements précédents en transmettant `eventMergeId` comme option aux commandes `event` de la manière suivante :

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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("event", {
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

En transmettant la même valeur d’ID de fusion d’événements aux deux commandes d’événement dans cet exemple, les données de la deuxième commande d’événement sont ajoutées aux données précédemment envoyées dans la première commande d’événement. Un enregistrement pour chaque commande d’événement est créé dans Experience Data Platform, mais pendant la création des rapports, les enregistrements sont joints ensemble à l’aide de l’ID de fusion d’événements et s’affichent comme un événement unique.

Si vous envoyez des données sur un événement particulier à des fournisseurs tiers, vous pouvez inclure le même ID de fusion d’événements avec ces données. Par la suite, si vous décidez d’importer les données tierces dans Adobe Experience Platform, l’ID de fusion d’événements sera utilisé pour fusionner toutes les données collectées à la suite de l’événement discret qui s’est produit sur votre page web.

## Génération d’un ID de fusion d’événements

La valeur de l’ID de fusion d’événements peut être n’importe quelle chaîne de votre choix, mais souvenez-vous que tous les événements envoyés à l’aide du même ID sont signalés comme un seul et même événement. Veillez donc à appliquer l’unicité lorsque les événements ne doivent pas être fusionnés. Si vous souhaitez que le SDK génère un ID de fusion d’événements unique (suivant la [spécification UUID v4](https://www.ietf.org/rfc/rfc4122.txt) largement adoptée), vous pouvez utiliser la commande `createEventMergeId`.

Comme pour toutes les commandes, une promesse est renvoyée, car vous pouvez exécuter la commande avant que le SDK ne soit chargé. La promesse sera résolue avec un ID de fusion d’événements unique dès que possible. Vous pouvez attendre que la promesse soit résolue avant d’envoyer les données au serveur de la manière suivante :

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("event", {
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

Suivez ce même modèle si vous souhaitez accéder à l’ID de fusion d’événements pour d’autres raisons (par exemple, pour l’envoyer à un fournisseur tiers) :

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
alloy("event", {
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

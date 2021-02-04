---
title: Fusion de données d’événement
seo-title: Fusion des données d’événement du SDK Web d’Adobe Experience Platform
description: Découvrez comment fusionner les données d’événement du SDK Web d’Experience Platform
seo-description: Découvrez comment fusionner les données d’événement du SDK Web d’Experience Platform
keywords: merge;données de événement;eventMergeId;createEventMergeId;sendEvent;mergeId;mergeId;eventMergeIdPromise; Promesse d'ID de fusion ;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 52%

---


# Fusion de données d’événement

>[!IMPORTANT]
>
>Cette fonctionnalité est encore en cours de développement. Toutes les solutions ne pourront pas fusionner les données de événement comme décrit sur cette page.

Parfois, toutes les données ne sont pas disponibles lorsqu’un événement se produit. Vous souhaiterez peut-être capturer les données que vous possédez afin qu’elles ne soient pas perdues si, par exemple, l’utilisateur ferme le navigateur. D’un autre côté, vous pouvez également inclure toutes les données qui seront disponibles ultérieurement.

Dans ce cas, vous pouvez fusionner les données avec des événements précédents en transmettant `mergeId` comme option aux commandes `event` de la manière suivante :

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
  },
  "mergeId": "ABC123"
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
  },
  "mergeId": "ABC123"
});
```

En transmettant la même valeur pour l&#39;option `mergeId` aux deux commandes de événement dans cet exemple, les données de la deuxième commande de événement sont augmentées aux données précédemment envoyées sur la première commande de événement. Un enregistrement pour chaque commande de événement est créé dans [!DNL Experience Data Platform], mais pendant le rapports, les enregistrements sont regroupés à l&#39;aide de l&#39;ID de fusion de événement et apparaissent comme un événement unique.

Si vous envoyez des données sur un événement particulier à des fournisseurs tiers, vous pouvez inclure le même ID de fusion d’événements avec ces données. Par la suite, si vous choisissez d’importer les données tierces dans Adobe Experience Platform, l’ID de fusion de événement sera utilisé pour fusionner toutes les données collectées à la suite du événement discret qui s’est produit sur votre page Web.

## Génération d’un ID de fusion d’événements

L’ID de fusion de événement peut être n’importe quelle chaîne de votre choix, mais n’oubliez pas que tous les événements envoyés à l’aide du même ID sont signalés comme un seul événement. Veillez donc à appliquer l’unicité lorsque les événements ne doivent pas être fusionnés. Si vous souhaitez que le SDK génère un ID de fusion d’événements unique (suivant la [spécification UUID v4](https://www.ietf.org/rfc/rfc4122.txt) largement adoptée), vous pouvez utiliser la commande `createEventMergeId`.

Comme pour toutes les commandes, une promesse est renvoyée, car vous pouvez exécuter la commande avant que le SDK ne soit chargé. La promesse sera résolue avec un ID de fusion d’événements unique dès que possible. Vous pouvez attendre que la promesse soit résolue avant d’envoyer les données au serveur de la manière suivante :

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
    },
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
    },
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

Dans la commande événement, l’ID de fusion de événement est ajouté à la charge utile `xdm` à l’emplacement correct en votre nom.  Si vous le souhaitez, l&#39;ID de fusion de événement peut être envoyé dans le cadre de l&#39;option `xdm` à la place, comme suit :

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

Lors de l&#39;ajout direct de l&#39;ID de fusion du événement à l&#39;objet `xdm`, notez que le nom `eventMergeID` est utilisé à la place de `mergeId`.

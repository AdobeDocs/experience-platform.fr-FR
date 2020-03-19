---
title: 'Fusion de données '
seo-title: Fusion des données  du SDK Web d’Adobe Experience Platform
description: 'Découvrez comment fusionner les données du SDK Web Experience Platform '
seo-description: 'Découvrez comment fusionner les données du SDK Web Experience Platform '
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Bêta) Fusionner des données 

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Parfois, toutes les données ne sont pas disponibles lorsqu’un se produit. Vous souhaiterez peut-être capturer les données que vous _possédez_ afin qu’elles ne soient pas perdues si, par exemple, l’utilisateur ferme le navigateur. D’un autre côté, vous pouvez également inclure toutes les données qui seront disponibles ultérieurement.

Dans ce cas, vous pouvez fusionner des données avec des  précédentes en transmettant `eventMergeId` comme option aux `event` commandes comme suit :

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

En transmettant la même valeur d’ID de fusion  aux deux commandes de  dans cet exemple, les données de la deuxième commande de  sont augmentées aux données précédemment envoyées dans la première commande de l’. Un enregistrement pour chaque commande de  d’est créé dans la plateforme de données d’expérience, mais pendant l’ les enregistrements sont regroupés à l’aide de l’ID de fusion de l’ et apparaissent sous la forme d’un seul de données d’expérience.

Si vous envoyez des données sur un particulier à des fournisseurs tiers, vous pouvez inclure le même ID de fusion de  avec ces données. Par la suite, si vous décidez d’importer les données tierces dans Adobe Experience Platform, l’ID de fusion du sera utilisé pour fusionner toutes les données collectées à la suite du discret  qui s’est produit sur votre page Web.

## Génération d’un ID de fusion 

La valeur de l’ID de fusion  peut être n’importe quelle chaîne de votre choix, mais n’oubliez pas que tous les envoyés à l’aide du même ID sont signalés comme un seul et même. Veillez donc à appliquer l’unicité lorsque le ne doit pas être fusionné. Si vous souhaitez que le SDK génère en votre nom un identifiant de fusion de unique (suivant la spécification [UUID v4](https://www.ietf.org/rfc/rfc4122.txt)largement adoptée `createEventMergeId` ), vous pouvez utiliser lacommande pour ce faire.

Comme pour toutes les commandes, une promesse est renvoyée, car vous pouvez exécuter la commande avant que le SDK ne soit chargé. La promesse sera résolue avec un ID de fusion de unique dès que possible. Vous pouvez attendre que la promesse soit résolue avant d’envoyer les données au serveur comme suit :

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
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
    "mergeId": eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(eventMergeId) {
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
    "mergeId": eventMergeId
  });
});
```

Suivez ce même modèle si vous souhaitez accéder à l’ID de fusion  pour d’autres raisons (par exemple, pour l’envoyer à un fournisseur tiers) :

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
  // send event merge ID to a third-party provider
  console.log(eventMergeId);
});
```

## Remarque concernant le format XDM

Dans la commande  du, le `mergeId` code est en fait ajouté à la `xdm` charge utile.  Si vous le souhaitez, vous `mergeId` pouvez plutôt envoyer le fichier dans le cadre de l’option xdm, comme suit :

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

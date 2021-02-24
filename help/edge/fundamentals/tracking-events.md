---
title: Suivi des Événements à l’aide du SDK Web Adobe Experience Platform
seo-description: Découvrez comment effectuer le suivi des événements du SDK Web Adobe Experience Platform.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 56%

---


# Suivi des événements

Pour envoyer des données de événement à Adobe Experience Cloud, utilisez la commande `sendEvent`. La commande `sendEvent` constitue le principal moyen pour envoyer des données à et pour récupérer du contenu personnalisé, des identités et des destinations d’audience.[!DNL Experience Cloud]

Les données envoyées à Adobe Experience Cloud entrent dans deux catégories :

* Données XDM
* Données autres que XDM (actuellement non prises en charge)

## Envoi de données XDM

Les données XDM sont un objet dont le contenu et la structure correspondent à un schéma que vous avez créé dans Adobe Experience Platform. [En savoir plus sur la création d’un schéma.](../../xdm/tutorials/create-schema-ui.md)

Toutes les données XDM que vous souhaitez intégrer à vos analyses, personnalisation, audiences ou destinations doivent être envoyées à l’aide de l’option `xdm`.


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
});
```

Un certain temps peut s&#39;écouler entre l&#39;exécution de la commande `sendEvent` et l&#39;envoi des données au serveur (par exemple, si la bibliothèque du SDK Web n&#39;a pas été entièrement chargée ou si le consentement n&#39;a pas encore été reçu). Si vous souhaitez modifier une partie de l&#39;objet `xdm` après avoir exécuté la commande `sendEvent`, il est vivement recommandé de cloner l&#39;objet `xdm` _avant d&#39;exécuter la commande_. `sendEvent` Par exemple :

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

Dans cet exemple, la couche de données est clonée en la sérialisant sur JSON, puis en la désérialisant. Ensuite, le résultat cloné est transmis dans la commande `sendEvent`. Cela permet de s&#39;assurer que la commande `sendEvent` contient un instantané de la couche de données telle qu&#39;elle existait lors de l&#39;exécution de la commande `sendEvent`, de sorte que les modifications ultérieures apportées à l&#39;objet de couche de données d&#39;origine ne soient pas répercutées dans les données envoyées au serveur. Si vous utilisez une couche de données pilotée par un événement, le clonage de vos données est probablement déjà géré automatiquement. Par exemple, si vous utilisez la couche de données client [Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), la méthode `getState()` fournit un instantané calculé et cloné de toutes les modifications antérieures. Cela est également géré automatiquement si vous utilisez l’extension Adobe Experience Platform Web SDK dans Adobe Experience Platform Launch.

>[!NOTE]
>
>Les données pouvant être envoyées dans chaque événement du champ XDM sont limitées à 32 Ko.

### Envoi de données autres que XDM

Actuellement, l’envoi de données qui ne correspondent pas à un schéma XDM n’est pas pris en charge. La prise en charge est prévue pour une date ultérieure.

### Définition de `eventType`

Dans un événement d’expérience XDM, il existe un champ `eventType` facultatif. Il contient le type d’événement principal pour l’enregistrement. Définir un type d&#39;événement peut vous aider à différencier les différents événements que vous allez envoyer. XDM fournit plusieurs types d&#39;événement prédéfinis que vous pouvez utiliser ou vous créez toujours vos propres types d&#39;événement personnalisés pour vos cas d&#39;utilisation. Vous trouverez ci-dessous une liste de tous les types d&#39;événement prédéfinis fournis par XDM. [Pour en savoir plus, consultez le rapport](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values) public XDM.


| **Type d’événement:** | **Définition:** |
| ---------------------------------- | ------------ |
| advertising.completes | Indique si un fichier multimédia minuté a été visionné jusqu’à la fin ; cela ne signifie pas nécessairement que l’utilisateur a visionné l’ensemble de la vidéo, elle aurait pu faire une avance rapide |
| advertising.timePlayed | Décrit le temps passé par un utilisateur sur une ressource multimédia minutée spécifique. |
| advertising.federated | Indique si un événement d’expérience a été créé par le biais d’une fédération de données (partage de données entre clients). |
| advertising.clicks | Actions de clic sur une publicité |
| advertising.conversions | Actions prédéfinies par le client qui déclenchent un événement pour l’évaluation des performances |
| advertising.firstQuartiles | Une publicité vidéo numérique a été lue pendant 25 % de sa durée à une vitesse normale |
| advertising.impressions | Impression d’une publicité destinée à un utilisateur final susceptible d’être visualisé |
| advertising.midpoints | Une publicité vidéo numérique a été lue pendant 50% de sa durée à une vitesse normale |
| advertising.starts | La lecture d’une publicité vidéo numérique a commencé |
| advertising.thirdQuartiles | Une publicité vidéo numérique a été lue pendant 75 % de sa durée à une vitesse normale |
| web.webpagedetails.pageViews | Vues qu’une page web a produites |
| web.webinteraction.linkClicks | Un clic sur un lien web s’est produit |
| commerce.checkouts | Action durant un processus de passage en caisse d’une des listes de produits. Il peut y avoir plusieurs événements de passage en caisse s’il existe plusieurs étapes dans un processus de passage en caisse. S’il existe plusieurs étapes, les informations sur l’heure de l’événement et la page ou l’expérience référencée sont utilisées pour identifier l’étape que chaque événement représente dans l’ordre |
| commerce.productListAdds | Ajout d’un produit à la liste de produits. Exemple : ajout d’un produit dans le panier |
| commerce.productListOpens | Initialisation d’une nouvelle liste de produits. Exemple : création d’un panier |
| commerce.productListRemovals | Suppression d’une ou de plusieurs entrées sur une liste de produits. Exemple : suppression d’un produit dans un panier |
| commerce.productListReopens | Une liste de produits qui n’était plus accessible (abandonnée) a été réactivée par l’utilisateur. Exemple avec une activité de remarketing |
| commerce.productListViews | Vues qu’une liste de produits a générées |
| commerce.productViews | Vues qu’un produit a générées |
| commerce.purchases | Une commande a été acceptée. L’achat est la seule action requise dans une conversion commerciale. Une liste de produits doit être référencée pour l’achat |
| commerce.saveForLaters | La liste de produits est enregistrée pour une utilisation ultérieure. Exemple d’une liste de souhaits de produits |
| delivery.feedback | Événements de commentaires pour une diffusion. Exemples de événements de commentaire pour une diffusion de courriel |


Ces types d&#39;événement s&#39;afficheront dans une liste déroulante si vous utilisez l&#39;extension Adobe Experience Platform Launch ou si vous pouvez toujours les transmettre sans Experience Platform Launch. Ils peuvent être transmis dans le cadre de l&#39;option `xdm`.


```javascript
alloy("sendEvent", {
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

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Remplacement de l’ID de jeu de données

Dans certains cas, vous pouvez envoyer un événement à un jeu de données autre que celui configuré dans l’interface utilisateur de configuration. Pour cela, vous devez définir l&#39;option `datasetId` sur la commande `sendEvent` :


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Ajouter des informations d&#39;identité

Des informations d&#39;identité personnalisées peuvent également être ajoutées au événement. Voir [Récupération de l’ID d’Experience Cloud](../identity/overview.md).

## Utilisation de l’API sendBeacon

Il peut s’avérer difficile d’envoyer des données d’événement juste avant que l’utilisateur ne quitte une page web. Si la requête prend trop de temps, le navigateur peut l’annuler. Certains navigateurs ont implémenté une API web appelée `sendBeacon` pour faciliter la collecte des données pendant cette période. Lors de l’utilisation de `sendBeacon`, le navigateur effectue la demande web dans le contexte de navigation globale. Cela signifie que le navigateur effectue la demande de balise en arrière-plan et n’interrompt pas la navigation dans la page. Pour indiquer à Adobe Experience Platform [!DNL Web SDK] d&#39;utiliser `sendBeacon`, ajoutez l&#39;option `"documentUnloading": true` à la commande événement.  Voici un exemple :


```javascript
alloy("sendEvent", {
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

Les navigateurs ont imposé des limites à la quantité de données pouvant être simultanément envoyées avec `sendBeacon`. Dans de nombreux navigateurs, la limite est de 64 Ko. Si le navigateur rejette le événement car la charge utile est trop importante, Adobe Experience Platform [!DNL Web SDK] revient à utiliser sa méthode de transport normale (par exemple, récupérer).

## Gestion des réponses d’événements

Si vous souhaitez gérer une réponse d’un événement, vous pouvez être averti d’un succès ou d’un échec de la manière suivante :


```javascript
alloy("sendEvent", {
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
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

1. Valeurs transmises sous forme d’options à la commande d’événement `alloy("sendEvent", { xdm: ... });`
2. Valeurs collectées automatiquement  (voir [Informations automatiques](../data-collection/automatic-information.md))
3. Modifications apportées dans le rappel `onBeforeEventSend`

Si le rappel `onBeforeEventSend` renvoie une exception, l’événement est toujours envoyé ; toutefois, aucune des modifications apportées dans le rappel n’est appliquée à l’événement final.

## Erreurs potentielles

Lors de l’envoi d’un événement, une erreur peut être générée si les données envoyées sont trop volumineuses (plus de 32 Ko pour la requête complète). Dans ce cas, vous devez réduire la quantité de données envoyées.

Lorsque le débogage est activé, le serveur valide de manière synchrone les données d’événement envoyées par rapport au schéma XDM configuré. Si les données ne correspondent pas au schéma, les détails sur la discordance sont renvoyés par le serveur et une erreur est générée. Dans ce cas, modifiez les données pour qu’elles correspondent au schéma. Lorsque le débogage n’est pas activé, le serveur valide les données de manière asynchrone et, par conséquent, aucune erreur correspondante n’est générée.

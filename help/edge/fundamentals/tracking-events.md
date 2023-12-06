---
title: Suivi des événements à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment effectuer le suivi des événements du SDK Web Adobe Experience Platform.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 21%

---


# Suivi des événements

Pour envoyer des données d’événement à Adobe Experience Cloud, utilisez la variable `sendEvent` . La variable `sendEvent` est le moyen principal d’envoyer des données à la variable [!DNL Experience Cloud]et pour récupérer du contenu personnalisé, des identités et des destinations d’audience.

Les données envoyées à Adobe Experience Cloud entrent dans deux catégories :

* Données XDM
* Données autres que XDM

## Envoi de données XDM

Les données XDM sont un objet dont le contenu et la structure correspondent à un schéma que vous avez créé dans Adobe Experience Platform. [En savoir plus sur la création d’un schéma.](../../xdm/tutorials/create-schema-ui.md)

Toutes les données XDM que vous souhaitez intégrer à vos analyses, à votre personnalisation, à vos audiences ou à vos destinations doivent être envoyées à l’aide de la variable `xdm` .


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

Un certain temps peut s’écouler entre le moment où la variable `sendEvent` est exécutée et lorsque les données sont envoyées au serveur (par exemple, si la bibliothèque SDK Web n’a pas été entièrement chargée ou si le consentement n’a pas encore été reçu). Si vous avez l’intention de modifier une partie de la variable `xdm` après avoir exécuté l’objet `sendEvent` , il est vivement recommandé de cloner l’événement `xdm` objet _before_ en exécutant la fonction `sendEvent` . Par exemple :

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

Dans cet exemple, la couche de données est clonée en la sérialisant au format JSON, puis en la désérialisant. Ensuite, le résultat cloné est transmis dans la variable `sendEvent` . Cela permet de s’assurer que la variable `sendEvent` contient un instantané de la couche de données telle qu’elle existait lors de la `sendEvent` a été exécutée afin que les modifications ultérieures apportées à l’objet de couche de données d’origine ne soient pas répercutées dans les données envoyées au serveur. Si vous utilisez une couche de données pilotée par un événement, le clonage de vos données est probablement déjà géré automatiquement. Par exemple, si vous utilisez la variable [Adobe de la couche de données client](https://github.com/adobe/adobe-client-data-layer/wiki), la variable `getState()` fournit un instantané calculé et cloné de toutes les modifications antérieures. Cela est également géré automatiquement si vous utilisez l’extension de balise du SDK Web de Adobe Experience Platform.

>[!NOTE]
>
>Les données pouvant être envoyées dans chaque événement du champ XDM sont limitées à 32 Ko.


## Envoi de données autres que XDM

Les données qui ne correspondent pas à un schéma XDM doivent être envoyées à l’aide de la variable `data` de l’ `sendEvent` . Cette fonctionnalité est prise en charge dans les versions 2.5.0 et ultérieures du SDK Web.

Cela s’avère utile si vous devez mettre à jour un profil Adobe Target ou envoyer des attributs Recommendations Target. [En savoir plus sur ces fonctionnalités de Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

À l’avenir, vous pourrez envoyer la couche de données complète sous le `data` et l’associer au serveur XDM.

**Comment envoyer des attributs Profile et Recommendations à Adobe Target :**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### Définition de `eventType` {#event-types}

Dans les schémas XDM ExperienceEvent, il existe une `eventType` champ . Il contient le type d’événement principal pour l’enregistrement. La définition d’un type d’événement peut vous aider à différencier les différents événements que vous envoyez. XDM fournit plusieurs types d’événements prédéfinis que vous pouvez utiliser ou vous créez toujours vos propres types d’événements personnalisés pour vos cas d’utilisation. Pour obtenir un [liste de tous les types d’événements prédéfinis](../../xdm/classes/experienceevent.md#eventType).

Ces types d’événement sont affichés dans une liste déroulante si vous utilisez l’extension de balise ou si vous pouvez toujours les transmettre sans balise. Ils peuvent être transmis dans le cadre de la fonction `xdm` .


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

### Remplacement de l’identifiant du jeu de données

>[!IMPORTANT]
>
>La variable `datasetId` l’option prise en charge par `sendEvent` était obsolète. Pour remplacer un identifiant de jeu de données, utilisez [remplacements de configuration](../../datastreams/overrides.md) au lieu de .

Dans certains cas d’utilisation, vous pouvez envoyer un événement à un jeu de données autre que celui configuré dans l’interface utilisateur de configuration. Pour ce faire, vous devez définir la variable `datasetId` sur l’option `sendEvent` command :



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Ajout d’informations sur l’identité

Vous pouvez également ajouter des informations d’identité personnalisées à l’événement. Voir [Récupération de l’ID d’Experience Cloud](../identity/overview.md).

## Utilisation de l’API sendBeacon

Il peut s’avérer difficile d’envoyer des données d’événement juste avant que l’utilisateur ne quitte une page web. Si la requête prend trop de temps, le navigateur peut l’annuler. Certains navigateurs ont implémenté une API web appelée `sendBeacon` pour faciliter la collecte des données pendant cette période. Lors de l’utilisation de `sendBeacon`, le navigateur effectue la demande web dans le contexte de navigation globale. Cela signifie que le navigateur effectue la demande de balise en arrière-plan et ne retient pas la navigation dans la page. Pour indiquer à Adobe Experience Platform [!DNL Web SDK] pour utiliser `sendBeacon`, ajoutez l’option `"documentUnloading": true` à la commande d’événement.

**Exemple**

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

Les navigateurs ont imposé des limites à la quantité de données pouvant être simultanément envoyées avec `sendBeacon`. Dans de nombreux navigateurs, la limite est de 64 Ko. Si le navigateur rejette l’événement car la charge utile est trop importante, Adobe Experience Platform [!DNL Web SDK] revient à utiliser son mode de transport normal (par exemple, récupérer).

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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### La variable `result` objet

La variable `sendEvent` renvoie une promesse résolue avec une `result` . La variable `result` contient les propriétés suivantes :

| Propriété | Description |
|---------|----------|
| `propositions` | Les offres de personnalisation pour lesquelles le visiteur a rempli les critères. [En savoir plus sur les propositions.](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| `decisions` | Cette propriété est obsolète. Utilisez `propositions` à la place. |
| `destinations` | Audiences de Adobe Experience Platform qui peuvent être partagées avec des plateformes de personnalisation externes, des systèmes de gestion de contenu, des serveurs de publicités et d’autres applications exécutées sur des sites web clients. [En savoir plus sur les destinations.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html) |

>[!WARNING]
>
>La variable `destinations` est en version bêta. La documentation et les fonctionnalités peuvent changer.

## Modification globale des événements {#modifying-events-globally}

Si vous souhaitez ajouter, supprimer ou modifier des champs de l’événement globalement, vous pouvez configurer une `onBeforeEventSend` rappel. Ce rappel est appelé chaque fois qu’un événement est envoyé. Ce rappel est transmis dans un objet d’événement avec une `xdm` champ . Pour modifier les données envoyées avec l’événement, modifiez `content.xdm`.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

Les champs `xdm` sont définis dans l’ordre suivant :

1. Valeurs transmises sous forme d’options à la commande d’événement `alloy("sendEvent", { xdm: ... });`.
2. Valeurs collectées automatiquement. Voir [Informations automatiques](../data-collection/automatic-information.md).
3. Modifications apportées dans le rappel `onBeforeEventSend`

Quelques notes sur le `onBeforeEventSend` callback :

* L’événement XDM peut être modifié pendant le rappel. Une fois le rappel renvoyé, tous les champs et valeurs modifiés des objets content.xdm et content.data sont envoyés avec l’événement .

  ```javascript
  onBeforeEventSend: function(content){
    //sets a query parameter in XDM
    const queryString = window.location.search;
    const urlParams = new URLSearchParams(queryString);
    content.xdm.marketing.trackingCode = urlParams.get('cid')
  }
  ```

* Si le rappel renvoie une exception, le traitement de l’événement est interrompu et l’événement n’est pas envoyé.
* Si le rappel renvoie la valeur booléenne de `false`, le traitement des événements s’interrompt sans erreur et l’événement n’est pas envoyé. Ce mécanisme permet d’ignorer facilement certains événements en examinant les données d’événement et en renvoyant `false` si l’événement ne doit pas être envoyé.

  >[!NOTE]
  >Veillez à ne pas renvoyer la valeur false lors du premier événement d’une page. Le renvoi de la valeur false sur le premier événement peut avoir une incidence négative sur la personnalisation.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Toute valeur renvoyée autre que la valeur booléenne `false` permettra à l’événement de traiter et d’envoyer après le rappel.

* Les événements peuvent être filtrés en examinant le type d’événement (voir [Types d’événement](#event-types).):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## Erreurs potentielles

Lors de l’envoi d’un événement, une erreur peut être générée si les données envoyées sont trop volumineuses (plus de 32 Ko pour la requête complète). Dans ce cas, vous devez réduire la quantité de données envoyées.

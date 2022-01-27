---
keywords: personnalisation personnalisée ; destination; destination personnalisée de la plateforme d’expérience ;
title: Connexion à la personnalisation personnalisée
description: Cette destination fournit une personnalisation externe, des systèmes de gestion de contenu, des serveurs de publicités et d’autres applications qui s’exécutent sur votre site pour récupérer des informations de segment à partir de Adobe Experience Platform. Cette destination fournit une personnalisation en temps réel basée sur l’appartenance au segment du profil utilisateur.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: dd9493077706b102467493e90b363ac202550eee
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 7%

---

# Connexion à la personnalisation personnalisée {#custom-personalization-connection}

## Présentation {#overview}

Cette destination permet de récupérer les informations de segment de Adobe Experience Platform vers des plateformes de personnalisation externes, des systèmes de gestion de contenu, des serveurs de publicités et d’autres applications qui s’exécutent sur les sites web des clients.

## Conditions préalables {#prerequisites}

Cette intégration est optimisée par la fonction [SDK Web Adobe Experience Platform](../../../edge/home.md) ou le [SDK Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/). Vous devez utiliser l’un de ces SDK pour utiliser cette destination.

## Type d&#39;export {#export-type}

**Requête de profil** - vous demandez tous les segments mappés dans la destination de personnalisation personnalisée pour un profil unique. Différentes destinations de personnalisation personnalisées peuvent être configurées pour différentes [Adobe des flux de données de collecte de données](../../../edge/fundamentals/datastreams.md).

## Cas dʼutilisation {#use-cases}

Cette destination partage les audiences avec les serveurs d’annonces et les applications de personnalisation autres que les Adobes, qui doivent être utilisées en temps réel, afin de décider quelle publicité les utilisateurs doivent voir sur un site web.

### Cas d’utilisation #1

**Personnaliser une page d&#39;accueil**

Un site web de location et de vente d’habitations souhaite personnaliser sa page d’accueil en fonction des qualifications de segments dans Adobe Experience Platform. L’entreprise peut sélectionner les audiences qui doivent bénéficier d’une expérience personnalisée et les mapper à la destination de personnalisation personnalisée configurée pour leur application de personnalisation autre qu’un Adobe en tant que critères de ciblage.

**Publicité sur site ciblée**

En utilisant une destination de personnalisation personnalisée distincte pour leur serveur d’annonces, le même site web peut cibler la publicité sur site à l’aide d’un ensemble différent de segments de Adobe Experience Platform en tant que critères de ciblage.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **[!UICONTROL Alias d’intégration]**: Cette valeur est envoyée au SDK Web Experience Platform sous la forme d’un nom d’objet JSON.
* **[!UICONTROL Identifiant du flux de données]**: Cela détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configuration d’un flux de données](../../../edge/fundamentals/datastreams.md) pour plus d’informations.

## Activation des segments vers cette destination {#activate}

Lecture [Activation des profils et des segments vers les destinations de requête de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Si vous utilisez [Adobe des balises](../../../tags/home.md) pour déployer le SDK Web Experience Platform, utilisez la méthode [envoi d’événement terminé](../../../edge/extension/event-types.md) et votre action de code personnalisé comporte une `event.destinations` que vous pouvez utiliser pour afficher les données exportées.

Voici un exemple de valeur pour la variable `event.destinations` variable :

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

Si vous n’utilisez pas [Adobe des balises](../../../tags/home.md) pour déployer le SDK Web Experience Platform, utilisez la méthode [gestion des réponses des événements](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) pour afficher les données exportées.

Vous pouvez analyser la réponse JSON de Adobe Experience Platform pour trouver l’alias d’intégration correspondant à l’application que vous intégrez à Adobe Experience Platform. Les identifiants de segment peuvent être transmis dans le code de l’application en tant que paramètres de ciblage. Vous trouverez ci-dessous un exemple de ce à quoi cela ressemblerait spécifique à la réponse de destination.

```
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
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## Utilisation et gouvernance des données {#data-usage-governance}

Tous [!DNL Adobe Experience Platform] Les destinations sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la section [Présentation de la gouvernance des données](../../../data-governance/home.md).

---
keywords: personnalisation personnalisée;destination;destination personnalisée Experience Platform;
title: Connexion de personnalisation personnalisée
description: Cette destination fournit une personnalisation externe, des systèmes de gestion de contenu, des serveurs de publicités et d’autres applications qui s’exécutent sur votre site pour récupérer des informations de segment à partir d’Adobe Experience Platform. Cette destination fournit une personnalisation en temps réel basée sur l’appartenance au segment du profil utilisateur.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 05217dead7e1365d6dcc0cc7ae4078628514d1d5
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 99%

---

# Connexion de personnalisation personnalisée {#custom-personalization-connection}

## Présentation {#overview}

Cette destination permet de récupérer des informations sur des segments depuis Adobe Experience Platform vers des plateformes de personnalisation externes, des systèmes de gestion de contenu, des serveurs publicitaires et d’autres applications exécutées sur les sites web des clients.

## Conditions préalables {#prerequisites}

Cette intégration est optimisée par le [SDK web Adobe Experience Platform](../../../edge/home.md) ou le [SDK mobile Adobe Experience Platform](https://aep-sdks.gitbook.io/docs/). Pour utiliser cette destination, vous devez utiliser l’un de ces SDK.

>[!IMPORTANT]
>
>Avant de créer une connexion de personnalisation personnalisée, lisez le guide expliquant comment [configurer des destinations de personnalisation pour la personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md). Ce guide vous fait parcourir toutes les étapes de configuration requises pour les cas d’utilisation de la personnalisation de la même page et de la page suivante, sur plusieurs composants Experience Platform.

## Type d’exportation et fréquence {#export-type-frequency}

**Requête de profil** : vous demandez tous les segments mappés dans la destination de personnalisation personnalisée pour un profil unique. Différentes destinations de personnalisation personnalisées peuvent être configurées pour différents [flux de données de collecte de données Adobe](../../../edge/fundamentals/datastreams.md).

## Cas dʼutilisation {#use-cases}

Cette destination partage les audiences avec les serveurs de publicités et les applications de personnalisation autres qu’Adobe, pour une utilisation en temps réel, afin de décider quelle publicité les utilisateurs doivent voir sur un site web.

### Cas d’utilisation 1

**Personnaliser une page d’accueil**

Un site web de location et de vente d’habitations souhaite personnaliser sa page d’accueil en fonction des qualifications de segments dans Adobe Experience Platform. L’entreprise peut sélectionner les audiences qui doivent bénéficier d’une expérience personnalisée et les mapper à la destination de personnalisation personnalisée configurée pour son application de personnalisation autre qu’Adobe en tant que critères de ciblage.

**Publicité sur site ciblée**

En utilisant une destination de personnalisation personnalisée distincte pour son serveur de publicités, le même site web peut cibler la publicité sur site à l’aide d’un ensemble différent de segments d’Adobe Experience Platform en tant que critères de ciblage.

## Se connecter à la destination {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="À propos des identifiants de flux de données"
>abstract="Cette option détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Vous devez configurer un flux de données avant de pouvoir configurer votre destination."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr" text="Découvrez comment configurer un flux de données"

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **[!UICONTROL Alias d’intégration]** : cette valeur est envoyée au SDK web Experience Platform sous forme de nom d’objet JSON.
* **[!UICONTROL Identifiant du flux de données]** : détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configurer un flux de données](../../../edge/fundamentals/datastreams.md) pour plus d’informations.

## Activer des segments vers cette destination {#activate}

Consultez la section [Activer des profils et des segments vers les destinations de requête de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Si vous utilisez des [balises dans Adobe Experience Platform](../../../tags/home.md) pour déployer le SDK web Experience Platform, utilisez la fonctionnalité [Envoi de l’événement terminé](../../../edge/extension/event-types.md) et votre action de code personnalisé contiendra une variable `event.destinations` que vous pourrez utiliser pour afficher les données exportées.

Voici un exemple de valeur pour la variable `event.destinations` :

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

Si vous n’utilisez pas de [balises](../../../tags/home.md) pour déployer le SDK web Experience Platform, utilisez la fonctionnalité [Gestion des réponses d’événements](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) pour afficher les données exportées.

Vous pouvez analyser la réponse JSON d’Adobe Experience Platform pour trouver l’alias d’intégration correspondant à l’application que vous intégrez dans Adobe Experience Platform. Les identifiants de segment peuvent être transmis dans le code de l’application en tant que paramètres de ciblage. Vous trouverez ci-dessous un exemple de ce à quoi cela ressemblerait dans le cas spécifique de la réponse de destination.

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

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](../../../data-governance/home.md).

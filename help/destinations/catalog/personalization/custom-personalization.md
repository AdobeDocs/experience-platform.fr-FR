---
keywords: personnalisation personnalisée;destination;destination personnalisée Experience Platform;
title: Connexion de personnalisation personnalisée
description: Cette destination fournit une personnalisation externe, des systèmes de gestion de contenu, des serveurs de publicités et d’autres applications qui s’exécutent sur votre site pour récupérer les informations d’audience à partir de Adobe Experience Platform. Cette destination fournit une personnalisation en temps réel basée sur l’appartenance à l’audience du profil utilisateur.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 40%

---


# Connexion de personnalisation personnalisée {#custom-personalization-connection}

## Journal des modifications de destination {#changelog}

| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Mai 2023 | Nouvelles fonctionnalités et mise à jour de la documentation | Depuis mai 2023, la connexion **[!UICONTROL Custom personalization]** prend en charge la [personnalisation basée sur les attributs](../../ui/activate-edge-personalization-destinations.md#map-attributes) et est généralement disponible pour tous les clients. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Les attributs de profil peuvent contenir des données sensibles. Pour protéger ces données, vous devez utiliser l’API [Edge Network](https://developer.adobe.com/data-collection-apis/docs/) lors de la configuration de la destination **[!UICONTROL Custom Personalization]** pour la personnalisation basée sur les attributs. Tous les appels API d’Edge Network doivent être effectués dans un [contexte authentifié](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication).
>
><br>Vous pouvez récupérer les attributs de profil via l’[API Edge Network](https://developer.adobe.com/data-collection-apis/docs/) en ajoutant une intégration côté serveur qui utilise le même flux de données que celui que vous utilisez déjà pour votre implémentation de Web ou Mobile SDK.
>
><br>Si vous ne suivez pas les exigences ci-dessus, la personnalisation sera basée sur l’appartenance à l’audience uniquement.

## Vue d’ensemble {#overview}

Configurez cette destination pour permettre aux plateformes de personnalisation externes, aux systèmes de gestion de contenu, aux serveurs de publicités et aux autres applications s’exécutant sur les sites web des clients de récupérer les informations d’audience à partir de Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Cette destination nécessite l’utilisation de l’une des méthodes de collecte de données suivantes, selon votre implémentation :

* Utilisez [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) si vous souhaitez collecter des données sur votre site Web.
* Utilisez [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) si vous souhaitez collecter des données à partir de votre application mobile.
* Utilisez l’API [Edge Network](https://developer.adobe.com/data-collection-apis/docs/) si vous n’utilisez pas Web SDK ou Mobile SDK, ou si vous souhaitez personnaliser l’expérience utilisateur en fonction des attributs de profil.

>[!IMPORTANT]
>
>**Exigences de personnalisation basées sur les attributs :** si vous souhaitez effectuer une personnalisation en fonction des attributs de profil (et pas seulement de l’appartenance à l’audience), vous **devez** utiliser l’[API Edge Network](https://developer.adobe.com/data-collection-apis/docs/) avec une intégration côté serveur authentifiée, que vous utilisiez également Web SDK ou Mobile SDK pour la collecte de données.
>
>Web SDK et Mobile SDK prennent en charge la personnalisation uniquement en fonction de l’appartenance à l’audience. L’API Edge Network est **obligatoire** pour récupérer en toute sécurité les attributs de profil pour la personnalisation.

>[!IMPORTANT]
>
>Avant de créer une connexion de personnalisation personnalisée, lisez le guide expliquant comment [activer les données d’audience vers des destinations de personnalisation Edge](../../ui/activate-edge-personalization-destinations.md). Ce guide vous fait parcourir toutes les étapes de configuration requises pour les cas d’utilisation de la personnalisation de la même page et de la page suivante, sur plusieurs composants Experience Platform.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!DNL Profile request]** | Vous demandez toutes les audiences mappées dans la destination de personnalisation personnalisée pour un profil unique. Différentes destinations de personnalisation personnalisées peuvent être configurées pour différents [flux de données de collecte de données Adobe](../../../datastreams/overview.md). |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

## Se connecter à la destination {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="À propos des trains de données"
>abstract="Cette option détermine dans quel train de données de collecte de données les audiences seront inclues dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Vous devez configurer un flux de données avant de pouvoir configurer votre destination."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=fr" text="Découvrez comment configurer un train de données"

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Name]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : saisissez une description de la destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **[!UICONTROL Integration alias]** : cette valeur est envoyée au SDK Web Experience Platform sous la forme d’un nom d’objet JSON.
* **[!UICONTROL Datastream]** : détermine dans quel flux de données de collecte de données les audiences seront incluses dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configurer un flux de données](../../../datastreams/overview.md) pour plus d’informations.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Lisez [Activer des destinations de personnalisation Edge de profils et d’audiences](../../ui/activate-edge-personalization-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Données exportées {#exported-data}

Si vous utilisez des [balises dans Adobe Experience Platform](/help/tags/home.md) pour déployer le SDK web Experience Platform, utilisez la fonctionnalité [Envoi de l’événement terminé](/help/tags/extensions/client/web-sdk/event-types.md) et votre action de code personnalisé contiendra une variable `event.destinations` que vous pourrez utiliser pour afficher les données exportées.

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

Si vous n’utilisez pas [Balises](/help/tags/home.md) pour déployer Experience Platform Web SDK, utilisez [réponses des commandes](/help/collection/js/commands/command-responses.md) pour afficher les données exportées.

Vous pouvez analyser la réponse JSON d’Adobe Experience Platform pour trouver l’alias d’intégration correspondant à l’application que vous intégrez dans Adobe Experience Platform. Les identifiants d’audience peuvent être transmis dans le code de l’application en tant que paramètres de ciblage. Vous trouverez ci-dessous un exemple de ce à quoi cela ressemblerait dans le cas spécifique de la réponse de destination.

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Exemple de réponse pour [!UICONTROL Custom Personalization With Attributes]

Lors de l’utilisation de **[!UICONTROL Custom Personalization With Attributes]**, la réponse de l’API ressemblera à l’exemple ci-dessous.

La différence entre **[!UICONTROL Custom Personalization With Attributes]** et **[!UICONTROL Custom Personalization]** est l’inclusion de la section `attributes` dans la réponse de l’API.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](../../../data-governance/home.md).

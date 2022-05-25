---
keywords: personnalisation personnalisée;destination;destination personnalisée Experience Platform;
title: Connexion de personnalisation personnalisée
description: Cette destination fournit une personnalisation externe, des systèmes de gestion de contenu, des serveurs de publicités et d’autres applications qui s’exécutent sur votre site pour récupérer des informations de segment à partir d’Adobe Experience Platform. Cette destination fournit une personnalisation en temps réel basée sur l’appartenance au segment du profil utilisateur.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 57%

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

**Requête de profil** : vous demandez tous les segments mappés dans la destination de personnalisation personnalisée pour un profil unique. Différentes destinations de personnalisation personnalisées peuvent être configurées pour différents [flux de données de collecte de données Adobe](../../../edge/datastreams/overview.md).

## Cas dʼutilisation {#use-cases}

Le [!DNL Custom personalization connection] vous permet d’utiliser vos propres plateformes de partenaire de personnalisation (par exemple, [!DNL Optimizely], [!DNL Pega]), tout en exploitant les fonctionnalités Experience Platform de collecte et de segmentation des données du réseau Edge, pour offrir une expérience de personnalisation plus approfondie aux clients.

Les cas d’utilisation décrits ci-dessous incluent à la fois la personnalisation du site et la publicité ciblée sur site.

Pour activer ces cas d’utilisation, les clients doivent disposer d’une méthode rapide et simplifiée pour récupérer les informations de segment de l’Experience Platform et envoyer ces informations à leurs systèmes désignés qu’ils ont configurés en tant que connexions de personnalisation personnalisées dans l’interface utilisateur de l’Experience Platform.

Il peut s’agir de plateformes de personnalisation externes, de systèmes de gestion de contenu, de serveurs de publicités et d’autres applications s’exécutant sur les propriétés web et mobiles des clients.

### Personnalisation de la même page {#same-page}

Un utilisateur visite une page de votre site web. Le client peut utiliser les informations actuelles sur la visite de la page (par exemple, l’URL de référence, la langue du navigateur, les informations sur les produits incorporés) pour sélectionner l’action/la décision suivante (par exemple, la personnalisation), à l’aide de la connexion de personnalisation personnalisée pour les plateformes non Adobes (par exemple, [!DNL Pega], [!DNL Optimizely], etc.).

### Personnalisation de la page suivante {#next-page}

Un utilisateur visite la page A de votre site web. En fonction de cette interaction, l’utilisateur a rempli les critères d’un ensemble de segments. L’utilisateur clique ensuite sur un lien qui le mène de la page A à la page B. Les segments pour lesquels l’utilisateur s’était qualifié lors de l’interaction précédente sur la page A, ainsi que les mises à jour de profil déterminées par la visite actuelle du site web, seront utilisés pour alimenter l’action/la décision suivante (par exemple, quelle bannière publicitaire afficher pour le visiteur, ou, dans le cas d’un test A/B, quelle version de la page afficher).

### Personnalisation de la prochaine session {#next-session}

Un utilisateur visite plusieurs pages de votre site web. En fonction de ces interactions, l’utilisateur a rempli les critères d’un ensemble de segments. L’utilisateur met ensuite fin à la session de navigation actuelle.

Le lendemain, l’utilisateur revient au même site web client. Les segments pour lesquels ils avaient été qualifiés lors de l’interaction précédente avec toutes les pages du site web visitées, ainsi que les mises à jour de profil déterminées par la visite du site web en cours, seront utilisés pour sélectionner l’action/la décision suivante (par exemple, la bannière publicitaire à afficher au visiteur ou, dans le cas d’un test A/B, la version de la page à afficher).

## Se connecter à la destination {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="À propos des identifiants de flux de données"
>abstract="Cette option détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Vous devez configurer un flux de données avant de pouvoir configurer votre destination."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr" text="Découvrez comment configurer un flux de données"

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **[!UICONTROL Alias d’intégration]** : cette valeur est envoyée au SDK web Experience Platform sous forme de nom d’objet JSON.
* **[!UICONTROL Identifiant du flux de données]** : détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configurer un flux de données](../../../edge/datastreams/overview.md) pour plus d’informations.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

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

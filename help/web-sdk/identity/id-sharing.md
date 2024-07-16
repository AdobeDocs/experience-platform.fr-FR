---
title: Partage d’identifiants entre appareils mobiles et domaines
description: Découvrez comment conserver les identifiants visiteur des propriétés mobiles aux propriétés web et entre les domaines
keywords: Identité;mobile;id;partage;domaine;interdomaines;sdk;plateforme;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 3%

---

# Partage d’identifiants entre appareils mobiles et domaines

## Vue d’ensemble

Le SDK Web de Adobe Experience Platform prend en charge les fonctionnalités de partage des identifiants visiteur qui permettent aux clients de fournir des expériences personnalisées plus précisément, entre les applications mobiles et le contenu web mobile, et entre les domaines.

## Cas d’utilisation {#use-cases}

### offrir une personnalisation cohérente entre les applications mobiles et les sites web mobiles ;

Une société de vêtements souhaite personnaliser l’expérience de ses clients en fonction de leurs intérêts et conserver la personnalisation exacte dans une application mobile qui charge également WebViews. En utilisant la fonction de partage d’ID entre appareils mobiles et Web, ils peuvent s’assurer que les offres les plus précises sont présentées aux clients, en utilisant le même identifiant visiteur dans l’application et le même contenu web mobile en transmettant le [!DNL ECID] à l’URL web mobile.

### Effectuer une personnalisation cohérente entre les domaines

Un détaillant disposant de plusieurs boutiques en ligne souhaite personnaliser l’expérience client sur l’ensemble de ses domaines, en fonction des intérêts des clients. À l’aide de la fonctionnalité de partage d’identifiants inter-domaines du SDK Web, le détaillant peut fournir des offres précises en fonction des intérêts des clients, sur tous leurs domaines.

### Amélioration de la création de rapports sur les activités des visiteurs

Un détaillant de technologie souhaite améliorer la création de rapports sur l’activité des visiteurs avec des informations sur le moment où ses visiteurs passent de l’application mobile à leur site web mobile ou à leurs autres domaines. Grâce à la fonctionnalité de partage d’identifiants inter-domaines du SDK Web, l’équipe marketing peut effectuer un suivi précis des visiteurs sur leurs propriétés web et générer des rapports d’activité.

## Conditions préalables {#prerequisites}

Pour utiliser le partage d&#39;identifiants entre appareils mobiles et sur plusieurs domaines, vous devez utiliser la version 2.11.0 ou ultérieure de [!DNL Web SDK].

Pour les implémentations mobiles Edge Network, cette fonctionnalité est prise en charge dans l’extension [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) commençant par la version 1.1.0 (iOS et Android).

Cette fonctionnalité est également compatible avec [!DNL VisitorAPI.js] version 1.7.0 ou ultérieure.

## Partage des identifiants de mobile à web {#mobile-to-web}

Utilisez l’API `getUrlVariables` de l’extension [ Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) pour récupérer les identifiants en tant que paramètres de requête et les joindre à votre URL lors de l’ouverture de [!DNL webViews].

Aucune configuration supplémentaire n’est requise pour que le SDK Web accepte les valeurs `ECID` dans la chaîne de requête.

Le paramètre de chaîne de requête comprend :

* `MCID` : ID Experience Cloud (`ECID`)
* `MCORGID` : Experience Cloud `orgID` qui doit correspondre au `orgID` configuré dans le [!DNL Web SDK].
* `TS` : paramètre d’horodatage ne pouvant pas dépasser cinq minutes.


Le partage d’ID entre appareils mobiles et web utilise le paramètre `adobe_mc` . Lorsque le paramètre `adobe_mc` est présent et valide, le `ECID` de la chaîne de requête est automatiquement ajouté à la carte d’identité dans la première requête envoyée à l’Edge Network. Toutes les interactions Edge Network suivantes utiliseront cet `ECID`.

Pour plus d’informations sur la manière de transmettre les identifiants visiteur d’une application mobile à un WebView, consultez la documentation sur la [gestion des WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Mise en oeuvre du partage d’identifiants entre domaines {#cross-domain-sharing}

Voir la commande [`appendIdentityToUrl`](../commands/appendidentitytourl.md) pour obtenir des instructions d’implémentation à l’aide de l’extension de balise du SDK Web et de la bibliothèque JavaScript du SDK Web.

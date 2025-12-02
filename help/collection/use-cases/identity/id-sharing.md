---
title: Partage d’identifiants entre appareils mobiles et domaines
description: Découvrez comment conserver les identifiants visiteur des appareils mobiles dans les propriétés web et entre les domaines
keywords: Identité;mobile;id;partage;domaine;inter-domaines;sdk;platform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 3%

---

# Partage d’identifiants entre appareils mobiles et domaines

## Vue d’ensemble

Adobe Experience Platform Web SDK prend en charge les fonctionnalités de partage des identifiants visiteur qui permettent aux clients de fournir des expériences personnalisées plus précisément, entre les applications mobiles et le contenu web mobile, et entre les domaines.

## Cas d’utilisation {#use-cases}

### Personnalisation cohérente entre les applications mobiles et les sites web mobiles

Une entreprise de vêtements souhaite personnaliser l’expérience de ses clients en fonction de leurs intérêts et conserver une personnalisation précise dans une application mobile qui charge également WebViews. En utilisant la fonctionnalité de partage d’identifiants mobile à web, ils peuvent s’assurer que les offres les plus précises sont présentées aux clients, en utilisant le même identifiant visiteur dans l’application et le contenu web mobile en transmettant le [!DNL ECID] à l’URL web mobile.

### Personnalisation cohérente sur plusieurs domaines

Un retailer avec plusieurs magasins en ligne souhaite personnaliser l’expérience de l’acheteur sur leurs domaines, en fonction des intérêts du client. Grâce à la fonctionnalité de partage d’identifiants entre domaines de Web SDK, retailer peut diffuser des offres précises en fonction des intérêts des clients, sur tous leurs domaines.

### Améliorer les rapports d’activité des visiteurs

Un retailer technologique souhaite améliorer les rapports d’activité des visiteurs en fournissant des informations sur le moment où leurs visiteurs passent de l’application mobile à leur site web mobile ou à leurs autres domaines. Grâce à la fonctionnalité de partage d’identifiants entre domaines de Web SDK, l’équipe marketing peut effectuer le suivi précis des visiteurs sur leurs propriétés web et générer des rapports d’activité.

## Conditions préalables {#prerequisites}

Pour utiliser le partage d’identifiants entre appareils mobiles et domaines, vous devez utiliser [!DNL Web SDK] version 2.11.0 ou ultérieure.

Pour les implémentations mobiles d’Edge Network, cette fonctionnalité est prise en charge dans l’extension [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) commençant par la version 1.1.0 (iOS et Android).

Cette fonctionnalité est également compatible avec [!DNL VisitorAPI.js] version 1.7.0 ou ultérieure.

## Partage d’identifiants entre appareils mobiles et sites web {#mobile-to-web}

Utilisez l’API `getUrlVariables` de l’extension [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) pour récupérer les identifiants en tant que paramètres de requête et les joindre à votre URL lors de l’ouverture de [!DNL webViews].

Aucune configuration supplémentaire n’est requise pour que le SDK Web accepte les valeurs `ECID` dans la chaîne de requête.

Le paramètre de chaîne de requête comprend :

* `MCID` : Experience Cloud ID (`ECID`)
* `MCORGID` : `orgID` Experience Cloud qui doit correspondre au `orgID` configuré dans le [!DNL Web SDK].
* `TS` : paramètre d’horodatage qui ne peut pas être antérieur à cinq minutes.


Le partage d’identifiants entre appareils mobiles et sites web utilise le paramètre `adobe_mc` . Lorsque le paramètre `adobe_mc` est présent et valide, le `ECID` de la chaîne de requête est automatiquement ajouté au mappage d’identité dans la première requête envoyée à Edge Network. Toutes les interactions Edge Network suivantes utiliseront ce `ECID`.

Pour plus d’informations sur la manière de transmettre des identifiants visiteur d’une application mobile à un WebView, consultez la documentation sur la [gestion des WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Implémenter le partage d’ID entre domaines {#cross-domain-sharing}

Consultez les liens ci-dessous, en fonction de la configuration de Web SDK :

* **Bibliothèque JavaScript** : commande [`appendIdentityToUrl`](../../js/commands/appendidentitytourl.md)
* **Extension de balise** : [redirection avec identité](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) action

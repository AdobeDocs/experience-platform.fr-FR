---
title: Présentation de l’installation de Web SDK
description: Découvrez comment installer Experience Platform Web SDK.
keywords: installation du sdk web;installer le sdk web;internet explorer;promesse;package npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Présentation de l’installation de Web SDK

Il existe trois manières prises en charge d’utiliser Adobe Experience Platform Web SDK :

1. **[Extension de balise Web SDK](/help/tags/extensions/client/web-sdk/overview.md)** : Adobe recommande d’utiliser cette méthode. Installez une balise de chargement sur votre site, puis utilisez l’interface utilisateur de la collecte de données de Adobe Experience Platform pour configurer votre implémentation.
1. **[Bibliothèque JavaScript Web SDK](library.md)** : référencez un fichier de bibliothèque hébergé sur un réseau CDN ou hébergez le fichier de bibliothèque à l’aide de votre propre infrastructure. Effectuez des appels à la bibliothèque dans le code de votre site.
1. **[NPM](npm.md)** : installez le SDK Web sur votre site à l’aide du gestionnaire de packages NPM.

## Conditions préalables

Avant d’utiliser ou d’installer le SDK Web, vous devez respecter les conditions suivantes :

* L’architecture dans Adobe Experience Platform doit d’abord être configurée. Ces paramètres comprennent tous les schémas, identités et flux de données nécessaires.
* Vous devez disposer des autorisations appropriées configurées pour accéder aux outils appropriés. Par exemple, si votre organisation décide d’utiliser l’extension de balise, vous devez disposer des autorisations appropriées pour accéder à l’interface utilisateur de la collecte de données. Pour plus d’informations, voir [Autorisations de collecte de données](../../permissions.md).
* Il est recommandé d’avoir un domaine propriétaire (CNAME). Si vous disposez déjà d’un CNAME pour Adobe Analytics, vous pouvez l’utiliser. Les tests en développement fonctionnent sans CNAME, mais Adobe recommande d’en avoir un avant la publication en production. Voir [Identifiants d’appareils propriétaires](../../use-cases/identity/first-party-device-ids.md) pour plus d’informations.

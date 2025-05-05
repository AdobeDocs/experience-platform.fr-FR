---
title: Présentation de l’installation du SDK Web
description: Découvrez comment installer le SDK Web Experience Platform.
keywords: installation du sdk web;installation du sdk web;internet explorer;promesse;package npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Présentation de l’installation du SDK Web

Il existe trois façons d’utiliser le SDK Web de Adobe Experience Platform prises en charge :

1. **[Extension de balise SDK Web](extension.md)** : Adobe recommande d’utiliser cette méthode. Installez un chargeur de balises sur votre site, puis utilisez l’interface utilisateur de collecte de données Adobe Experience Platform pour configurer votre mise en oeuvre.
1. **[Bibliothèque JavaScript du SDK Web](library.md)** : référencez un fichier de bibliothèque hébergé par le CDN ou hébergez le fichier à l’aide de votre propre infrastructure. Appelez la bibliothèque dans le code de votre site.
1. **[NPM](npm.md)** : installez le SDK Web sur votre site à l’aide du gestionnaire de modules NPM .

## Conditions préalables

Avant d’utiliser ou d’installer le SDK Web, vous devez répondre aux exigences suivantes :

* L’architecture de Adobe Experience Platform doit d’abord être configurée. Ces paramètres comprennent les schémas, les identités et les flux de données nécessaires.
* Vous devez disposer des autorisations appropriées configurées pour accéder aux outils appropriés. Par exemple, si votre entreprise décide d’utiliser l’extension de balise, vous devez disposer des autorisations appropriées pour accéder à l’interface utilisateur de la collecte de données. Pour plus d’informations, voir [Gestion des autorisations de collecte de données](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=fr) .
* Il est recommandé d’avoir un domaine propriétaire (CNAME). Si vous disposez déjà d’un CNAME pour Adobe Analytics, vous pouvez l’utiliser. Le test en développement fonctionne sans CNAME, mais Adobe recommande d’en avoir un avant de le publier en production. Pour plus d’informations, voir [Identifiants d’appareil propriétaire](../identity/first-party-device-ids.md) .

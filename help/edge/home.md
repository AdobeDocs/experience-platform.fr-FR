---
title: Présentation du SDK Web d’Adobe Experience Platform
description: Découvrez comment utiliser le SDK Web d’Adobe Experience Platform pour intégrer les fonctionnalités de Platform à votre Site Web.
keywords: SDK Web Adobe Experience Platform;SDK Web Platform;SDK Web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK web;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 100%

---

# Présentation du SDK Web d’Adobe Experience Platform {#overview}

Le SDK Web d’Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients d’Adobe Experience Cloud d’interagir avec les différents services d’[!DNL Experience Cloud] à travers Adobe Experience Platform Edge Network. Outre la bibliothèque JavaScript, il existe une [extension de balise](./extension/web-sdk-extension-configuration.md) pour vous aider à configurer votre SDK Web.

Pour obtenir un guide détaillé sur la configuration du SDK Web avec des balises et l’envoi de données aux solutions, veuillez consultez notre [tutoriel sur l’implémentation d’Adobe Experience Cloud dans le SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr).

>[!IMPORTANT]
>
>Ce produit évolue et se développe constamment pour prendre en charge de plus en plus de cas d’utilisation. Pour connaître les dernières nouveautés et notre prise en charge actuelle, consultez la [page des cas d’utilisation pris en charge](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] fait partie de la collection qui constitue [!DNL Adobe Experience Edge]. [!DNL Experience Edge] se compose des technologies suivantes :

* **[[!DNL Adobe Experience Platform Web SDK]](#overview) :** un SDK JavaScript et une extension de balise pour simplifier considérablement le déploiement de technologies [!DNL Adobe].
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview) :** une extension du SDK Mobile v5 pour permettre aux clients d’utiliser la nouvelle méthodologie de déploiement.
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md) :** un réseau distribué mondial de serveurs offrant une nouvelle méthodologie de déploiement des produits [!DNL Adobe].

[!DNL Adobe Experience Edge] est un nouveau cadre pour la collecte de données à faible latence, l’informatique enfichable et l’activation de données rapide sur tous les canaux adressables.

[!DNL Adobe Experience Edge] fournit un SDK consolidé unique pour chaque canal (JavaScript, mobile, côté serveur), qui envoie des données à un domaine Adobe commun (`adobedc.net`) et reçoit une seule payload pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle de périphérie unifiée et un cadre commun de services de plateforme facilitent l’intégration et le déploiement de nouvelles fonctionnalités dans cet environnement informatique en temps réel.  Cette architecture :

* diminue le délai de rentabilisation du client ;
* met fin au besoin d’intégrations « point à point » ;
* améliore les performances par rapport aux anciennes bibliothèques ;
* réduit les coûts ;
* augmente la vitesse d’innovation ;
* crée des avantages concurrentiels durables pour les clients Adobe.

Un seul système de périphérie consolidé permet aux clients de gérer leurs campagnes publicitaires, marketing ou personnalisées sur tous les canaux comme s’il s’agissait d’une expérience intégrée. Ce système à [!DNL Adobe] de fournir des services dont le coût total de possession est plus faible pour les clients.  Cela permet également d’accélérer l’innovation des produits en rendant le système de périphérie en temps réel enfichable. De plus, [!DNL Adobe] et ses clients peuvent ajouter plus rapidement de nouvelles fonctionnalités et intégrer une logique définie par le client à ce système en temps réel.

## Vue d’ensemble des vidéos {#video}

La vidéo suivante offre un aperçu d’Adobe Experience Platform [!DNL Web SDK] et d’Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliothèques remplacées par le SDK Web {#sdks}

Le SDK Web n’est pas seulement un wrapper des bibliothèques existantes. Il s’agit d’une toute nouvelle bibliothèque, écrite de A à Z pour intégrer les fonctionnalités des bibliothèques existantes. Son objectif est de mettre fin aux problèmes liés au déclenchement des balises dans le bon ordre, à l’incohérence avec les problèmes de contrôle de version des bibliothèques et à une meilleure gestion des dépendances. Il s’agit d’une nouvelle méthode d’implémentation, [open source](https://github.com/adobe/alloy), d’[!DNL Experience Cloud].

Le SDK Web de Platform remplace les SDK suivants :

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Outre une nouvelle bibliothèque, il existe un nouveau point d’entrée qui rationalise les requêtes HTTP vers les solutions Adobe. Auparavant, Visitor.js envoyait un appel de blocage au service d’ID de visiteur, puis AT.js envoyait un appel à Adobe Target, DIL.js envoyait un appel à Adobe Audience Manager, et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. Cette nouvelle bibliothèque et ce nouveau point d’entrée peuvent récupérer un identifiant ou une expérience [!DNL Target], envoyer les données à [!DNL Audience Manager] et les transmettre à Adobe Experience Platform grâce à un seul appel.

La vidéo suivante présente Adobe Experience Platform [!DNL Web SDK] et Adobe Experience Platform [!DNL Edge Network] en action. L’exemple vidéo utilise un appel unique à Adobe qui envoie les données à [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], et [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrer des bibliothèques existantes vers le SDK Web {#migrating-to-web-sdk}

Pour simplifier votre migration depuis l’une des [bibliothèques existantes](#sdks) vers le SDK Web, Adobe offre un chemin de mise à niveau simplifié vers le SDK Web. Il vous permet de migrer chaque page de votre site web vers le SDK Web, sans avoir à migrer l’intégralité de votre site Web en une seule fois..

Vous pouvez donc utiliser le SDK Web sur une page et laisser les bibliothèques existantes sur les autres pages, jusqu’à ce que vous puissiez les migrer également.

### Considérations relatives à la migration d’at.js vers le SDK Web {#considerations}

Avant de migrer des pages qui utilisent [!DNL at.js] dans le SDK Web, veillez à activer les options de configuration du SDK Web suivantes. Cela garantit que le profil du visiteur est conservé lors de la navigation à partir des pages avec [!DNL at.js ] aux pages utilisant le SDK Web.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [`targetMigrationEnabled`](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Les fonctionnalités Target suivantes ne sont pas prises en charge lors de la migration d’at.js vers le SDK Web :
> * [Offres de redirection](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=fr)
> * [Prise en charge CNAME et inter-domaines](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=fr)


Après la migration d’at.js vers le SDK Web, vous devez supprimer l’option `targetMigrationEnabled` de votre configuration.




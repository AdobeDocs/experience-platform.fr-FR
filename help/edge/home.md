---
title: Aide du SDK Web d’Adobe Experience Platform
seo-title: Aide du SDK Web d’Adobe Experience Platform
description: Découvrez le SDK Web d’Adobe Experience Platform et comment l’utiliser.
seo-description: Découvrez comment permettre aux clients de Adobe Experience Cloud d'interagir avec les différents services de l'Experience Cloud.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
translation-type: tm+mt
source-git-commit: bdd80b15258bf4e3c0dee1e260fd3469c76d5885
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 20%

---


# Qu’est-ce que le SDK Web Adobe Experience Platform ?

Adobe Experience Platform Web SDK is a client-side JavaScript library that allows customers of Adobe Experience Cloud to interact with the various services in the [!DNL Experience Cloud] through the Adobe Experience Platform Edge Network. Outre la bibliothèque JavaScript, il existe une extension [](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) Experience Platform Launch pour vous aider à configurer votre SDK Web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] fait partie de la collection qui constitue Experience Edge. Experience Edge est constitué de trois technologies :

* **[!DNL Adobe Experience Platform Web SDK]:** Un SDK JavaScript et une [!DNL Experience Platform Launch] extension pour simplifier considérablement le déploiement des [!DNL Adobe] technologies
* **Adobe Experience Platform Mobile SDK :** Extension du SDK mobile v5 pour permettre aux clients d’utiliser la nouvelle méthodologie de déploiement
* **[!DNL Adobe Experience Platform Edge Network]:** Réseau mondial distribué de serveurs qui permet une nouvelle méthodologie de déploiement de [!DNL Adobe] produits

The [!DNL Adobe Experience Edge] is a new framework for low-latency data collection, pluggable computing and rapid data activation across all addressable channels.

[!DNL Adobe Experience Edge] fournit un seul SDK consolidé pour chaque canal (JavaScript, Mobile, côté serveur), qui envoie les données à un domaine d’Adobe commun (`adobedc.net`) et reçoit une charge utile unique pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle d&#39;arête unifiée et un cadre commun de services de plate-forme facilitent la connexion et le déploiement de nouvelles fonctionnalités dans cet environnement informatique en temps réel.  Cette architecture :

* Réduit le temps passé par le client à la valeur
* Met fin au besoin d’intégrations &quot;ponctuelles&quot;
* Améliore les performances par rapport aux anciennes bibliothèques.
* Diminue les coûts
* Augmente la vitesse d&#39;innovation
* Créer des avantages concurrentiels durables pour les clients Adobes

Un système d&#39;arête unique consolidé permet aux clients de gérer leurs campagnes de publicité, de marketing ou de personnalisation sur tous les canaux en tant qu&#39;expérience intégrée.  Il permet [!DNL Adobe] de fournir des services avec un coût total de possession inférieur pour les clients.  Il permet également d&#39;accélérer l&#39;innovation des produits en rendant l&#39;avantage en temps réel enfichable et en permettant à ses clients [!DNL Adobe] et à ses clients d&#39;ajouter plus rapidement de nouvelles fonctionnalités et une logique définie par le client à ce système en temps réel.

## Vue d’ensemble des vidéos

La vidéo suivante donne un aperçu de la Adobe Experience Platform [!DNL Web SDK] et de la Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK remplacés par le SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform remplace les SDK suivants :

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Il ne s’agit pas seulement d’une enveloppe autour des bibliothèques existantes. Il s’agit d’une réécriture complète. Son objectif est de mettre fin aux défis avec des balises qui doivent se déclencher dans le bon ordre, des incohérences avec les défis de gestion des versions des bibliothèques et une meilleure gestion des dépendances. C&#39;est une nouvelle façon de mettre en oeuvre le [!DNL Experience Cloud] et c&#39;est le [open source](https://github.com/adobe/alloy).

Outre une nouvelle bibliothèque, il existe un nouveau point de terminaison qui rationalise les requêtes HTTP vers les solutions Adobe. Auparavant, Visitor.js envoyait un appel de blocage au service d’ID de visiteur, puis AT.js envoyait un appel à Adobe Target, DIL.js envoyait un appel à Adobe Audience Manager, et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. This new library and endpoint can retrieve an ID, fetch a [!DNL Target] experience, send data to [!DNL Audience Manager], and pass the data to Adobe Experience Platform in a single call.

La vidéo suivante montre Adobe Experience Platform [!DNL Web SDK] et Adobe Experience Platform [!DNL Edge Network] en action. L&#39;exemple vidéo utilise un appel unique à l&#39;Adobe qui envoie des données à [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]et [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Ce produit est en constante évolution et croissance pour prendre en charge de plus en plus de cas d&#39;utilisation. Pour rester au courant des dernières nouveautés, consultez notre carte des [cas d&#39;utilisation](https://github.com/adobe/alloy/projects/5)prise en charge. Nous tenons à jour cette situation avec les cas d&#39;utilisation que nous prenons actuellement en charge et ceux sur lesquels nous travaillons pour vous permettre de prendre les meilleures décisions possibles.

* **Cas d’utilisation non encore pris en charge :** Il s&#39;agit de cas d&#39;utilisation qui sont sur notre feuille de route à soutenir à l&#39;avenir.
* **Cas d’utilisation en cours :** Il s’agit des cas d’utilisation sur lesquels l’équipe travaille actuellement pour la publication.
* **Cas d’utilisation pris en charge :** Il s’agit des cas d’utilisation qui sont pris en charge et qui fonctionnent aujourd’hui.
* **Cas d&#39;utilisation que nous ne prendrons pas en charge :** Ce sont les cas d&#39;utilisation que nous avons pris la décision de ne pas appuyer.

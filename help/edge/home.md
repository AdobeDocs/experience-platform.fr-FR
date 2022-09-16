---
title: Présentation du SDK Web d’Adobe Experience Platform
description: Découvrez comment utiliser le SDK Web d’Adobe Experience Platform pour intégrer les fonctionnalités de Platform à votre Site Web.
keywords: SDK Web Adobe Experience Platform;SDK Web Platform;SDK Web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK web;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 71857ffc5e671f4d9a0502fb95d89d30fdec1f15
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 100%

---

# Présentation du SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients d’Adobe Experience Cloud d’interagir avec les différents services d’[!DNL Experience Cloud] à travers Adobe Experience Platform Edge Network. Outre la bibliothèque JavaScript, il existe une [extension de balise](./extension/web-sdk-extension-configuration.md) pour vous aider à configurer votre SDK Web.

**Pour obtenir un guide détaillé sur la configuration du SDK Web avec des balises et l’envoi de données aux solutions, consultez notre [Tutoriel sur l’implémentation d’Adobe Experience Cloud avec le SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr)**.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] est l’un des composants d’Experience Edge. Experience Edge se compose de trois technologies :

* **[!DNL Adobe Experience Platform Web SDK] :** un SDK JavaScript et une extension de balise pour simplifier considérablement le déploiement de technologies [!DNL Adobe].
* **SDK Mobile d’Adobe Experience Platform :** une extension du SDK Mobile v5 pour permettre aux clients d’utiliser la nouvelle méthodologie de déploiement.
* **[!DNL Adobe Experience Platform Edge Network] :** un réseau distribué mondial de serveurs offrant une nouvelle méthodologie de déploiement des produits [!DNL Adobe].

[!DNL Adobe Experience Edge] est un nouveau cadre pour la collecte de données à faible latence, l’informatique enfichable et l’activation de données rapide sur tous les canaux adressables.

[!DNL Adobe Experience Edge] fournit un SDK consolidé unique pour chaque canal (JavaScript, mobile, côté serveur), qui envoie des données à un domaine Adobe commun (`adobedc.net`) et reçoit une seule payload pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle de périphérie unifiée et un cadre commun de services de plateforme facilitent l’intégration et le déploiement de nouvelles fonctionnalités dans cet environnement informatique en temps réel.  Cette architecture :

* diminue le délai de rentabilisation du client ;
* met fin au besoin d’intégrations « point à point » ;
* améliore les performances par rapport aux anciennes bibliothèques ;
* réduit les coûts ;
* augmente la vitesse d’innovation ;
* crée des avantages concurrentiels durables pour les clients Adobe.

Un seul système de périphérie consolidé permet aux clients de gérer leurs campagnes publicitaires, marketing ou personnalisées sur tous les canaux comme s’il s’agissait d’une expérience intégrée.  Ce système à [!DNL Adobe] de fournir des services dont le coût total de possession est plus faible pour les clients.  Cela permet également d’accélérer l’innovation des produits en rendant le système de périphérie en temps réel enfichable. De plus, [!DNL Adobe] et ses clients peuvent ajouter plus rapidement de nouvelles fonctionnalités et intégrer une logique définie par le client à ce système en temps réel.

## Vue d’ensemble des vidéos

La vidéo suivante offre un aperçu d’Adobe Experience Platform [!DNL Web SDK] et d’Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK remplacés par le SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform remplace les SDK suivants :

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Il ne s’agit pas seulement d’une enveloppe autour des bibliothèques existantes. Il s’agit d’une réécriture complète. Son objectif est de mettre fin aux problèmes liés au déclenchement des balises dans le bon ordre, à l’incohérence avec les problèmes de contrôle de version des bibliothèques et à une meilleure gestion des dépendances. Il s’agit d’une nouvelle méthode d’implémentation, [open source](https://github.com/adobe/alloy), d’[!DNL Experience Cloud].

Outre une nouvelle bibliothèque, il existe un nouveau point de terminaison qui rationalise les requêtes HTTP vers les solutions Adobe. Auparavant, Visitor.js envoyait un appel de blocage au service d’ID de visiteur, puis AT.js envoyait un appel à Adobe Target, DIL.js envoyait un appel à Adobe Audience Manager, et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. Cette nouvelle bibliothèque et ce nouveau point d’entrée peuvent récupérer un identifiant ou une expérience [!DNL Target], envoyer les données à [!DNL Audience Manager] et les transmettre à Adobe Experience Platform grâce à un seul appel.

La vidéo suivante présente Adobe Experience Platform [!DNL Web SDK] et Adobe Experience Platform [!DNL Edge Network] en action. L’exemple vidéo utilise un appel unique à Adobe qui envoie les données à [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], et [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Ce produit évolue et se développe constamment pour prendre en charge de plus en plus de cas d’utilisation. Pour connaître les dernières nouveautés et notre prise en charge actuelle, consultez la [page des cas d’utilisation pris en charge](https://github.com/orgs/adobe/projects/18/views/1).

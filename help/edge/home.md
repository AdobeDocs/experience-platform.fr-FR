---
title: Présentation du SDK Web Adobe Experience Platform
description: Découvrez comment utiliser Adobe Experience Platform Web SDK pour intégrer des fonctionnalités de plate-forme à votre site Web.
keywords: Adobe Experience Platform Web SDK ; Platform Web SDK ; Web SDK ; edge ; Visiteur.js ; AppMeasurement.js ; AT.js ; DIL.js ; web sdk ; SDK ; web SDK ; Launch ; launch
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 15%

---


# Présentation du SDK Web Adobe Experience Platform

Adobe Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les différents services de [!DNL Experience Cloud] via le réseau Adobe Experience Platform Edge. Outre la bibliothèque JavaScript, il existe une [extension Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) pour vous aider à configurer votre SDK Web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] fait partie de la collection qui constitue Experience Edge. Experience Edge est constitué de trois technologies :

* **[!DNL Adobe Experience Platform Web SDK]:** Un SDK JavaScript et une  [!DNL Experience Platform Launch] extension pour simplifier considérablement le déploiement des  [!DNL Adobe] technologies
* **Adobe Experience Platform Mobile SDK :** extension du SDK mobile v5 pour permettre aux clients d’utiliser la nouvelle méthodologie de déploiement
* **[!DNL Adobe Experience Platform Edge Network]:** Réseau mondial distribué de serveurs permettant une nouvelle méthodologie de déploiement des  [!DNL Adobe] produits

[!DNL Adobe Experience Edge] est un nouveau cadre pour la collecte de données à faible latence, l&#39;informatique enfichable et l&#39;activation rapide des données dans tous les canaux adressables.

[!DNL Adobe Experience Edge] fournit un seul SDK consolidé pour chaque canal (JavaScript, Mobile, côté serveur), qui envoie les données à un domaine d’Adobe commun (`adobedc.net`) et reçoit une charge utile unique pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle d&#39;arête unifiée et un cadre commun de services de plate-forme facilitent la connexion et le déploiement de nouvelles fonctionnalités dans cet environnement informatique en temps réel.  Cette architecture :

* Réduit le temps passé par le client à la valeur
* Met fin au besoin d’intégrations &quot;ponctuelles&quot;
* Améliore les performances par rapport aux anciennes bibliothèques.
* Diminue les coûts
* Augmente la vitesse d&#39;innovation
* Créer des avantages concurrentiels durables pour les clients Adobes

Un système d&#39;arête unique consolidé permet aux clients de gérer leurs campagnes de publicité, de marketing ou de personnalisation sur tous les canaux en tant qu&#39;expérience intégrée.  Il permet à [!DNL Adobe] de fournir des services dont le coût total de possession est inférieur pour les clients.  Il permet également d&#39;accélérer l&#39;innovation des produits en rendant l&#39;avantage en temps réel enfichable et en permettant à [!DNL Adobe] et à ses clients d&#39;ajouter plus rapidement de nouvelles fonctionnalités et une logique définie par le client à ce système en temps réel.

## Vue d’ensemble des vidéos

La vidéo suivante donne un aperçu des [!DNL Web SDK] Adobe Experience Platform et [!DNL Edge Network] Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK remplacés par le SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform remplace les SDK suivants :

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Il ne s’agit pas seulement d’une enveloppe autour des bibliothèques existantes. Il s’agit d’une réécriture complète. Son objectif est de mettre fin aux défis avec des balises qui doivent se déclencher dans le bon ordre, des incohérences avec les défis de gestion des versions des bibliothèques et une meilleure gestion des dépendances. Il s’agit d’une nouvelle façon de mettre en oeuvre [!DNL Experience Cloud] et il s’agit de [open source](https://github.com/adobe/alloy).

Outre une nouvelle bibliothèque, il existe un nouveau point de terminaison qui rationalise les requêtes HTTP vers les solutions Adobe. Auparavant, Visitor.js envoyait un appel de blocage au service d’ID de visiteur, puis AT.js envoyait un appel à Adobe Target, DIL.js envoyait un appel à Adobe Audience Manager, et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. Cette nouvelle bibliothèque et ce nouveau point de terminaison peuvent récupérer un identifiant, récupérer une expérience [!DNL Target], envoyer des données à [!DNL Audience Manager] et transmettre les données à Adobe Experience Platform dans un seul appel.

La vidéo suivante présente Adobe Experience Platform [!DNL Web SDK] et Adobe Experience Platform [!DNL Edge Network] en action. L&#39;exemple vidéo utilise un appel unique à l&#39;Adobe qui envoie des données à [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] et [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Ce produit est en constante évolution et croissance pour prendre en charge de plus en plus de cas d&#39;utilisation. Pour connaître les dernières nouveautés, consultez notre [forum des cas d&#39;utilisation ](https://github.com/adobe/alloy/projects/5) pris en charge. Nous tenons à jour cette situation avec les cas d&#39;utilisation que nous prenons actuellement en charge et ceux sur lesquels nous travaillons pour vous permettre de prendre les meilleures décisions possibles.

* **Cas d&#39;utilisation non encore pris en charge :** Il s&#39;agit de cas d&#39;utilisation qui sont sur notre feuille de route à prendre en charge dans le futur.
* **Cas d’utilisation en cours :** il s’agit des cas d’utilisation sur lesquels l’équipe travaille actuellement pour la publication.
* **Cas d’utilisation pris en charge :** il s’agit des cas d’utilisation qui sont pris en charge et qui fonctionnent actuellement.
* **Cas d&#39;utilisation que nous ne prendrons pas en charge :** il s&#39;agit des cas d&#39;utilisation que nous avons pris la décision de ne pas prendre en charge.

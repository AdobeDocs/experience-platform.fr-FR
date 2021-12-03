---
title: Présentation du SDK Web Adobe Experience Platform
description: Découvrez comment utiliser le SDK Web de Adobe Experience Platform pour intégrer des fonctionnalités de Platform à votre site web.
keywords: SDK Web Adobe Experience Platform;SDK Web Platform;SDK Web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk Web;SDK;SDK Web;Launch;lancement
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 92344ca9c2daf603d866c8a3cc4e92b72a382fb1
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 14%

---

# Présentation du SDK Web Adobe Experience Platform

Le SDK Web de Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les différents services du [!DNL Experience Cloud] via Adobe Experience Platform Edge Network. Outre la bibliothèque JavaScript, il existe une [extension de balise](./extension/web-sdk-extension-configuration.md) pour obtenir de l’aide sur les configurations de votre SDK Web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] fait partie de la collection qui constitue Experience Edge. Experience Edge se compose de trois technologies :

* **[!DNL Adobe Experience Platform Web SDK]:** Un SDK JavaScript et une extension de balise pour simplifier considérablement le déploiement [!DNL Adobe] technologies
* **SDK Adobe Experience Platform Mobile :** Une extension du SDK mobile v5 pour permettre aux clients d’utiliser la nouvelle méthodologie de déploiement
* **[!DNL Adobe Experience Platform Edge Network]:** Un réseau mondial distribué de serveurs permettant une nouvelle méthodologie de déploiement [!DNL Adobe] products

Le [!DNL Adobe Experience Edge] est un nouveau cadre pour la collecte de données à faible latence, l’informatique enfichable et l’activation rapide des données sur tous les canaux adressables.

[!DNL Adobe Experience Edge] fournit un SDK consolidé unique pour chaque canal (JavaScript, mobile, côté serveur), qui envoie des données à un domaine d’Adobe commun (`adobedc.net`) et reçoit une seule payload pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle Edge unifiée et un framework de services de plateforme communs facilitent la connexion et le déploiement de nouvelles fonctionnalités dans cet environnement informatique en temps réel.  Cette architecture :

* Diminue le temps passé par le client pour augmenter sa valeur
* Met fin à la nécessité des intégrations &quot;ponctuelles&quot;
* Améliore les performances par rapport aux anciennes bibliothèques.
* Réduction des coûts
* Augmente la vitesse d’innovation
* Crée des avantages concurrentiels durables pour les clients Adobe

Un seul système de périphérie consolidé permet aux clients de gérer leurs campagnes publicitaires, marketing ou de personnalisation sur tous les canaux en tant qu’expérience intégrée.  Elle permet [!DNL Adobe] pour fournir des services dont le coût total de propriété est inférieur pour les clients.  Cela permet également d’accélérer l’innovation des produits en rendant la technologie de pointe en temps réel enfichable et en permettant [!DNL Adobe] et ses clients pour ajouter plus rapidement de nouvelles fonctionnalités et une logique définie par le client à ce système en temps réel.

## Vue d’ensemble des vidéos

La vidéo suivante présente un aperçu de Adobe Experience Platform [!DNL Web SDK] et Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK remplacés par le SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform remplace les SDK suivants :

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Il ne s’agit pas seulement d’une enveloppe autour des bibliothèques existantes. Il s’agit d’une réécriture complète. Son objectif est de mettre fin aux problèmes liés aux balises qui doivent se déclencher dans le bon ordre, à l’incohérence avec les problèmes de contrôle de version des bibliothèques et à une meilleure gestion des dépendances. Il s’agit d’une nouvelle méthode de mise en oeuvre de la variable [!DNL Experience Cloud] et que [open source](https://github.com/adobe/alloy).

Outre une nouvelle bibliothèque, il existe un nouveau point de terminaison qui rationalise les requêtes HTTP vers les solutions Adobe. Auparavant, Visitor.js envoyait un appel de blocage au service d’ID de visiteur, puis AT.js envoyait un appel à Adobe Target, DIL.js envoyait un appel à Adobe Audience Manager, et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. Cette nouvelle bibliothèque et ce nouveau point de terminaison peuvent récupérer un ID, récupérer un [!DNL Target] expérience, envoyer des données à [!DNL Audience Manager]et transmettez les données à Adobe Experience Platform dans un seul appel.

La vidéo suivante présente Adobe Experience Platform [!DNL Web SDK] et Adobe Experience Platform [!DNL Edge Network] en action. L’exemple vidéo utilise un appel unique à Adobe qui envoie des données à [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], et [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Ce produit évolue et se développe constamment pour prendre en charge de plus en plus de cas d’utilisation. Pour connaître la dernière version, reportez-vous à la section [page des cas d’utilisation pris en charge](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). Cette page répertorie les cas d’utilisation actuellement pris en charge, avec des liens vers d’autres informations lorsque disponibles.

* **Cas D’Utilisation Non Encore Pris En Charge :** Il s’agit de cas d’utilisation sur notre feuille de route qui seront pris en charge à l’avenir.
* **Cas D’Utilisation En Cours :** Il s’agit des cas d’utilisation sur lesquels l’équipe travaille actuellement pour la mise à jour.
* **Cas d’utilisation pris en charge :** Il s’agit des cas d’utilisation pris en charge et qui fonctionnent aujourd’hui.
* **Cas d’utilisation que nous ne prendrons pas en charge :** Il s’agit des cas d’utilisation que nous avons pris la décision de ne pas prendre en charge.

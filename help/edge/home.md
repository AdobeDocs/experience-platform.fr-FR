---
title: Aide du SDK Web d’Adobe Experience Platform
seo-title: Aide du SDK Web d’Adobe Experience Platform
description: Découvrez le SDK Web d’Adobe Experience Platform et comment l’utiliser.
seo-description: permettre aux clients d’Adobe Experience Cloud d’interagir avec les différents services dans Experience Cloud 
translation-type: tm+mt
source-git-commit: 3f52def8318f57cfc6534e15415d172e768a8614
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 33%

---


# Qu’est-ce que le SDK Web Adobe Experience Platform

Adobe Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients d’Adobe Experience Cloud d’interagir avec les différents services de l’Experience Cloud via Adobe Experience Platform Edge Network.

## SDK remplacés par le SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform remplace les SDK suivants :

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Il ne s’agit pas seulement d’une enveloppe autour des bibliothèques existantes. Il s’agit d’une réécriture complète. Son objectif est de mettre fin aux défis avec des balises qui doivent se déclencher dans le bon ordre, des incohérences avec les défis de gestion des versions des bibliothèques et une meilleure gestion des dépendances. C&#39;est une nouvelle façon de mettre en oeuvre l&#39;Experience Cloud et c&#39;est une source [ouverte](https://github.com/adobe/alloy).

Outre une nouvelle bibliothèque, il existe un nouveau point de terminaison qui rationalise les requêtes HTTP vers les solutions Adobe. Auparavant, Visitor.js envoyait un appel de blocage au service d’ID de visiteur, puis AT.js envoyait un appel à Adobe Target, DIL.js envoyait un appel à Adobe Audience Manager, et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. This new library and endpoint can retrieve an ID, fetch a [!DNL Target] experience, send data to Audience Manager, and pass the data to the Adobe Experience Platform in a single call.

## Prise en main

Nous vous recommandons vivement de [consulter notre guide](getting-started/quick-start-with-launch.md) de prise en main pour obtenir un didacticiel rapide sur la façon de commencer à utiliser Adobe Launch.

Ce produit est en constante évolution et croissance pour prendre en charge de plus en plus de cas d&#39;utilisation. Pour rester au courant des dernières nouveautés, consultez notre carte des [cas d&#39;utilisation](https://github.com/adobe/alloy/projects/5)prise en charge. Nous tenons à jour cette situation avec les cas d&#39;utilisation que nous prenons actuellement en charge et ceux sur lesquels nous travaillons pour vous permettre de prendre les meilleures décisions possibles.

* __Cas d&#39;utilisation non encore pris en charge__ - Il s&#39;agit de cas d&#39;utilisation qui sont sur notre feuille de route à soutenir dans l&#39;avenir.
* __Cas d&#39;utilisation en cours__ - Il s&#39;agit des cas d&#39;utilisation sur lesquels l&#39;équipe travaille actuellement pour la publication.
* __Cas__ d&#39;utilisation pris en charge - Il s&#39;agit des cas d&#39;utilisation qui sont pris en charge et fonctionnent aujourd&#39;hui.
* __Cas d&#39;utilisation que nous ne prendrons pas en charge__ - Il s&#39;agit des cas d&#39;utilisation que nous avons pris la décision de ne pas prendre en charge.

---
title: Aide du SDK Web d’Adobe Experience Platform
seo-title: Aide du SDK Web d’Adobe Experience Platform
description: Découvrez le SDK Web d’Adobe Experience Platform et comment l’utiliser.
seo-description: permettre aux clients d’Adobe Experience Cloud d’interagir avec les différents services dans Experience Cloud.
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 39%

---


# Qu’est-ce qu’Adobe Experience Platform Web SDK ?

Le SDK Web d’Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients d’Adobe Experience Cloud d’interagir avec les différents services d’Experience Cloud via le réseau Edge d’Adobe Experience Platform.

## SDK remplacés par le SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform remplace les SDK suivants :

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Il ne s’agit pas seulement d’une enveloppe autour des bibliothèques existantes. Il s’agit d’une réécriture complète. Son objectif est de mettre fin aux problèmes liés au déclenchement des balises dans le bon ordre, à l’incohérence avec les problèmes de contrôle de version des bibliothèques et à une meilleure gestion des dépendances. Il s’agit d’une nouvelle méthode d’implémentation d’Experience Cloud et d’une solution [open source.](https://github.com/adobe/alloy)

Outre une nouvelle bibliothèque, il existe un nouveau point de terminaison qui rationalise les requêtes HTTP vers les solutions Adobe. Auparavant, Visitor.js envoyait un appel de blocage au service d’ID de visiteur, puis AT.js envoyait un appel à Adobe Target, DIL.js envoyait un appel à Adobe Audience Manager, et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. Cette nouvelle bibliothèque et ce nouveau point de terminaison peuvent récupérer un identifiant, récupérer une expérience de Cible, envoyer des données à Audience Manager et transmettre les données à Adobe Experience Platform en un seul appel.

## Prise en main

Nous vous recommandons vivement de [consulter notre guide](getting-started/quick-start-with-launch.md) de prise en main pour obtenir un didacticiel rapide sur la façon de commencer à utiliser le lancement.

Ce produit est en constante évolution et croissance pour prendre en charge de plus en plus de cas d&#39;utilisation. Pour vous tenir au courant des dernières nouveautés, consultez notre carte des [cas d&#39;utilisation](https://github.com/adobe/alloy/projects/5)prise en charge. Nous tenons à jour cette situation avec les cas d&#39;utilisation que nous prenons actuellement en charge et ceux sur lesquels nous travaillons pour vous permettre de prendre les meilleures décisions possibles.

* __Cas d&#39;utilisation non encore pris en charge__ - sont des cas d&#39;utilisation qui sont sur notre feuille de route à faire à l&#39;avenir.
* __Cas d&#39;utilisation en cours__ - Il s&#39;agit des cas d&#39;utilisation sur lesquels l&#39;équipe travaille actuellement pour la publication.
* __Cas__ d&#39;utilisation pris en charge - Il s&#39;agit des cas d&#39;utilisation qui sont pris en charge et fonctionnent aujourd&#39;hui.
* __Cas d&#39;utilisation que nous ne prendrons pas en charge__ - Il s&#39;agit des cas d&#39;utilisation que nous avons pris la décision de ne pas prendre en charge.

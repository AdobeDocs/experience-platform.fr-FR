---
title: Aide du SDK Web d’Adobe Experience Platform
seo-title: Aide du SDK Web d’Adobe Experience Platform
description: Découvrez le SDK Web d’Adobe Experience Platform et comment l’utiliser.
seo-description: permettre aux clients d’Adobe Experience Cloud d’interagir avec les différents services dans Experience Cloud
translation-type: tm+mt
source-git-commit: 68361835437026c86af2402cc8400a3b3f32cb81

---


# (Version bêta) Présentation du SDK Web d’Adobe Experience Platform

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Le SDK Web d’Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients d’Adobe Experience Cloud d’interagir avec les différents services d’Experience Cloud via le réseau Edge d’Adobe Experience Platform.

## SDK remplacés par le SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform remplace les SDK suivants :

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Il ne s’agit pas seulement d’une enveloppe autour des bibliothèques existantes. Il s’agit d’une réécriture complète. Son objectif est de mettre fin aux problèmes liés au déclenchement des balises dans le bon ordre, à l’incohérence avec les problèmes de contrôle de version des bibliothèques et à une meilleure gestion des dépendances. Il s’agit d’une nouvelle méthode d’implémentation d’Experience Cloud.

Outre une nouvelle bibliothèque, il existe un nouveau point de terminaison qui rationalise les requêtes HTTP vers les solutions Adobe. Auparavant, Visitor.js envoyait un appel de blocage au service d’ID de visiteur, puis AT.js envoyait un appel à Adobe Target, DIL.js envoyait un appel à Adobe Audience Manager, et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. Cette nouvelle bibliothèque et ce nouveau point de terminaison peuvent récupérer un ID et une expérience Target, envoyer des données à Audience Manager et transmettre les données dans Adobe Experience Platform dans un seul appel.
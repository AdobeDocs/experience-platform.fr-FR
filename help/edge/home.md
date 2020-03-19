---
title: Aide du SDK Web d’Adobe Experience Platform
seo-title: Aide du SDK Web d’Adobe Experience Platform
description: Découvrez ce qu’est le SDK Web d’Adobe Experience Platform et comment il peut être utilisé.
seo-description: permettre aux clients d’Adobe Experience Cloud d’interagir avec les différents services dans Experience Cloud
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Qu’est-ce que le SDK Web d’Adobe Experience Platform ?

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Le SDK Web d’Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients d’Adobe Experience Cloud d’interagir avec les différents services d’Experience Cloud.

## SDK remplacés par le SDK Web d’Adobe Experience Platform

Le SDK Web d’Adobe Experience Platform remplace les SDK suivants :

* .js
* AppMeasurement.js
* AT.js
* DIL.js

Il ne s&#39;agit pas seulement d&#39;une enveloppe autour des bibliothèques existantes. C&#39;est une réécriture complète. Son objectif est de mettre fin aux défis liés au déclenchement des balises dans le bon ordre, à l’incohérence avec les problèmes de gestion des versions des bibliothèques et à une meilleure gestion des dépendances. Il s’agit d’une nouvelle méthode d’implémentation d’Experience Cloud.

Outre une nouvelle bibliothèque, il existe un nouveau point de fin qui rationalise les requêtes HTTP vers les solutions Adobe. Avant,.js envoyait un appel de blocage au service d’ID de, puis AT.js envoyait un appel à Adobe , DIL.js envoyait un appel à Adobe  Gestionnaire de , et finalement AppMeasurement.js envoyait un appel à Adobe Analytics. Cette nouvelle bibliothèque et ce nouveau point de fin peuvent récupérer un ID, récupérer une expérience de , envoyer des données à  Gestionnaire de  de et transmettre les données dans Adobe Experience Platform en un seul appel.
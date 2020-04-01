---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur Kafka
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Connecteur Kafka pour Adobe Experience Platform

Le connecteur de flux pour Adobe Experience Platform est basé sur Apache Kafka Connect. Cette bibliothèque peut être utilisée pour diffuser en temps réel des  JSON depuis les rubriques Kafka de votre centre de données, directement vers Experience Platform.

Le connecteur de flux est un connecteur d’évier (unidirectionnel), qui fournit des données des rubriques Kafka à un point de terminaison enregistré sur la plateforme d’expérience. Pour utiliser ce connecteur, vous devez télécharger la bibliothèque, l’ajouter à votre déploiement Kafka existant et configurer les rubriques Kafka dans l’URL HTTP Adobe Streaming. Le code supplémentaire **n’est pas** requis. Le connecteur prend en charge les fonctionnalités suivantes :

- Collecte authentifiée de données
- Correspondance des messages pour réduire les appels réseau et augmenter le débit

Pour plus d&#39;informations sur le connecteur Kafka, y compris des instructions sur la configuration du connecteur, veuillez lire le guide de [prise en main](https://github.com/adobe/experience-platform-streaming-connect). Pour un flux de travail plus détaillé, veuillez lire le guide [du](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)développeur.
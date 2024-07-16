---
keywords: Experience Platform;accueil;rubriques populaires;kafka;connecteur kafka;Kafka;
solution: Experience Platform
title: Connecteur Kafka
description: Le connecteur de flux pour Adobe Experience Platform est basé sur Apache Kafka Connect. Cette bibliothèque peut être utilisée pour diffuser en temps réel des événements JSON depuis les rubriques Kafka de votre centre de données directement vers Experience Platform.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 26%

---

# Connecteur [!DNL Kafka] pour Adobe Experience Platform

Le connecteur de flux pour Adobe Experience Platform est basé sur [!DNL Apache Kafka Connect]. Cette bibliothèque peut être utilisée pour diffuser en temps réel des événements JSON de [!DNL Kafka] rubriques de votre centre de données directement vers [!DNL Experience Platform].

Le connecteur de flux est un connecteur unidirectionnel, qui fournit des données des rubriques [!DNL Kafka] à un point de terminaison enregistré sur [!DNL Experience Platform]. Pour utiliser ce connecteur, vous devez télécharger la bibliothèque, l’ajouter à votre déploiement [!DNL Kafka] existant et configurer la ou les rubriques [!DNL Kafka] sur l’URL HTTP en flux continu Adobe. **Aucun** code supplémentaire n’est requis. Le connecteur est compatible avec les fonctionnalités suivantes :

- Collecte de données authentifiée
- Messages par lots pour réduire les appels réseau et augmenter le débit

Pour plus d’informations sur le connecteur [!DNL Kafka], y compris des instructions sur la configuration du connecteur, consultez le [guide de prise en main](https://github.com/adobe/experience-platform-streaming-connect). Pour un workflow plus détaillé, veuillez consulter le [guide de développement](https://www.adobe.com/go/kafka-connector-developer-guide).

---
keywords: Experience Platform ; accueil ; sujets populaires ; kafka ; connecteur kafka ; Kafka ;
solution: Experience Platform
title: Connecteur Kafka
topic: overview
description: Le connecteur de flux pour Adobe Experience Platform est basé sur Apache Kafka Connect. Cette bibliothèque peut être utilisée pour diffuser en temps réel les événements JSON des rubriques Kafka de votre centre de données directement vers l’Experience Platform.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 30%

---


# [!DNL Kafka]Connecteur pour Adobe Experience Platform

Le connecteur de flux pour Adobe Experience Platform est basé sur [!DNL Apache Kafka Connect]. Cette bibliothèque peut être utilisée pour diffuser en temps réel les événements JSON de [!DNL Kafka] rubriques de votre centre de données directement vers [!DNL Experience Platform].

Le connecteur de flux est un connecteur d’évier (à sens unique), qui fournit des données de [!DNL Kafka] rubriques à un point de terminaison enregistré sur [!DNL Experience Platform]. Pour utiliser ce connecteur, vous devez télécharger la bibliothèque, l’ajouter à votre déploiement [!DNL Kafka] existant et configurer les [!DNL Kafka] rubriques dans l’URL HTTP de diffusion en continu de l’Adobe. **Aucun** code supplémentaire n’est requis. Le connecteur est compatible avec les fonctionnalités suivantes :

- Collecte de données authentifiée
- Messages par lots pour réduire les appels réseau et augmenter le débit

Pour plus d&#39;informations sur le connecteur [!DNL Kafka], y compris des instructions sur la façon de configurer le connecteur, consultez le [guide de prise en main](https://github.com/adobe/experience-platform-streaming-connect). Pour un workflow plus détaillé, veuillez consulter le [guide de développement](https://www.adobe.com/go/kafka-connector-developer-guide).
---
keywords: Experience Platform ; accueil ; sujets populaires ; kafka ; connecteur kafka ; Kafka ;
solution: Experience Platform
title: Connecteur Kafka
topic-legacy: overview
description: Le connecteur de flux pour Adobe Experience Platform est basé sur Apache Kafka Connect. Cette bibliothèque peut être utilisée pour diffuser en temps réel les événements JSON des rubriques Kafka de votre centre de données directement vers l’Experience Platform.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 29%

---

# [!DNL Kafka]Connecteur pour Adobe Experience Platform

Le connecteur de flux pour Adobe Experience Platform est basé sur [!DNL Apache Kafka Connect]. Cette bibliothèque peut être utilisée pour diffuser en temps réel les événements JSON de [!DNL Kafka] rubriques de votre centre de données directement vers [!DNL Experience Platform].

Le connecteur de flux est un connecteur d’évier (à sens unique), qui fournit des données de [!DNL Kafka] rubriques à un point de terminaison enregistré sur [!DNL Experience Platform]. Pour utiliser ce connecteur, vous devez télécharger la bibliothèque, l’ajouter à votre déploiement [!DNL Kafka] existant et configurer les [!DNL Kafka] rubriques dans l’URL HTTP de diffusion en continu de l’Adobe. **Aucun** code supplémentaire n’est requis. Le connecteur est compatible avec les fonctionnalités suivantes :

- Collecte de données authentifiée
- Messages par lots pour réduire les appels réseau et augmenter le débit

Pour plus d&#39;informations sur le connecteur [!DNL Kafka], y compris des instructions sur la façon de configurer le connecteur, consultez le [guide de prise en main](https://github.com/adobe/experience-platform-streaming-connect). Pour un workflow plus détaillé, veuillez consulter le [guide de développement](https://www.adobe.com/go/kafka-connector-developer-guide).

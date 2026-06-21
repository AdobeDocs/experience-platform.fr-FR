---
keywords: Experience Platform;accueil;rubriques populaires;kafka;connecteur kafka;Kafka;
solution: Experience Platform
title: Connecteur Kafka
description: Le connecteur de flux pour Adobe Experience Platform est basé sur Apache Kafka Connect. Cette bibliothèque peut être utilisée pour diffuser en temps réel des événements JSON depuis les rubriques Kafka de votre centre de données, directement vers Experience Platform.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
TQID: https://experienceleague.adobe.com/LujCg-p47RA8z5YZ1OtJ7LjuG1cfRqbaWCRfZCmbvyM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 195
ht-degree: 27%

---

# Connecteur [!DNL Kafka] pour Adobe Experience Platform

Le connecteur de flux pour Adobe Experience Platform est basé sur [!DNL Apache Kafka Connect]. Cette bibliothèque peut être utilisée pour diffuser en temps réel des événements JSON depuis [!DNL Kafka] rubriques de votre centre de données directement vers [!DNL Experience Platform].

Le connecteur de flux est un connecteur unidirectionnel qui fournit des données de rubriques [!DNL Kafka] à un point d’entrée enregistré sur [!DNL Experience Platform]. Pour utiliser ce connecteur, vous devez télécharger la bibliothèque, l’ajouter à votre déploiement [!DNL Kafka] existant et configurer la ou les rubriques [!DNL Kafka] à l’URL HTTP de diffusion en continu Adobe. **Aucun** code supplémentaire n’est requis. Le connecteur est compatible avec les fonctionnalités suivantes :

- Collecte de données authentifiée
- Messages par lots pour réduire les appels réseau et augmenter le débit

Pour plus d’informations sur le connecteur [!DNL Kafka], y compris des instructions sur la configuration du connecteur, consultez le [ guide de prise en main ](https://github.com/adobe/experience-platform-streaming-connect). Pour un workflow plus détaillé, veuillez consulter le [guide de développement](https://www.adobe.com/go/kafka-connector-developer-guide).

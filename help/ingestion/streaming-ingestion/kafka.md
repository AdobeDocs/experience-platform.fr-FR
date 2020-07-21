---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur Kafka
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 36%

---


# [!DNL Kafka]Connecteur pour Adobe Experience Platform

The stream connector for Adobe Experience Platform is based on [!DNL Apache Kafka Connect]. This library can be used to stream JSON events from [!DNL Kafka] topics in your data center directly to [!DNL Experience Platform] in real-time.

The stream connector is a sink (one-way) connector, delivering data from [!DNL Kafka] topics to a registered endpoint on [!DNL Experience Platform]. To use this connector, you must download the library, add it to your existing [!DNL Kafka] deployment, and configure the [!DNL Kafka] topic(s) to the Adobe Streaming HTTP URL. **Aucun** code supplémentaire n’est requis. Le connecteur est compatible avec les fonctionnalités suivantes :

- Collecte de données authentifiée
- Messages par lots pour réduire les appels réseau et augmenter le débit

For more information on the [!DNL Kafka] connector, including instructions on how to set up the connector, please read the [getting started guide](https://github.com/adobe/experience-platform-streaming-connect). Pour un workflow plus détaillé, veuillez consulter le [guide de développement](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).
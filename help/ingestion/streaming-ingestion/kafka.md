---
keywords: Experience Platform;accueil;rubriques les plus consultées;kafka;connecteur kafka;Kafka;
solution: Experience Platform
title: Connecteur Kafka
topic-legacy: overview
description: Le connecteur de flux pour Adobe Experience Platform est basé sur Apache Kafka Connect. Cette bibliothèque peut être utilisée pour diffuser en temps réel des événements JSON depuis les rubriques Kafka de votre centre de données directement vers Experience Platform.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: 5a3aa74ca7319235c10902422abc0e897ad823b8
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 23%

---

# [!DNL Kafka] connecteur pour Adobe Experience Platform (obsolète)

>[!IMPORTANT]
>
>Le connecteur Kafka est obsolète. Pour créer une connexion en continu et importer des données dans Adobe Experience Platform, consultez le tutoriel sur [création d’une connexion en continu à l’API HTTP](../../sources/connectors/streaming/http.md)

Le connecteur de flux pour Adobe Experience Platform est basé sur [!DNL Apache Kafka Connect]. Cette bibliothèque peut être utilisée pour diffuser des événements JSON à partir de [!DNL Kafka] rubriques de votre centre de données directement vers [!DNL Experience Platform] en temps réel.

Le connecteur de flux est un connecteur unidirectionnel, qui fournit des données à partir de [!DNL Kafka] rubriques vers un point de terminaison enregistré sur [!DNL Experience Platform]. Pour utiliser ce connecteur, vous devez télécharger la bibliothèque et l’ajouter à votre [!DNL Kafka] et configurez la variable [!DNL Kafka] rubrique(s) vers l’URL HTTP de diffusion en continu de l’Adobe. **Aucun** code supplémentaire n’est requis. Le connecteur est compatible avec les fonctionnalités suivantes :

- Collecte de données authentifiée
- Messages par lots pour réduire les appels réseau et augmenter le débit

Pour plus d’informations sur la variable [!DNL Kafka] Connecteur, y compris des instructions sur la configuration du connecteur, veuillez lire la section [guide de prise en main](https://github.com/adobe/experience-platform-streaming-connect). Pour un workflow plus détaillé, veuillez consulter le [guide de développement](https://www.adobe.com/go/kafka-connector-developer-guide).

---
keywords: Experience Platform;home;popular topics;data ingestion;ingested data;streaming;overview;streaming ingestion;latency;streaming latency;
solution: Experience Platform
title: Présentation de la fonction d’ingestion par flux d’Adobe Experience Platform
topic: overview
description: L’ingestion par flux pour Adobe Experience Platform fournit aux utilisateurs une méthode pour envoyer en temps réel des données de périphériques côté client et côté serveur vers Experience Platform.
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 36%

---


# Présentation de l’ingestion par flux

Streaming ingestion for Adobe Experience Platform provides users a method to send data from client and server-side devices to [!DNL Experience Platform] in real-time.

## Que pouvez-vous faire avec l’ingestion par flux ?

Adobe Experience Platform enables you to drive coordinated, consistent, and relevant experiences by generating a [!DNL Real-time Customer Profile] for each of your individual customers. Streaming ingestion plays a key role in building these profiles by enabling you to deliver [!DNL Profile] data into the [!DNL Data Lake] with as little latency as possible.

La vidéo suivante est conçue pour vous aider à comprendre l’assimilation en flux continu et présente les concepts ci-dessus.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Stream profile records and [!DNL ExperienceEvents]

With streaming ingestion, users can stream profile records and [!DNL ExperienceEvents] to [!DNL Platform] in seconds to help drive real-time personalization. All data sent to streaming ingestion APIs is automatically persisted in the [!DNL Data Lake].

Pour plus d’informations, consultez le [guide de création d’une connexion en continu](../tutorials/create-streaming-connection.md).

### Diffusion vers les jeux de données

Once you are confident that your data is clean, you can enable your datasets for [!DNL Real-time Customer Profile] and [!DNL Identity Service].

For more information on enabling a dataset for [!DNL Profile] and [!DNL Identity Service], please read the [configure a dataset guide](../../profile/tutorials/dataset-configuration.md).

## What is the expected latency for streaming ingestion on [!DNL Platform]?

| Destination | Latence attendue |
| --------- | ---------------- |
| Real-time Customer Profile | &lt; 1 minute |
| Lac de données | &lt; 60 minutes |

## Extension Adobe Experience Platform

Vous pouvez utiliser l’extension Adobe Experience Platform pour créer une connexion en continu. The [!DNL Experience Platform] extension provides actions to send beacons formatted in [!DNL Experience Data Model] (XDM) for real-time ingestion to [!DNL Experience Platform]. Pour plus d’informations, consultez la documentation de [l’extension Experience Platform](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html).
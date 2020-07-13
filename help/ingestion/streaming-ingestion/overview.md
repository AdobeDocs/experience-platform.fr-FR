---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de la fonction d’ingestion par flux d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 93%

---


# Présentation de l’ingestion par flux

L’ingestion par flux pour Adobe Experience Platform fournit aux utilisateurs une méthode pour envoyer en temps réel des données de périphériques côté client et côté serveur vers Experience Platform.

## Que pouvez-vous faire avec l’ingestion par flux ?

Adobe Experience Platform vous permet de générer des expériences coordonnées, cohérentes et pertinentes en générant un profil client en temps réel pour chacun de vos clients. L’ingestion par flux joue un rôle clé dans la création de ces profils en vous permettant de fournir des données de profil dans le lac de données avec le moins de latence possible.

La vidéo suivante est conçue pour vous aider à comprendre l’assimilation en flux continu et présente les concepts ci-dessus.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Diffusion d’enregistrements de profil et d’ExperienceEvent

Grâce à l’ingestion par flux, les utilisateurs peuvent diffuser en quelques secondes des enregistrements de profil et des ExperienceEvent sur Platform afin de faciliter la personnalisation en temps réel. Toutes les données envoyées aux API d’ingestion par flux sont automatiquement conservées dans le lac de données.

Pour plus d’informations, consultez le [guide de création d’une connexion en continu](../tutorials/create-streaming-connection.md).

### Diffusion vers les jeux de données

Une fois que vous êtes certain que vos données sont propres, vous pouvez activer vos jeux de données pour Real-time Customer Profile et Identity Service.

Pour plus d’informations sur l’activation d’un jeu de données pour Profile et Identity Service, consultez le [guide de configuration d’un jeu de données](../../profile/tutorials/dataset-configuration.md).

## Quelle est la latence attendue sur Platform pour l’ingestion par flux ?

| Destination | Latence attendue |
| --------- | ---------------- |
| Real-time Customer Profile | &lt; 1 minute |
| Lac de données | &lt; 60 minutes |

## Extension Adobe Experience Platform

Vous pouvez utiliser l’extension Adobe Experience Platform pour créer une connexion en continu. L’extension Experience Platform fournit des actions permettant d’envoyer des balises formatées dans Experience Data Model (XDM) pour l’ingestion en temps réel vers Experience Platform. Pour plus d’informations, consultez la documentation de [l’extension Experience Platform](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html).
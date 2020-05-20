---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’intuition de flux continu Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: a570a7a3d905c4618d80f56f01747cced1d124e8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---


# Présentation de l&#39;assimilation en flux continu

L’assimilation en flux continu pour Adobe Experience Platform fournit aux utilisateurs une méthode d’envoi en temps réel de données depuis des périphériques client et serveur vers Experience Platform.

## Que pouvez-vous faire avec l&#39;ingestion en flux continu ?

Adobe Experience Platform vous permet de générer des expériences coordonnées, cohérentes et pertinentes en générant un Profil client en temps réel pour chacun de vos clients. La diffusion en continu de l&#39;assimilation joue un rôle clé dans la création de ces profils en vous permettant de fournir des données de Profil dans Data Lake avec le moins de latence possible.

### Enregistrements de profil de diffusion en continu et événements d’expérience

Avec l’assimilation en flux continu, les utilisateurs peuvent diffuser en quelques secondes des enregistrements de profil et des événements d’expérience sur la plate-forme pour faciliter la personnalisation en temps réel. Toutes les données envoyées aux API d’assimilation en flux continu sont automatiquement conservées dans Data Lake.

Pour plus d&#39;informations, consultez le guide [de](../tutorials/create-streaming-connection.md) création d&#39;une connexion en flux continu.

### Diffusion en continu des jeux de données

Une fois que vous avez la certitude que vos données sont propres, vous pouvez activer vos jeux de données pour le service de Profil client et d’identité en temps réel.

Pour plus d&#39;informations sur l&#39;activation d&#39;un jeu de données pour Profil et Identity Service, consultez le guide [](../../profile/tutorials/dataset-configuration.md)Configurer un jeu de données.

## Quelle est la latence attendue pour l’assimilation en flux continu sur la plate-forme ?

| Destination | Latence attendue |
| --------- | ---------------- |
| Profil client en temps réel | &lt; 1 minute |
| Data Lake | &lt; 60 minutes |

## Extension Adobe Experience Platform

Vous pouvez utiliser l’extension Adobe Experience Platform pour créer une nouvelle connexion de diffusion en continu. L’extension de plate-forme d’expérience fournit des actions permettant d’envoyer des balises formatées dans le modèle de données d’expérience (XDM) pour l’assimilation en temps réel à la plate-forme d’expérience. Pour plus d’informations, consultez la documentation [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .
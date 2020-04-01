---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de la fonction d’importation en flux continu d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: a570a7a3d905c4618d80f56f01747cced1d124e8

---


# Présentation de l&#39;assimilation en flux continu

L’assimilation en flux continu pour Adobe Experience Platform fournit aux utilisateurs une méthode d’envoi en temps réel des données des périphériques client et serveur vers Experience Platform.

## Que pouvez-vous faire avec l&#39;ingestion en flux continu ?

Adobe Experience Platform vous permet de générer des expériences coordonnées, cohérentes et pertinentes en générant une  Client en temps réel pour chacun de vos clients. La diffusion en flux continu de l’ingestion joue un rôle clé dans la création de ces  en vous permettant de fournir des données  dans Data Lake avec le moins de latence possible.

### Enregistrements de  de diffusion en continu et événements d’expérience

Avec l’assimilation en flux continu, les utilisateurs peuvent diffuser en quelques secondes des enregistrements  et des événements d’expérience sur une plateforme afin de faciliter la personnalisation en temps réel. Toutes les données envoyées aux API d’assimilation en flux continu sont automatiquement conservées dans Data Lake.

Pour plus d&#39;informations, consultez le guide [](../tutorials/create-streaming-connection.md) de création d&#39;une connexion en flux continu.

### Flux vers des jeux de données

Une fois que vous êtes certain que vos données sont propres, vous pouvez activer vos jeux de données pour  client et service d’identité en temps réel.

Pour plus d&#39;informations sur l&#39;activation d&#39;un jeu de données pour les services d&#39; et d&#39;identité, consultez le guide [Configuration d&#39;un jeu de données](../../profile/tutorials/dataset-configuration.md).

## Quelle est la latence attendue pour l’assimilation en flux continu sur la plateforme ?

| Destination | Latence attendue |
| --------- | ---------------- |
| Profil client en temps réel | &lt; 1 minute |
| Lac Data | &lt; 60 minutes |

## Extension Adobe Experience Platform

Vous pouvez utiliser l’extension Adobe Experience Platform pour créer une connexion en flux continu. L’extension de plateforme d’expérience fournit des actions permettant d’envoyer des balises formatées dans le modèle de données d’expérience (XDM) pour l’assimilation en temps réel vers la plateforme d’expérience. Pour plus d’informations, consultez la documentation de [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .
---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion de données;données ingérées;diffusion en continu;présentation;ingestion par flux;latence;latence de diffusion en continu;latence ;
solution: Experience Platform
title: Présentation de l’ingestion par flux
topic-legacy: overview
description: L’ingestion par flux pour Adobe Experience Platform fournit aux utilisateurs une méthode pour envoyer en temps réel des données de périphériques côté client et côté serveur vers Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 17%

---

# Présentation de l’ingestion par flux

L’ingestion par flux pour Adobe Experience Platform fournit aux utilisateurs une méthode pour envoyer des données depuis des périphériques côté client et côté serveur vers [!DNL Experience Platform] en temps réel.

## Que pouvez-vous faire avec l’ingestion par flux ?

Adobe Experience Platform vous permet de générer des expériences coordonnées, cohérentes et pertinentes en générant une [!DNL Real-Time Customer Profile] pour chacun de vos clients. L’ingestion par flux joue un rôle clé dans la création de ces profils en vous permettant de diffuser des [!DNL Profile] dans la variable [!DNL Data Lake] avec le moins de latence possible.

La vidéo suivante est conçue pour vous aider à comprendre l’ingestion par flux et décrit les concepts ci-dessus.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Diffusion en continu des enregistrements de profil et [!DNL ExperienceEvents]

Grâce à l’ingestion par flux, les utilisateurs peuvent diffuser en continu des enregistrements de profil et des [!DNL ExperienceEvents] to [!DNL Platform] en secondes pour faciliter la personnalisation en temps réel. Toutes les données envoyées aux API d’ingestion par flux sont automatiquement conservées dans la variable [!DNL Data Lake].

Pour plus d’informations, consultez le [guide de création d’une connexion en continu](../tutorials/create-streaming-connection.md).

### Diffusion vers les jeux de données

Une fois que vous êtes certain que vos données sont propres, vous pouvez activer vos jeux de données pour [!DNL Real-Time Customer Profile] et [!DNL Identity Service].

Pour plus d’informations sur l’activation d’un jeu de données pour [!DNL Profile] et [!DNL Identity Service], veuillez lire la [configuration d’un guide de jeu de données](../../profile/tutorials/dataset-configuration.md).

## Quelle est la latence attendue sur l’ingestion par flux ? [!DNL Platform]?

| Destination | Latence attendue |
| --------- | ---------------- |
| Profil client en temps réel | &lt; 1 minute |
| Lac de données | &lt; 60 minutes |

## Instructions de requête par seconde (RPS) sur l’ingestion par flux

Le tableau ci-dessous présente des conseils sur les limites de requête par seconde pour l’ingestion par flux.

| Limite RPS | Notes |
| --- | --- |
| 1 000 demandes par seconde | Ils peuvent contenir plusieurs messages lors de l’utilisation de `/collection/batch` point de terminaison . |
| 1 000 messages individuels par seconde | Les messages peuvent être regroupés en moins de requêtes réelles lors de l’utilisation de la variable `/collection/batch` point de terminaison . |

>[!IMPORTANT]
>
>La limite appliquée devient **60 demandes par minute** lors de l’utilisation de la validation synchrone, car elle est destinée à des fins de débogage.

## Extension Adobe Experience Platform

Vous pouvez utiliser l’extension Adobe Experience Platform pour créer une connexion en continu. Le [!DNL Experience Platform] L’extension fournit des actions pour envoyer des balises formatées dans [!DNL Experience Data Model] (XDM) pour l’ingestion en temps réel vers [!DNL Experience Platform]. Pour plus d’informations, consultez la documentation de [l’extension Experience Platform](../../tags/extensions/client/sdk/overview.md).

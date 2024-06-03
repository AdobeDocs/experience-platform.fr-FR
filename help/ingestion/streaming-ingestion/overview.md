---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion de données;données ingérées;diffusion en continu;présentation;ingestion par flux;latence;latence de diffusion en continu;latence ;
solution: Experience Platform
title: Vue d’ensemble de l’ingestion en flux continu
description: L’ingestion par flux pour Adobe Experience Platform fournit aux utilisateurs une méthode pour envoyer en temps réel des données de périphériques côté client et côté serveur vers Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: d6424e2a9afc046f4bff329797954fd43939a819
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 14%

---

# Présentation de l’ingestion par flux

L’ingestion par flux pour Adobe Experience Platform fournit aux utilisateurs une méthode pour envoyer des données depuis des périphériques côté client et côté serveur vers [!DNL Experience Platform] en temps réel.

## Que pouvez-vous faire avec l’ingestion par flux ?

Adobe Experience Platform vous permet de générer des expériences coordonnées, cohérentes et pertinentes en générant une [!DNL Real-Time Customer Profile] pour chacun de vos clients. L’ingestion par flux joue un rôle clé dans la création de ces profils en vous permettant de diffuser des [!DNL Profile] dans la variable [!DNL Data Lake] avec le moins de latence possible.

La vidéo suivante est conçue pour vous aider à comprendre l’ingestion par flux et décrit les concepts ci-dessus.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Diffusion des enregistrements de profil et [!DNL ExperienceEvents]

Grâce à l’ingestion par flux, les utilisateurs peuvent diffuser en continu des enregistrements de profil et des [!DNL ExperienceEvents] to [!DNL Platform] en secondes pour faciliter la personnalisation en temps réel. Toutes les données envoyées aux API d’ingestion par flux sont automatiquement conservées dans la variable [!DNL Data Lake].

Pour plus d’informations, consultez le [guide de création d’une connexion en continu](../tutorials/create-streaming-connection.md).

### Diffusion vers les jeux de données

Une fois que vous êtes certain que vos données sont propres, vous pouvez activer vos jeux de données pour [!DNL Real-Time Customer Profile] et [!DNL Identity Service].

Pour plus d’informations sur l’activation d’un jeu de données pour [!DNL Profile] et [!DNL Identity Service], veuillez lire la [configuration d’un guide de jeu de données](../../profile/tutorials/dataset-configuration.md).

## Quelle est la latence attendue sur Experience Platform pour l’ingestion par flux ?

>[!IMPORTANT]
>
>Les barrières de sécurité pour l’ingestion par flux sont calculées au niveau de l’organisation et non au niveau de l’environnement de test. Cela signifie que votre utilisation des données par environnement de test est liée au total des droits d’utilisation des licences qui correspondent à l’ensemble de votre organisation. En outre, l’utilisation des données dans les environnements de test de développement est limitée à 10 % de vos profils totaux. Pour plus d’informations sur les droits d’utilisation des licences, consultez la section [guide des bonnes pratiques relatives à la gestion des données](../../landing/license-usage-and-guardrails/data-management-best-practices.md).

| Destination | Latence attendue |
| --------- | ---------------- |
| Profil client en temps réel | &lt; 15 minutes au 95e percentile |
| Lac de données | &lt; 60 minutes |

## Instructions de requête par seconde (RPS) sur l’ingestion par flux

Le tableau ci-dessous présente des conseils sur les limites de requête par seconde pour l’ingestion par flux.

| Limite RPS | Notes |
| --- | --- |
| 1 000 demandes par seconde | Ils peuvent contenir plusieurs messages lorsque vous utilisez `/collection/batch` point de terminaison . |
| 1 000 messages individuels par seconde | Les messages peuvent être regroupés en moins de requêtes réelles lors de l’utilisation de la variable `/collection/batch` point de terminaison . |

>[!IMPORTANT]
>
>La limite appliquée devient **60 demandes par minute** lors de l’utilisation de la validation synchrone, car elle est destinée à des fins de débogage.

## Extension Adobe Experience Platform

Vous pouvez utiliser l’extension Adobe Experience Platform pour créer une connexion en continu. La variable [!DNL Experience Platform] L’extension fournit des actions pour envoyer des balises formatées dans [!DNL Experience Data Model] (XDM) pour l’ingestion en temps réel vers [!DNL Experience Platform]. Pour plus d’informations, consultez la documentation de [l’extension Experience Platform](../../tags/extensions/client/web-sdk/overview.md).

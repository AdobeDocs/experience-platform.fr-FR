---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion de données;données ingérées;diffusion en continu;présentation;ingestion en flux continu;latence;latence en flux continu;
solution: Experience Platform
title: Vue d’ensemble de l’ingestion en flux continu
description: Découvrez l’ingestion par flux dans Adobe Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
TQID: https://experienceleague.adobe.com/htRFdI6kObtLCuiaLwexpBLQVRe5-TfcxLgeRLrHZTw
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: b784da9a-7978-4766-bf1f-5ab2b23d894a
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
  - id: f5efb499-54f9-432b-ac5c-599dbac103af
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 437
ht-degree: 15%

---

# Présentation de l’ingestion en flux continu

L’ingestion par flux pour Adobe Experience Platform fournit aux utilisateurs une méthode pour envoyer en temps réel des données d’appareils côté client et côté serveur vers Experience Platform.

## Que pouvez-vous faire avec l’ingestion en flux continu ?

Adobe Experience Platform vous permet de générer des expériences coordonnées, cohérentes et pertinentes en générant un profil client en temps réel pour chacun de vos clients. L’ingestion par flux joue un rôle clé dans la création de ces profils en vous permettant de diffuser des données de profil dans le lac de données avec le moins de latence possible.

La vidéo suivante est conçue pour vous aider à comprendre l’ingestion par flux et décrit les concepts ci-dessus.

>[!VIDEO](https://video.tv.adobe.com/v/31636?captions=fre_fr&quality=12&learn=on)

### Diffusion d’enregistrements de profil et de [!DNL ExperienceEvents]

Grâce à l’ingestion par flux, les utilisateurs peuvent diffuser des enregistrements de profil et des [!DNL ExperienceEvents] à Experience Platform en quelques secondes afin d’orienter la personnalisation en temps réel. Toutes les données envoyées aux API d’ingestion en flux continu sont automatiquement conservées dans le lac de données.

Pour plus d’informations, consultez le [guide de création d’une connexion en continu](../tutorials/create-streaming-connection.md).

### Diffusion vers les jeux de données

Une fois que vous êtes certain que vos données sont nettoyées, vous pouvez activer vos jeux de données pour le profil client en temps réel et les [!DNL Identity Service].

Pour plus d’informations sur l’activation d’un jeu de données pour Profile et [!DNL Identity Service], veuillez lire le guide [Configurer un jeu de données](/help/profile/tutorials/dataset-configuration.md).

## Quelle est la latence attendue pour l’ingestion en flux continu sur Experience Platform ?

>[!IMPORTANT]
>
>Les mécanismes de sécurisation pour l’ingestion en flux continu sont liés au droit total d’utilisation de licence qui correspond à l’ensemble de votre organisation. En outre, l’utilisation des données dans les sandbox de développement est limitée à 10 % du total de vos profils. Pour plus d’informations sur les droits d’utilisation de licence, consultez le [guide des bonnes pratiques de gestion des données](/help/landing/license-usage-and-guardrails/data-management-best-practices.md). Pour savoir comment définir des limites au débit de diffusion en continu, lisez la [présentation de la capacité](../../landing/license-usage-and-guardrails/capacity.md).

| Destination | Latence attendue |
| --------- | ---------------- |
| Profil client en temps réel | <ul><li>&lt; 15 minutes au 95e centile pour l’ingestion de données B2C.</li><li>&lt; 30 minutes au 95e centile pour l’ingestion de données B2B.</li></ul> |
| Lac de données | &lt; 60 minutes |

## Conseils sur les demandes par seconde (RPS) pour l’ingestion en flux continu

Le tableau ci-dessous donne des conseils sur les limites de requête par seconde pour l’ingestion en flux continu.

| Limite RPS | Remarques |
| --- | --- |
| 1 000 requêtes par seconde | Ils peuvent contenir plusieurs messages lors de l’utilisation du point d’entrée `/collection/batch`. |
| 10000 messages individuels par seconde | Les messages peuvent être regroupés en moins de requêtes réelles lors de l’utilisation du point d’entrée `/collection/`. |

>[!IMPORTANT]
>
>La limite appliquée devient de **60 requêtes par minute** lors de l’utilisation de la validation synchrone à des fins de débogage.

## Extension Adobe Experience Platform

Vous pouvez utiliser l’extension Adobe Experience Platform pour créer une connexion en continu. L’extension [!DNL Experience Platform] fournit des actions permettant d’envoyer des balises formatées en [!DNL Experience Data Model] (XDM) pour l’ingestion en temps réel vers [!DNL Experience Platform]. Pour plus d’informations, consultez la documentation de [l’extension Experience Platform](/help/tags/extensions/client/web-sdk/overview.md).

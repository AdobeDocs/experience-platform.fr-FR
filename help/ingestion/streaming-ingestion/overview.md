---
keywords: Experience Platform ; accueil ; rubriques populaires ; assimilation de données ; données assimilées ; diffusion en continu ; présentation ; assimilation en flux continu ; latence ; latence en flux continu ;
solution: Experience Platform
title: Présentation de la gestion en flux continu
topic-legacy: overview
description: L’assimilation en flux continu pour Adobe Experience Platform permet aux utilisateurs d’envoyer en temps réel des données en provenance de périphériques client et serveur à l’Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 21%

---

# Présentation de l’ingestion par flux

L’assimilation en flux continu pour Adobe Experience Platform permet aux utilisateurs d’envoyer en temps réel des données depuis des périphériques client et serveur à [!DNL Experience Platform].

## Que pouvez-vous faire avec l’ingestion par flux ?

Adobe Experience Platform vous permet de générer des expériences coordonnées, cohérentes et pertinentes en générant une [!DNL Real-time Customer Profile] pour chacun de vos clients. La diffusion en continu de l&#39;assimilation joue un rôle clé dans la création de ces profils en vous permettant de fournir des données [!DNL Profile] dans [!DNL Data Lake] avec le moins de latence possible.

La vidéo suivante est conçue pour vous aider à comprendre l’assimilation en flux continu et présente les concepts ci-dessus.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Enregistrements de profil de diffusion en continu et [!DNL ExperienceEvents]

Avec l’assimilation en flux continu, les utilisateurs peuvent diffuser les enregistrements de profil et [!DNL ExperienceEvents] en [!DNL Platform] en secondes afin de faciliter la personnalisation en temps réel. Toutes les données envoyées aux API d’assimilation en flux continu sont automatiquement conservées dans [!DNL Data Lake].

Pour plus d’informations, consultez le [guide de création d’une connexion en continu](../tutorials/create-streaming-connection.md).

### Diffusion vers les jeux de données

Une fois que vous êtes certain que vos données sont propres, vous pouvez activer vos jeux de données pour [!DNL Real-time Customer Profile] et [!DNL Identity Service].

Pour plus d&#39;informations sur l&#39;activation d&#39;un jeu de données pour [!DNL Profile] et [!DNL Identity Service], consultez le [guide de configuration d&#39;un jeu de données](../../profile/tutorials/dataset-configuration.md).

## Quelle est la latence attendue pour l&#39;assimilation en flux continu sur [!DNL Platform] ?

| Destination | Latence attendue |
| --------- | ---------------- |
| Real-time Customer Profile | &lt; 1 minute |
| Lac de données | &lt; 60 minutes |

## Extension Adobe Experience Platform

Vous pouvez utiliser l’extension Adobe Experience Platform pour créer une connexion en continu. L&#39;extension [!DNL Experience Platform] fournit des actions permettant d&#39;envoyer des balises formatées dans [!DNL Experience Data Model] (XDM) pour l&#39;assimilation en temps réel à [!DNL Experience Platform]. Pour plus d’informations, consultez la documentation de [l’extension Experience Platform](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html).

---
title: Paramètres des notifications push
description: Configurez les paramètres de notification push pour l’extension de balise Web SDK.
exl-id: 96ab7ea8-7180-46bb-9c15-eecba2009c52
TQID: https://experienceleague.adobe.com/VgGzBccAStme5jPkQ-szKaebhisbDHrn6ds850CLQMk
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 180
ht-degree: 11%

---

# Paramètres des notifications push {#push-notifications}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_pushnotifications"
>title="Notifications push"
>abstract="Définit une clé publique VAPID pour l’authentification par notification push."

Cette section de configuration vous permet de définir une clé publique VALIDE pour l’authentification par notification push.

>[!NOTE]
>
>Cette fonctionnalité doit d’abord être activée à l’aide de [Composants de version personnalisés](custom-build-components.md) ; elle est désactivée par défaut.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK].
1. Développez **[!UICONTROL Custom build components]**, puis activez **[!UICONTROL Push notifications]**.
1. Sous [!UICONTROL SDK instances], faites défiler vers le bas pour localiser la section [!UICONTROL Push Notifications].
1. Saisissez votre clé publique VALIDE dans le champ **[!UICONTROL VAPID Public Key]** .

![Image montrant les paramètres de notifications push à l’aide de l’extension de balise Web SDK](../assets/push-notifications.png)

Les champs disponibles sont les suivants :

## [!UICONTROL VAPID public key]

Clé publique VALIDE utilisée pour les abonnements aux notifications push. Il s’agit d’une chaîne codée en Base64.

## [!UICONTROL Application ID]

ID de l’application associé à la clé publique valide.

## [!UICONTROL Tracking dataset ID]

Identifiant du jeu de données pour le suivi et l’analyse des notifications push.

## Notifications push à l’aide de la bibliothèque JavaScript

Cette section est l’équivalent de la balise [`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md) lors de la configuration de la bibliothèque JavaScript. La page liée fournit également des informations sur les conditions préalables et la génération d’une clé publique VALIDE.

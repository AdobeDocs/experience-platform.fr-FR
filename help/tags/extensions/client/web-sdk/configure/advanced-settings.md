---
title: Paramètres de configuration avancés
description: Configurez les paramètres avancés de l’extension de balise Web SDK.
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---

# Paramètres de configuration avancés {#advanced}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advanced"
>title="Paramètres avancés"
>abstract="Paramètres de configuration avancés. Adobe recommande de conserver ces options en l’état pour la plupart des implémentations."

Cette section de configuration vous permet de modifier les paramètres avancés. Adobe recommande de conserver ces options en l’état pour la plupart des implémentations.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Advanced Settings]** .

![Image montrant les paramètres avancés à l’aide de la page d’extension de balise Web SDK](../assets/advanced-settings.png)

Actuellement, une option est disponible.

## [!UICONTROL Edge base path]

Utilisez ce champ pour modifier le chemin d’accès de base utilisé pour interagir avec Edge Network. Adobe peut vous demander de modifier ce champ si vous participez à certains tests alpha ou bêta ; dans le cas contraire, Adobe recommande de le laisser à la valeur par défaut de `ee`.

Ce champ est l’équivalent de la balise [`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md) lors de la configuration de la bibliothèque JavaScript.

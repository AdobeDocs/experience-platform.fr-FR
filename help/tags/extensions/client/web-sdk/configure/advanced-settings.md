---
title: Paramètres de configuration avancés
description: Configurez les paramètres avancés de l’extension de balise Web SDK.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---

# Paramètres de configuration avancés

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

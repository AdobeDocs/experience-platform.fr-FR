---
title: Obtention du suivi Media Analytics
description: Exporte l’API Media héritée vers un objet de fenêtre.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# Obtention du suivi Media Analytics

L’action **[!UICONTROL Get Media Analytics tracker]** est utilisée pour obtenir l’API Media Analytics héritée. Lors de la configuration de l’action et qu’un nom d’objet est fourni, l’API Media Analytics héritée est exportée vers cet objet de fenêtre. Cette action est utile pour passer de l’ancienne version de Media Analytics à Streaming Media Analytics.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant du [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Action type] sur **[!UICONTROL Get Media Analytics tracker]**.

![Image de l’interface utilisateur d’Experience Platform montrant le type d’action Get Media Analytics Tracker.](../assets/get-media-analytics-tracker.png)

Cette action contient un seul champ que vous pouvez configurer :

* **[!UICONTROL Export the Media Legacy API to this window object]** : sélectionne l’objet vers lequel exporter l’API héritée du média. Si aucun n’est fourni, l’action exporte l’API vers `window.Media`.

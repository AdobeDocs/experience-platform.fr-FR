---
title: Paramètres de configuration d’Adobe Advertising
description: Activez ou désactivez la fonctionnalité Demand-side Platform.
source-git-commit: 526cb473a6288f367db9cb00c0277cce7543cd57
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---

# Paramètres de configuration d’Adobe Advertising

>[!AVAILABILITY]
>
>Adobe Advertising pour le SDK Web est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

La section **[!UICONTROL Adobe Advertising]** vous permet d’activer ou de désactiver la fonctionnalité Demand-side Platform (DSP) si elle est utilisée dans votre mise en œuvre. Vous ne devez définir ce champ que si votre implémentation utilise un DSP.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Adobe Advertising]** .

Actuellement, une option est disponible.

## [!UICONTROL Adobe Advertising DSP]

Un menu déroulant qui active ou désactive la fonctionnalité DSP pour Adobe Advertising.

* **[!UICONTROL Enabled]** : permet le suivi des vues publicitaires.
* **[!UICONTROL Disabled]** : désactive le suivi des vues publicitaires.

Lorsqu’ils sont activés, les paramètres suivants sont disponibles :

* **[!UICONTROL Advertisers]** : annonceurs pour lesquels activer le suivi des affichages publicitaires.
* **[!UICONTROL ID5 partner ID]** : facultatif. Identifiant partenaire ID5 de votre organisation. Ce paramètre permet au SDK Web de collecter les ID5 universels.
* **[!UICONTROL RampID JavaScript path]** : facultatif. Chemin d’accès au code JavaScript [!DNL LiveRamp RampID] de votre organisation (`ats.js`).  Ce paramètre permet au SDK Web de collecter les identifiants universels [!DNL RampID].

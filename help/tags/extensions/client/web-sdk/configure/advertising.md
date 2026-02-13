---
title: Paramètres de configuration d’Adobe Advertising
description: Activez ou désactivez la fonctionnalité Demand-side Platform.
exl-id: 594fd75d-bb13-4146-9105-1398e24c4c16
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 7%

---

# Paramètres de configuration d’Adobe Advertising {#advertising}

>[!AVAILABILITY]
>
>Adobe Advertising pour le SDK Web est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advertising"
>title="Adobe Advertising"
>abstract="Configurez les paramètres des intégrations Adobe Advertising. Notez qu’aucune configuration publicitaire n’est nécessaire pour activer la mesure des clics publicitaires. Aucune autre action n’est requise de la part des clients Search, Social et Commerce. Toutefois, les utilisateurs de Demand-side Platform (DSP) doivent configurer les annonceurs dans cette section pour mesurer les conversions d’affichage publicitaire."

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

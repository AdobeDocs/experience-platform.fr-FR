---
title: Paramètres de configuration du consentement
description: Configurez les paramètres de consentement et de confidentialité par défaut pour l’extension de balise.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---

# Paramètres de configuration du consentement

La section **[!UICONTROL Consent]** vous permet de sélectionner le niveau de consentement par défaut supposé si aucune autre préférence de consentement explicite n’est fournie. Le niveau de consentement par défaut n’est pas enregistré dans les profils utilisateur.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Consent]** .

![Image montrant les paramètres de confidentialité de l’extension de balise Web SDK dans l’interface utilisateur des balises](../assets/web-sdk-ext-privacy.png)

Cette section contient un seul ensemble de boutons radio qui déterminent le niveau de consentement par défaut :

* **[!UICONTROL In]** : collectez les événements qui se produisent avant que l’utilisateur ne fournisse des préférences de consentement.
* **[!UICONTROL Out]** : ignorez les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement.
* **[!UICONTROL Pending]** : événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse des préférences de consentement. Lorsque le consentement est accordé, les événements placés en file d’attente sont envoyés à Adobe. Lorsque le consentement est refusé, les événements placés en file d’attente sont ignorés.
* **[!UICONTROL Provide a data element]** : sélectionnez un élément de données qui détermine l’un des paramètres de configuration ci-dessus. Les valeurs valides comprennent les chaînes `"in"`, `"out"` ou `"pending"`.

Si votre organisation nécessite le consentement explicite de l’utilisateur pour collecter des données, Adobe recommande de définir le consentement par défaut sur **[!UICONTROL Out]** ou **[!UICONTROL Pending]**.

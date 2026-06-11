---
title: Paramètres de configuration du consentement
description: Configurez les paramètres de consentement et de confidentialité par défaut pour l’extension de balise.
exl-id: 93913a8b-0351-409d-b26a-8dc2ac0296c5
TQID: https://experienceleague.adobe.com/gm1sMHM7OVMTHr4dpM2CSBwZWY-26gUPylEfj25MDgI
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 11%

---

# Paramètres de configuration du consentement {#consent}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_consent"
>title="Consentement"
>abstract="Sélectionne le niveau de consentement par défaut supposé si aucune autre préférence de consentement explicite n’est fournie."

La section **[!UICONTROL Consentement]** vous permet de sélectionner le niveau de consentement par défaut supposé si aucune autre préférence de consentement explicite n’est fournie. Le niveau de consentement par défaut n’est pas enregistré dans les profils utilisateur.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Consentement]**.

![Image montrant les paramètres de confidentialité de l’extension de balise Web SDK dans l’interface utilisateur des balises](../assets/web-sdk-ext-privacy.png)

Cette section contient un seul ensemble de boutons radio qui déterminent le niveau de consentement par défaut :

* **[!UICONTROL In]** : collectez les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement.
* **[!UICONTROL Sortie]** : ignorez les événements qui se produisent avant que l’utilisateur ne fournisse des préférences de consentement.
* **[!UICONTROL En attente]** : événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. Lorsque le consentement est accordé, les événements placés en file d’attente sont envoyés à Adobe. Lorsque le consentement est refusé, les événements placés en file d’attente sont ignorés.
* **[!UICONTROL Fournir un élément de données]** : sélectionnez un élément de données qui détermine l’un des paramètres de configuration ci-dessus. Les valeurs valides comprennent les chaînes `"in"`, `"out"` ou `"pending"`.

Si votre organisation nécessite le consentement explicite de l’utilisateur pour collecter des données, Adobe recommande de définir le consentement par défaut sur **[!UICONTROL Expiré]** ou **[!UICONTROL En attente]**.

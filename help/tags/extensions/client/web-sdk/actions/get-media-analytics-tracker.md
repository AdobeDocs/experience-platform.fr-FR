---
title: Obtention du suivi Media Analytics
description: Exporte l’API Media héritée vers un objet de fenêtre.
exl-id: 45124032-efbf-4b38-8c96-59abc30af5bc
TQID: https://experienceleague.adobe.com/FFNRnk9K4IQhadiOIEtlMyZ4Twye3dXnPkyRbU56rH4
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 151
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

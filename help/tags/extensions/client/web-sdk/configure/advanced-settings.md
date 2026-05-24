---
title: Paramètres de configuration avancés
description: Configurez les paramètres avancés de l’extension de balise Web SDK.
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
TQID: https://experienceleague.adobe.com/NUVxcZpYp-e8ByeQjtJ2K-wJEJmiSigFtAMYXqXzZwQ
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 153
ht-degree: 22%

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

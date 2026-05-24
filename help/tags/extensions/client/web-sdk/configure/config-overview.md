---
title: Présentation des paramètres de configuration
description: Découvrez les options disponibles lors de la configuration de l’extension de balise Web SDK.
exl-id: 03f7bc0a-05c9-48ae-ae57-478db6d18f52
TQID: https://experienceleague.adobe.com/q8L7EqiSw47gxvuVoOE1MnZ1p2m1kIj6AIXOAK0c6Wk
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 2%

---

# Présentation des paramètres de configuration {#config-overview}

L’extension de balise Adobe Experience Platform Web SDK propose plusieurs options que vous pouvez personnaliser. Ces paramètres de configuration sont l’équivalent de balise de l’utilisation de la commande [`configure`](/help/collection/js/commands/configure/overview.md) dans la bibliothèque JavaScript.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .

## Composants de build personnalisés

Si l’optimisation de la taille de la version est une priorité pour votre organisation, vous pouvez désactiver certaines fonctionnalités que vous n’utilisez pas pour réduire la taille de la version de l’extension. Voir [Composants de version personnalisés](custom-build-components.md) pour plus d’informations.

## Instances du SDK

La plupart des implémentations nécessitent généralement une seule instance SDK. Cependant, si votre organisation nécessite plusieurs instances de tracking Web SDK, vous pouvez utiliser le bouton **[!UICONTROL Add instance]** . Les sections principales suivantes sont disponibles lors de la configuration de chaque instance de balise Web SDK :

* [**[!UICONTROL SDK instance]**](general.md) : paramètres généraux de l’instance. Tous les champs de cette section sont obligatoires.
* [**[!UICONTROL Datastreams]**](datastreams.md) : emplacement des données pour chaque environnement de balises.
* [**[!UICONTROL Consent]**](consent.md) : paramètres de consentement par défaut pour l’extension.
* [**[!UICONTROL Identity]**](identity.md) : paramètres de migration des cookies et des visiteurs.
* [**[!UICONTROL Personalization]**](personalization.md) : personnalisation de l’expérience du visiteur au niveau individuel.
* [**[!UICONTROL Data collection]**](data-collection.md) : incluez ou omettez les données collectées automatiquement.
* [**[!UICONTROL Streaming media]**](streaming-media.md) : paramètres spécifiques à la collecte de médias en flux continu.
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md) : modifiez les paramètres de configuration lorsque certaines conditions sont remplies.
* [**[!UICONTROL Advanced settings]**](advanced-settings.md) : spécifiez le chemin d’accès de base d’Edge Network.

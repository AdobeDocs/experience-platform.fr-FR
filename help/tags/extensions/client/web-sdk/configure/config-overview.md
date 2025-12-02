---
title: Présentation des paramètres de configuration
description: Découvrez les options disponibles lors de la configuration de l’extension de balise Web SDK.
source-git-commit: 5f0203cfff3cb5c8b892142ff9b1c121925c3c46
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---

# Présentation des paramètres de configuration

L’extension de balise Adobe Experience Platform Web SDK propose plusieurs options que vous pouvez personnaliser. Ces paramètres de configuration sont l’équivalent de balise de l’utilisation de la commande [`configure`](/help/collection/js/commands/configure/overview.md) dans la bibliothèque JavaScript.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .

## Composants de build personnalisés

Si l’optimisation de la taille de la version est une priorité pour votre organisation, vous pouvez désactiver certaines fonctionnalités que vous n’utilisez pas pour réduire la taille de la version de l’extension. Voir [Composants de version personnalisés](custom-build-components.md) pour plus d’informations.

## Instances de SDK

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

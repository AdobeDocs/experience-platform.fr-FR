---
title: Présentation des paramètres de configuration
description: Découvrez les options disponibles lors de la configuration de l’extension de balise Web SDK.
exl-id: 03f7bc0a-05c9-48ae-ae57-478db6d18f52
TQID: https://experienceleague.adobe.com/q8L7EqiSw47gxvuVoOE1MnZ1p2m1kIj6AIXOAK0c6Wk
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: ca3d6bf4-a4af-4944-936b-8de1eb09f149
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 713224af62da12436df4225233f2db7cac7d00fa
workflow-type: tm+mt
source-wordcount: 308
ht-degree: 1%

---

# Présentation des paramètres de configuration {#config-overview}

L’extension de balise Adobe Experience Platform Web SDK propose plusieurs options que vous pouvez personnaliser. Ces paramètres de configuration sont l’équivalent de balise de l’utilisation de la commande [`configure`](/help/collection/js/commands/configure/overview.md) dans la bibliothèque JavaScript.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].

La page de configuration est organisée en trois accordéons : [!UICONTROL Options de création], [!UICONTROL Instances de SDK] et [!UICONTROL Actions de propriété].

## Options de build

L’accordéon **[!UICONTROL Options de création]** contient les paramètres de gestion de bibliothèque et l’option permettant de désactiver des composants de création Web SDK spécifiques. La désactivation des composants inutilisés réduit la taille de la version de l’extension et peut améliorer les performances. Voir [Options de création](custom-build-components.md) pour plus d’informations.

## Instances du SDK

La plupart des implémentations nécessitent généralement une seule instance SDK. Cependant, si votre organisation nécessite plusieurs instances de tracking Web SDK, vous pouvez utiliser le bouton **[!UICONTROL Ajouter une instance]**. Les sections principales suivantes sont disponibles lors de la configuration de chaque instance de balise Web SDK :

* [**[!UICONTROL Instance SDK &#x200B;]**](general.md) : paramètres généraux de l&#39;instance. Tous les champs de cette section sont obligatoires.
* [**[!UICONTROL Flux de données]**](datastreams.md) : emplacement des données pour chaque environnement de balises.
* [**[!UICONTROL Consentement]**](consent.md) : paramètres de consentement par défaut pour l’extension.
* [**[!UICONTROL Identité]**](identity.md) : paramètres de migration des cookies et des visiteurs.
* [**&#128279;**](personalization.md) : personnalisez l&#39;expérience du visiteur au niveau individuel.
* [**[!UICONTROL Collecte de données]**](data-collection.md) : incluez ou omettez les données collectées automatiquement.
* [**[!UICONTROL Streaming media]**](streaming-media.md) : paramètres spécifiques à la collecte de médias en flux continu.
* [**[!UICONTROL Remplacements de la configuration des trains de données]**](configuration-overrides.md) : modifiez les paramètres de configuration lorsque certaines conditions sont remplies.
* [**[!UICONTROL Paramètres avancés]**](advanced-settings.md) : spécifiez le chemin de base de l’Edge Network.

## Actions de propriété

L’accordéon **[!UICONTROL Actions de propriété]** contient des utilitaires de maintenance à l’échelle de la propriété qui s’appliquent à la propriété de balise dans son ensemble plutôt qu’à des instances SDK individuelles.

* [**[!UICONTROL Réparer les références d’élément de données]**](repair-data-element-references.md) : analysez toutes les actions d’extension Web SDK dans la propriété et remplacez les références d’élément de données obsolètes si possible.

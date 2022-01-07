---
keywords: activer les destinations ; activer les données
title: Présentation de l’Activation
type: Tutorial
seo-title: Activation overview
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform vers différents types de destinations.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform to various types of destinations.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: f4ae6831569e8a5b458c42f76810212174f04811
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 9%

---

# Présentation de l’Activation

Adobe Experience Platform prend en charge un large éventail de destinations. Le workflow d’activation de l’audience varie selon les destinations, selon le type de données d’audience pris en charge et la fréquence d’exportation des données.

## Méthodes d’activation {#activation-methods}

Après vous [configuration de votre destination](connect-destination.md), vous pouvez activer les segments d’audience de plusieurs façons :

### Activation des audiences à partir du catalogue des destinations

Pour plus d’informations sur l’activation des audiences vers votre destination à partir du catalogue des destinations, consultez les guides suivants :

* [Activation des données d’audience vers des destinations d’exportation de segments de diffusion](activate-segment-streaming-destinations.md)
* [Activation des données d’audience vers des destinations d’exportation de profils en continu](activate-streaming-profile-destinations.md)
* [Activation des données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)

### Activation des audiences à partir de la fonction [!UICONTROL Parcourir] page

Suivez les étapes ci-dessous pour activer les données vers vos destinations à partir du **[!UICONTROL Parcourir]** page.

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez la variable **[!UICONTROL Parcourir]** .

   ![Onglet Parcourir](../assets/ui/activation-overview/browse-tab.png)

1. Recherchez la connexion de destination que vous souhaitez utiliser pour activer vos segments, sélectionnez les trois points dans le [!UICONTROL Nom] , puis sélectionnez **[!UICONTROL Activation des segments]**.

   ![Bouton Activer les segments](../assets/ui/activation-overview/activate-segments.png)

1. Selon la destination sélectionnée, suivez les étapes décrites dans les articles ci-dessous, en commençant par la **[!UICONTROL Sélection de segments]** pour terminer le workflow d’activation :

   * [Activation des données d’audience vers des destinations d’exportation de segments de diffusion](activate-segment-streaming-destinations.md)
   * [Activation des données d’audience vers des destinations d’exportation de profils en continu](activate-streaming-profile-destinations.md)
   * [Activation des données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)

### Activation des audiences à partir de la page des détails du segment {#activate-segment-details}

Vous pouvez activer des segments vers des destinations à partir de la page des détails du segment. Voir [Détails du segment](../../segmentation/ui/overview.md#segment-details) pour plus d’informations.

Selon la destination sélectionnée, suivez les étapes décrites dans les articles ci-dessous pour terminer le workflow d’activation :

* [Activation des données d’audience vers des destinations d’exportation de segments de diffusion](activate-segment-streaming-destinations.md)
* [Activation des données d’audience vers des destinations d’exportation de profils en continu](activate-streaming-profile-destinations.md)
* [Activation des données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)

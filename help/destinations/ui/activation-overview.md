---
keywords: activer les destinations ; activer les données
title: Présentation de l’activation
type: Tutorial
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform vers différents types de destinations.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 24%

---

# Présentation de l’activation

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Adobe Experience Platform prend en charge un large éventail de destinations. Le workflow d’activation de l’audience varie selon les destinations, selon le type de données d’audience pris en charge et la fréquence d’exportation des données.

## Méthodes d’activation {#activation-methods}

Après vous [configuration de votre destination](connect-destination.md), vous pouvez activer les segments d’audience de plusieurs façons :

### Activation des audiences à partir du catalogue des destinations

Pour plus d’informations sur l’activation des audiences vers votre destination à partir du catalogue des destinations, consultez les guides suivants :

* [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](activate-segment-streaming-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](activate-streaming-profile-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)

### Activation des audiences à partir de la fonction [!UICONTROL Parcourir] page

Suivez les étapes ci-dessous pour activer les données vers vos destinations à partir du **[!UICONTROL Parcourir]** page.

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez la variable **[!UICONTROL Parcourir]** .

   ![Onglet Parcourir](../assets/ui/activation-overview/browse-tab.png)

1. Recherchez la connexion de destination que vous souhaitez utiliser pour activer vos segments, sélectionnez les trois points dans le [!UICONTROL Nom] , puis sélectionnez **[!UICONTROL Activation des segments]**.

   ![Bouton Activer des segments](../assets/ui/activation-overview/activate-segments.png)

1. Selon la destination sélectionnée, suivez les étapes décrites dans les articles ci-dessous, en commençant par la **[!UICONTROL Sélection de segments]** pour terminer le workflow d’activation :

   * [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](activate-segment-streaming-destinations.md)
   * [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](activate-streaming-profile-destinations.md)
   * [Activer les données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)

### Activation des audiences à partir de la page des détails du segment {#activate-segment-details}

Vous pouvez activer des segments vers des destinations à partir de la page des détails du segment. Voir [Détails du segment](../../segmentation/ui/overview.md#segment-details) pour plus d’informations.

Selon la destination sélectionnée, suivez les étapes décrites dans les articles ci-dessous pour terminer le workflow d’activation :

* [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](activate-segment-streaming-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](activate-streaming-profile-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)

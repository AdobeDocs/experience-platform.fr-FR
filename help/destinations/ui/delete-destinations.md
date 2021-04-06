---
keywords: supprimer des destinations ; comment supprimer des destinations
title: Supprimer les destinations
type: Tutoriel
description: Ce didacticiel liste les étapes de suppression d’une destination existante dans l’interface utilisateur Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: ebe2a35e66b78acf6a9ffa20664877913cd35648
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---


# Supprimer des destinations {#delete-destinations}

## Présentation {#overview}

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez supprimer des connexions existantes aux destinations.

La suppression d&#39;une destination supprime tous les flux de données existants vers cette destination. Tous les segments activés pour les destinations que vous supprimez sont démappés avant la suppression du flux de données.

Vous pouvez supprimer des destinations de [!DNL Platform] [!DNL UI] de deux manières. Vous pouvez :

* [Suppression de destinations dans l’  onglet de navigation](#delete-browse-tab)
* [Supprimer des destinations de la page des détails de destination](#delete-destination-details-page)

## Supprimer des destinations à partir de l’onglet Parcourir{#delete-browse-tab}

Suivez les étapes ci-dessous pour supprimer une destination de l&#39;onglet [!UICONTROL Parcourir].

1. Connectez-vous à l&#39;[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Pour vue de vos destinations existantes, sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône de filtre ![Icône de filtre](../assets/ui/delete-destinations/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le bouton ![Supprimer](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Supprimer]** dans la colonne **[!UICONTROL Plateforme]** pour supprimer une destination existante.
   ![Supprimer les destinations](../assets/ui/delete-destinations/delete-destinations.png)

4. Sélectionnez **[!UICONTROL Supprimer]** pour confirmer la suppression de la destination.

   ![Confirmer la destination de suppression](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## Supprimer des destinations de la page des détails de destination{#delete-destination-details-page}

Suivez les étapes ci-dessous pour supprimer une destination de la page des détails de la destination.

1. Connectez-vous à l&#39;[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Pour vue de vos destinations existantes, sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône de filtre ![Icône de filtre](../assets/ui/delete-destinations/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le nom de la destination à supprimer.

   ![Sélectionner la destination](../assets/ui/delete-destinations/delete-destination-select.png)

   * Si la destination comporte des flux de données existants, vous êtes dirigé vers l&#39;onglet [!UICONTROL Flux de données].

      ![Onglet Flux de données](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Si la destination ne comporte pas de flux de données existants, vous accédez à une page vide dans laquelle vous pouvez début l’activation d’audiences.

      ![Détails de la destination](../assets/ui/delete-destinations/destination-details-empty.png)


4. Sélectionnez **[!UICONTROL Supprimer]** dans le rail de droite.

   ![Supprimer la destination](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Sélectionnez **[!UICONTROL Supprimer]** dans la boîte de dialogue de confirmation pour supprimer la destination.

   ![Confirmation de la suppression de la destination](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Selon la charge du serveur, [!DNL Platform] peut prendre quelques minutes pour supprimer la destination.
---
keywords: supprimer des destinations, comment supprimer des destinations, supprimer des destinations
title: Supprimer les destinations
type: Tutorial
description: Ce tutoriel répertorie les étapes de suppression d’une destination existante dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 33%

---

# Supprimer les destinations {#delete-destinations}

## Présentation {#overview}

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez supprimer les connexions existantes aux destinations.

La suppression d’une destination supprime tous les flux de données existants vers cette destination. Tous les segments activés vers les destinations que vous supprimez sont démappés avant la suppression du flux de données.

Vous pouvez supprimer des destinations de la variable [!DNL Platform] [!DNL UI]. Vous pouvez :

* [Suppression de destinations du [!UICONTROL Parcourir] tab](#delete-browse-tab)
* [Suppression de destinations de la page de détails des destinations](#delete-destination-details-page)

## Suppression de destinations dans l’onglet Parcourir{#delete-browse-tab}

Suivez les étapes ci-dessous pour supprimer une destination du [!UICONTROL Parcourir] .

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Pour afficher vos destinations existantes, sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](../assets/ui/delete-destinations/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrage des destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez la ![Bouton Plus](../assets/ui/delete-destinations/more-icon.png) dans la colonne Nom , puis sélectionnez ![Bouton Supprimer](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Supprimer]** pour supprimer une connexion de destination existante.
   ![Supprimer les destinations](../assets/ui/delete-destinations/delete-destinations.png)

4. Sélectionner **[!UICONTROL Supprimer]** pour confirmer la suppression de la connexion à la destination.

   ![Confirmer la suppression de la destination](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Suppression de destinations de la page de détails des destinations{#delete-destination-details-page}

Suivez les étapes ci-dessous pour supprimer une destination de la page de détails des destinations.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Pour afficher vos destinations existantes, sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](../assets/ui/delete-destinations/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrage des destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le nom de la destination que vous souhaitez supprimer.

   ![Sélectionnez des destinations](../assets/ui/delete-destinations/delete-destination-select.png)

   * Si la destination comporte des flux de données existants, vous êtes dirigé vers la variable [!UICONTROL Exécutions de flux de données] .

      ![Onglet Exécutions de flux de données](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Si la destination ne comporte pas de flux de données existants, vous accédez à une page vide dans laquelle vous pouvez commencer à activer les audiences.

      ![Détails de la destination](../assets/ui/delete-destinations/destination-details-empty.png)

4. Sélectionner **[!UICONTROL Supprimer]** dans le rail de droite.

   ![Supprimer la destination](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Sélectionner **[!UICONTROL Supprimer]** dans la boîte de dialogue de confirmation pour supprimer la destination.

   ![Confirmation de suppression de la destination](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Selon la charge du serveur, quelques minutes peuvent être nécessaires pour [!DNL Platform] pour supprimer la destination.

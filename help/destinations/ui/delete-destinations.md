---
keywords: supprimer des destinations, comment supprimer des destinations, supprimer une destination
title: Supprimer les destinations
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour supprimer une destination existante dans l’interface utilisateur de Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 32%

---

# Supprimer les destinations {#delete-destinations}

## Vue d’ensemble {#overview}

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez supprimer des connexions existantes à des destinations.

La suppression d’une destination supprime tous les flux de données existants vers cette destination. Toutes les audiences activées pour les destinations que vous supprimez ne sont pas mappées avant la suppression du flux de données.

Vous pouvez supprimer des destinations de l’[!DNL UI] [!DNL Experience Platform] de deux façons. Vous pouvez effectuer les actions suivantes :

* [Supprimer des destinations de l’onglet [!UICONTROL  Parcourir ]](#delete-browse-tab)
* [Supprimer des destinations de la page des détails de la destination](#delete-destination-details-page)

## Supprimer des destinations de l’onglet Parcourir{#delete-browse-tab}

Pour supprimer une destination de l’onglet [!UICONTROL Parcourir], procédez comme suit.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Pour afficher vos destinations existantes, sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le bouton ![Plus](/help/images/icons/more.png) dans la colonne Nom, puis sélectionnez ![Bouton Supprimer](/help/images/icons/delete.png) **[!UICONTROL Supprimer]** pour supprimer une connexion de destination existante.
   ![Supprimer des destinations](../assets/ui/delete-destinations/delete-destinations.png)

4. Sélectionnez **[!UICONTROL Supprimer]** pour confirmer la suppression de la connexion de destination.

   ![Confirmer la suppression de la destination](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Supprimer des destinations de la page des détails de la destination{#delete-destination-details-page}

Suivez les étapes ci-dessous pour supprimer une destination de la page de détails de la destination.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Pour afficher vos destinations existantes, sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le nom de la destination à supprimer.

   ![Sélectionnez des destinations](../assets/ui/delete-destinations/delete-destination-select.png)

   * Si la destination comporte des flux de données existants, vous accédez à l’onglet [!UICONTROL Exécutions de flux de données].

     ![ Onglet Exécutions de flux de données ](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Si la destination ne comporte pas de flux de données existants, vous accédez à une page vide où vous pouvez commencer à activer les audiences.

     ![Détails de la destination](../assets/ui/delete-destinations/destination-details-empty.png)

4. Sélectionnez **[!UICONTROL Supprimer]** dans le rail de droite.

   ![Supprimer la destination](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Sélectionnez **[!UICONTROL Supprimer]** dans la boîte de dialogue de confirmation pour supprimer la destination.

   ![Confirmation de la suppression de la destination](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >En fonction de la charge du serveur, la suppression de la destination peut prendre quelques minutes pour [!DNL Experience Platform].

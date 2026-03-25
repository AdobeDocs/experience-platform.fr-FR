---
keywords: supprimer des destinations, comment supprimer des destinations, supprimer une destination
title: Supprimer les destinations
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour supprimer une destination existante dans l’interface utilisateur de Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 26%

---

# Supprimer les destinations {#delete-destinations}

## Vue d’ensemble {#overview}

Dans l’interface utilisateur [!DNL Adobe Experience Platform], vous pouvez supprimer des connexions existantes à des destinations.

La suppression d’une destination supprime tous les flux de données existants vers cette destination. Toutes les audiences activées pour les destinations que vous supprimez ne sont pas mappées avant la suppression du flux de données.

Vous pouvez supprimer des destinations de l’[!DNL Experience Platform] [!DNL UI] de deux façons. Vous pouvez :

* [Supprimer des destinations de l’onglet [!UICONTROL Browse]](#delete-browse-tab)
* [Supprimer des destinations de la page des détails de la destination](#delete-destination-details-page)

## Supprimer des destinations de l’onglet Parcourir{#delete-browse-tab}

Suivez les étapes ci-dessous pour supprimer une destination de l’onglet [!UICONTROL Browse] .

1. Accédez à l’[interface utilisateur d’](https://platform.adobe.com/) puis sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Browse]** dans l’en-tête supérieur pour afficher vos destinations existantes.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le bouton ![&#x200B; Plus &#x200B;](/help/images/icons/more.png) dans la colonne Nom , puis sélectionnez ![Bouton Supprimer](/help/images/icons/delete.png) **[!UICONTROL Delete]** pour supprimer une connexion de destination existante.
   ![Supprimer des destinations](../assets/ui/delete-destinations/delete-destinations.png)

4. Sélectionnez **[!UICONTROL Delete]** pour confirmer la suppression de la connexion de destination.

   ![Confirmer la suppression de la destination](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Supprimer des destinations de la page des détails de la destination {#delete-destination-details-page}

Suivez les étapes ci-dessous pour supprimer une destination de la page de détails de la destination.

1. Accédez à l’[interface utilisateur d’](https://platform.adobe.com/) puis sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Browse]** dans l’en-tête supérieur pour afficher vos destinations existantes.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le nom de la destination à supprimer.

   ![Sélectionnez des destinations](../assets/ui/delete-destinations/delete-destination-select.png)

   * Si la destination comporte des flux de données existants, vous êtes redirigé(e) vers l’onglet [!UICONTROL Dataflow runs] .

     ![&#x200B; Onglet Exécutions de flux de données &#x200B;](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Si la destination ne comporte pas de flux de données existants, vous accédez à une page vide où vous pouvez commencer à activer les audiences.

     ![Détails de la destination](../assets/ui/delete-destinations/destination-details-empty.png)

4. Sélectionnez **[!UICONTROL Delete]** dans le rail de droite.

   ![Supprimer la destination](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Sélectionnez **[!UICONTROL Delete]** dans la boîte de dialogue de confirmation pour supprimer la destination.

   ![Confirmation de la suppression de la destination](..//assets/ui/delete-destinations/delete-destinations-delete.png)

>[!NOTE]
>
>En fonction de la charge du serveur, la suppression de la destination peut prendre quelques minutes pour [!DNL Experience Platform].

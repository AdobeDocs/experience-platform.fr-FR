---
keywords: supprimer des destinations, comment supprimer des destinations, supprimer des destinations
title: Suppression de destinations
type: Tutorial
description: Ce tutoriel répertorie les étapes de suppression d’une destination existante dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 84deb9d1eecee8ec4369915a0b3c1eb810fd7c9b
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---

# Suppression de destinations {#delete-destinations}

## Présentation {#overview}

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez supprimer les connexions existantes aux destinations.

La suppression d’une destination supprime tous les flux de données existants vers cette destination. Tous les segments activés vers les destinations que vous supprimez sont démappés avant la suppression du flux de données.

Vous pouvez supprimer des destinations de [!DNL Platform] [!DNL UI] de deux façons. Vous pouvez :

* [Supprimer des destinations de l’onglet [!UICONTROL Parcourir]](#delete-browse-tab)
* [Suppression de destinations de la page de détails des destinations](#delete-destination-details-page)

>[!IMPORTANT]
>
>Bien que vous puissiez supprimer des *connexions existantes aux destinations*, comme décrit dans cet article, Platform ne vous permet pas actuellement de supprimer les *[comptes de destination](/help/destinations/ui/destinations-workspace.md#accounts)* existants.

## Suppression de destinations dans l’onglet Parcourir{#delete-browse-tab}

Suivez les étapes ci-dessous pour supprimer une destination de l’onglet [!UICONTROL Parcourir] .

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Pour afficher vos destinations existantes, sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône de filtre ![Icône de filtre](../assets/ui/delete-destinations/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrage des destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le bouton ![Supprimer](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Supprimer]** dans la colonne **[!UICONTROL Plateforme]** pour supprimer une destination existante.
   ![Suppression de destinations](../assets/ui/delete-destinations/delete-destinations.png)

4. Sélectionnez **[!UICONTROL Supprimer]** pour confirmer la suppression de la destination.

   ![Confirmer la suppression de la destination](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## Suppression de destinations de la page de détails des destinations{#delete-destination-details-page}

Suivez les étapes ci-dessous pour supprimer une destination de la page de détails des destinations.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Pour afficher vos destinations existantes, sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur.

   ![Parcourir les destinations](../assets/ui/delete-destinations/browse-destinations.png)

2. Sélectionnez l’icône de filtre ![Icône de filtre](../assets/ui/delete-destinations/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrage des destinations](../assets/ui/delete-destinations/filter-destinations.png)

3. Sélectionnez le nom de la destination que vous souhaitez supprimer.

   ![Sélectionner la destination](../assets/ui/delete-destinations/delete-destination-select.png)

   * Si la destination comporte des flux de données existants, vous accédez à l’onglet [!UICONTROL Flux de données s’exécute] .

      ![Onglet Exécutions de flux de données](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Si la destination ne comporte pas de flux de données existants, vous accédez à une page vide dans laquelle vous pouvez commencer à activer les audiences.

      ![Détails de la destination](../assets/ui/delete-destinations/destination-details-empty.png)


4. Sélectionnez **[!UICONTROL Supprimer]** dans le rail de droite.

   ![Supprimer la destination](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Sélectionnez **[!UICONTROL Supprimer]** dans la boîte de dialogue de confirmation pour supprimer la destination.

   ![Confirmation de suppression de la destination](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Selon la charge du serveur, la suppression de la destination peut prendre quelques minutes pour [!DNL Platform].

---
keywords: supprimer un compte de destination, des comptes de destination, comment supprimer des comptes ;
title: Supprimer les comptes de destination
type: Tutorial
description: Ce tutoriel répertorie les étapes de suppression des comptes de destination dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 18%

---

# Supprimer les comptes de destination

## Vue d’ensemble {#overview}

L’onglet **[!UICONTROL Comptes]** vous montre des détails sur les connexions que vous avez établies avec différentes destinations. Reportez-vous à la [présentation des comptes](../ui/destinations-workspace.md#accounts) pour toutes les informations que vous pouvez obtenir sur chaque compte de destination.

Ce tutoriel décrit les étapes à suivre pour supprimer les comptes de destination qui ne sont plus nécessaires à l’aide de l’interface utilisateur de l’Experience Platform.

![Onglet Comptes](../assets/ui/update-accounts/destination-accounts.png)

## Supprimer des comptes {#delete}

>[!TIP]
>
>Avant de supprimer le compte de destination, vous devez d’abord supprimer tout flux de données existant associé au compte de destination. Pour supprimer des flux de données de destination existants, reportez-vous au tutoriel sur la [suppression des flux de données de destination dans l’interface utilisateur](./delete-destinations.md).

Suivez les étapes ci-dessous pour supprimer des comptes de destination existants.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Comptes]** dans l’en-tête supérieur pour afficher vos comptes existants.

   ![Onglet Comptes](../assets/ui/delete-accounts/accounts-tab.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de comptes associés aux destinations sélectionnées.

   ![Filtrer les destinations](../assets/ui/delete-accounts/filter-accounts.png)

3. Sélectionnez les points de suspension (`...`) à côté du nom du compte que vous avez l’intention de supprimer. Un panneau contextuel s’affiche, fournissant des options pour **[!UICONTROL Activer les audiences]**, **[!UICONTROL Modifier les détails]** et **[!UICONTROL Supprimer]** du compte. Sélectionnez le bouton ![Supprimer](/help/images/icons/delete.png) **[!UICONTROL Supprimer]** pour supprimer le compte de votre choix.

   ![Supprimer le compte de destination](../assets/ui/delete-accounts/delete-accounts.png)

4. Une boîte de dialogue de confirmation finale s’affiche. Sélectionnez **[!UICONTROL Supprimer]** pour terminer le processus.

![Confirmer la suppression de compte](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez correctement utilisé l’espace de travail des destinations pour supprimer des comptes existants.

Pour savoir comment effectuer ces opérations par programmation à l’aide de l’API [!DNL Flow Service], reportez-vous au tutoriel sur la [&#x200B; suppression des connexions à l’aide de l’API Flow Service](../api/delete-destination-account.md).

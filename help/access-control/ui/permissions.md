---
keywords: Experience Platform;home;popular topics;product profile;manage permissions
solution: Experience Platform
title: Gestion des autorisations d’un profil de produit
topic: user guide
description: Le contrôle d’accès dans Adobe Experience Platform vous permet de gérer les rôles et les autorisations pour diverses fonctionnalités de Platform à l’aide d’Adobe Admin Console. Ce document sert de guide pour la gestion des autorisations pour un profil de produits pour la plate-forme.
translation-type: tm+mt
source-git-commit: 8d234eaecbecef45ea4d4cbc6b65a7d7dcc18f2e
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 68%

---


# Gestion des autorisations d’un profil de produit

Immédiatement après la [création d’un nouveau profil de produit](#create-a-new-product-profile), vous êtes invité à configurer les autorisations du profil. Si vous modifiez les autorisations d’un profil existant, sélectionnez le profil depuis l’onglet **[!UICONTROL Profil de produit]** pour ouvrir la page des détails du profil, puis cliquez sur **[!UICONTROL Autorisations]**.

![autorisations de profil](../images/profile-permissions.png)

Les autorisations sont divisées en catégories et répertoriées sur cette page. La liste affiche le nom de la catégorie, le nombre d’autorisations qu’elle contient (et le nombre d’autorisations actives) ainsi que sa description.

Select any category on the list to open the **[!UICONTROL Edit Permissions]** page.

![modification des autorisations](../images/edit-permissions.png)

La page **[!UICONTROL Modifier les autorisations]** fournit un espace de travail servant à ajouter et à supprimer des autorisations pour le profil de produit sélectionné. Le côté gauche de l’écran affiche une liste de catégories d’autorisation. Selecting a category changes the permissions that are displayed under **[!UICONTROL Available Permissions Items]**.

![changement de catégorie d’autorisations](../images/change-permissions-category.png)

To add a permission, select the **plus (+)** icon next to the permission&#39;s name. Alternatively, you can select **[!UICONTROL Add all]** to add all permissions under the current category to the profile. Les autorisations ajoutées s’affichent sous **[!UICONTROL Éléments d’autorisation inclus]**.

![ajout d’autorisations](../images/add-permissions.png)

>[!NOTE]
>
>La liste des **[!UICONTROL Éléments d’autorisations inclus]** n’affiche que les autorisations ajoutées à partir de la catégorie actuellement sélectionnée.

To remove a permission, select the **X** icon next to the permission&#39;s name, or select **[!UICONTROL Remove all]** to remove all permissions under the current category. Les autorisations supprimées réapparaissent sous **[!UICONTROL Éléments d’autorisation disponibles]**.

Continuez à parcourir les catégories disponibles et ajoutez toutes les autorisations souhaitées. When finished, select **[!UICONTROL Save]**.

![ajout d’autorisations terminé](../images/permissions-finish.png)

L’onglet **[!UICONTROL Autorisations]** du profil de produit réapparaît et indique que les autorisations sélectionnées sont désormais actives.

![autorisations ajoutées](../images/added-permissions.png)

## Étapes suivantes

Une fois les autorisations établies, vous pouvez passer à l’étape suivante pour [gérer les détails et les services pour un profil de produit](details-and-services.md)
---
keywords: supprimer le compte de destination, comptes de destination, comment supprimer des comptes
title: Supprimer les comptes de destination
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour supprimer des comptes de destination dans l’interface utilisateur de Adobe Experience Platform
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
TQID: https://experienceleague.adobe.com/3dwqYSVa-P46Yu401egYBUwx9Ims1ODNzV9a1gAs1hY
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 298
ht-degree: 14%

---

# Supprimer les comptes de destination

## Vue d’ensemble {#overview}

L’onglet **[!UICONTROL Comptes]** affiche des détails sur les connexions que vous avez établies avec diverses destinations. Consultez la [ Présentation des comptes ](../ui/destinations-workspace.md#accounts) pour obtenir toutes les informations disponibles pour chaque compte de destination.

Ce tutoriel décrit les étapes à suivre pour supprimer des comptes de destination qui ne sont plus nécessaires à l’aide de l’interface utilisateur d’Experience Platform.

![Onglet Comptes](../assets/ui/update-accounts/destination-accounts.png)

## Supprimer des comptes {#delete}

>[!TIP]
>
>Avant de supprimer le compte de destination, vous devez d’abord supprimer les flux de données existants associés au compte de destination. Pour supprimer des flux de données de destination existants, reportez-vous au tutoriel sur la [suppression de flux de données de destination dans l’interface utilisateur](./delete-destinations.md).

Pour supprimer des comptes de destination existants, procédez comme suit.

1. Accédez à l’[interface utilisateur d’](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Comptes]** dans l’en-tête supérieur pour afficher vos comptes existants.

   ![Onglet Comptes](../assets/ui/delete-accounts/accounts-tab.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de comptes associés aux destinations sélectionnées.

   ![Filtrer les destinations](../assets/ui/delete-accounts/filter-accounts.png)

3. Sélectionnez les points de suspension (`...`) à côté du nom du compte que vous souhaitez supprimer. Un panneau pop-up s’affiche, fournissant des options pour **[!UICONTROL Activer les audiences]**, **[!UICONTROL Modifier les détails]** et **[!UICONTROL Supprimer]** le compte. Sélectionnez le bouton ![Supprimer](/help/images/icons/delete.png) **[!UICONTROL Supprimer]** pour supprimer le compte souhaité.

   ![Supprimer le compte de destination](../assets/ui/delete-accounts/delete-accounts.png)

4. Une boîte de dialogue de confirmation finale s’affiche. Sélectionnez **[!UICONTROL Supprimer]** pour terminer le processus.

![Confirmer la suppression du compte](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Étapes suivantes {#next-steps}

Vous avez correctement utilisé l’espace de travail des destinations pour supprimer des comptes existants.

Pour savoir comment effectuer ces opérations par programmation à l’aide de l’API [!DNL Flow Service], reportez-vous au tutoriel sur la [suppression de connexions à l’aide de l’API Flow Service](../api/delete-destination-account.md)

---
keywords: Experience Platform;home;popular topics;sandbox user guide;sandbox guide
solution: Experience Platform
title: Guide d’utilisation des environnements de test
topic: user guide
description: Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux environnements de test dans l’interface utilisateur d’Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 2d1a9699866bd39de7251731e9f0cd2f753a5083
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 50%

---


# Guide d’utilisation des environnements de test

Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux environnements de test dans l’interface utilisateur d’Adobe Experience Platform.

## Affichage des environnements de test

In the Experience Platform UI, select **[!UICONTROL Sandboxes]** in the left-navigation to open the **[!UICONTROL Sandboxes]** dashboard. Le tableau de bord répertorie tous les environnements de test disponibles pour votre organisation, y compris le type d’environnement de test (production ou développement) et l’état (actif, en cours de création, supprimé ou en échec).

![](../images/ui/view-sandboxes.png)

## Basculer entre des environnements de test

La commande **sélecteur d’environnements de test** située en haut à gauche de l’écran affiche l’environnement de test actuellement actif.

![](../images/ui/sandbox-switcher.png)

Pour passer d’un sandbox à l’autre, sélectionnez le sandbox et sélectionnez le sandbox de votre choix dans la liste déroulante.

![](../images/ui/switcher-menu.png)

Après avoir sélectionné un environnement de test, l’écran actualise l’environnement de test sélectionné depuis le sélecteur d’environnements de test.

![](../images/ui/switched.png)

## Recherche d’un sandbox

Vous pouvez naviguer dans la liste des sandbox à votre disposition en utilisant la fonction de recherche du menu sandbox. Tapez le nom du sandbox auquel vous souhaitez accéder pour filtrer tous les sandbox disponibles pour votre entreprise.

![](../images/ui/sandbox-search.png)

## Création d’un nouvel environnement de test

La vidéo suivante présente un aperçu rapide de l’utilisation des sandbox dans l’Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Pour créer un sandbox dans l’interface utilisateur, sélectionnez le bouton **[!UICONTROL Créer un sandbox]** dans la partie supérieure droite de l’écran.

![](../images/ui/create-sandbox.png)

La boîte de dialogue **[!UICONTROL Créer un environnement de test]** s’affiche et vous invite à fournir un titre et un nom d’affichage à votre environnement de test. Le **titre d’affichage** est prévu pour être lu par un utilisateur et doit être suffisamment descriptif pour permettre son identification rapide. The sandbox **[!UICONTROL Name]** is an all-lowercase identifier for use in API calls, and should therefore be unique and concise. Le **[!UICONTROL nom]** du sandbox ne doit contenir que des caractères alphanumériques et des tirets **(-)**, il doit commencer par une lettre et comporter au maximum 256 caractères.

When finished, select **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Étant donné que vous êtes limité à la création d’environnement de test de type hors production, l’option **[!UICONTROL type]** est verrouillée sur « hors production » et ne peut pas être modifiée.

Once you have finished creating the sandbox, refresh the page and the new sandbox appears in the **[!UICONTROL Sandboxes]** dashboard with a status of &quot;[!UICONTROL Creating]&quot;. New sandboxes take approximately 15 minutes to be provisioned by the system, after which their status changes to &quot;[!UICONTROL Active]&quot;.

![](../images/ui/creating.png)

## Réinitialisation d’un environnement de test

>[!NOTE]
>
>Cette fonctionnalité est disponible uniquement pour les environnements de test hors production. Il n’est pas possible de réinitialiser les environnements de test de production.

La réinitialisation d’un environnement de test hors production supprime toutes les ressources associées à cet environnement de test (schémas, jeux de données, etc.) tout en conservant le nom et les autorisations associés de l’environnement de test. Cet environnement de test « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

To reset a sandbox in the UI, select **[!UICONTROL Sandboxes]** in the left-nav, then select the sandbox you want to reset. In the dialog that appears on the right-hand side of the screen, select **[!UICONTROL Reset Sandbox]**.

![](../images/ui/reset-sandbox.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Select **[!UICONTROL Reset]** to continue.

![](../images/ui/reset-confirm.png)

A confirmation message appears and the sandbox&#39;s state changes to &quot;**[!UICONTROL Resetting]&quot;**. Once it has been provisioned by the system, its state will update to **&quot;[!UICONTROL Active]&quot;** or **&quot;[!UICONTROL Failed]&quot;**.

![](../images/ui/resetting.png)

## Suppression d’un environnement de test

>[!NOTE]
>
>Cette fonctionnalité est disponible uniquement pour les environnements de test hors production. Il n’est pas possible de supprimer les environnements de test de production.

La suppression d’un environnement de test hors production supprime définitivement toutes les ressources associées à cet environnement de test, y compris les autorisations.

To delete a sandbox in the UI, select **[!UICONTROL Sandboxes]** in the left-nav, then select the sandbox you want to delete. In the dialog that appears on the right-hand side of the screen, select **[!UICONTROL Delete Sandbox]**.

![](../images/ui/delete-sandbox.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Select **[!UICONTROL Delete]** to continue.

![](../images/ui/delete-confirm.png)

Un message de confirmation s’affiche et l’environnement de test est supprimé de l’espace de travail **[!UICONTROL Environnements de test]**.

## Étapes suivantes

Ce document vous a montré comment gérer les environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur la gestion des environnements de test à l’aide de l’API Sandbox, consultez le [guide de développement des environnements de test](../api/getting-started.md).
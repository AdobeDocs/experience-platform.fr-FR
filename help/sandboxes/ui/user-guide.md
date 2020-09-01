---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide d’utilisation des environnements de test
topic: user guide
translation-type: tm+mt
source-git-commit: 397f08efa276f7885e099a0a8d9dc6d23fe0e8cc
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 80%

---


# Guide d’utilisation des environnements de test

Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux environnements de test dans l’interface utilisateur d’Adobe Experience Platform.

## Affichage des environnements de test

Dans l’interface utilisateur d’Experience Platform, cliquez sur **[!UICONTROL Environnements de test]** dans le panneau de navigation de gauche pour ouvrir le tableau de bord **[!UICONTROL Environnements de test]**. Le tableau de bord répertorie tous les environnements de test disponibles pour votre organisation, y compris le type d’environnement de test (production ou développement) et l’état (actif, en cours de création, supprimé ou en échec).

![](../images/ui/sandboxes-tab.png)

## Basculer entre des environnements de test

La commande **sélecteur d’environnements de test** située en haut à gauche de l’écran affiche l’environnement de test actuellement actif.

![](../images/ui/sandbox-selector.png)

Pour passer d’un environnement de test à l’autre, cliquez sur le sélecteur d’environnements de test et sélectionnez l’environnement de test souhaité depuis la liste déroulante.

![](../images/ui/switch-sandbox.png)

Après avoir sélectionné un environnement de test, l’écran actualise l’environnement de test sélectionné depuis le sélecteur d’environnements de test.

![](../images/ui/sandbox-switched.png)

## Création d’un nouvel environnement de test

La vidéo suivante présente un aperçu rapide de l’utilisation des sandbox dans l’Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Pour créer un nouvel environnement de test dans l’interface utilisateur, cliquez sur **[!UICONTROL Environnements de test]** dans le volet de navigation de gauche, puis cliquez sur **[!UICONTROL Créer un environnement de test]**.

![](../images/ui/create-sandbox-button.png)

La boîte de dialogue **[!UICONTROL Créer un environnement de test]** s’affiche et vous invite à fournir un titre et un nom d’affichage à votre environnement de test. Le **titre d’affichage** est prévu pour être lu par un utilisateur et doit être suffisamment descriptif pour permettre son identification rapide. The sandbox **[!UICONTROL Name]** is an all-lowercase identifier for use in API calls, and should therefore be unique and concise.

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE]
>
>Étant donné que vous êtes limité à la création d’environnement de test de type hors production, l’option **[!UICONTROL type]** est verrouillée sur « hors production » et ne peut pas être modifiée.

Once you have finished creating the sandbox, refresh the page and the new sandbox appears in the **[!UICONTROL Sandboxes]** dashboard with a status of &quot;[!UICONTROL Creating]&quot;. New sandboxes take approximately 15 minutes to be provisioned by the system, after which their status changes to &quot;[!UICONTROL Active]&quot;.

![](../images/ui/sandbox-created.png)

## Réinitialisation d’un environnement de test

>[!NOTE]
>
>Cette fonctionnalité est disponible uniquement pour les environnements de test hors production. Il n’est pas possible de réinitialiser les environnements de test de production.

La réinitialisation d’un environnement de test hors production supprime toutes les ressources associées à cet environnement de test (schémas, jeux de données, etc.) tout en conservant le nom et les autorisations associés de l’environnement de test. Cet environnement de test « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

Pour réinitialiser un environnement de test dans l’interface utilisateur, cliquez sur **[!UICONTROL Environnements de test]** dans le menu de navigation de gauche, puis cliquez sur l’environnement de test que vous souhaitez réinitialiser. Dans la boîte de dialogue qui apparaît sur le côté droit de l’écran, cliquez sur **[!UICONTROL Réinitialiser un environnement de test]**.

![](../images/ui/reset-sandbox-button.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Cliquez sur **[!UICONTROL Réinitialiser]** pour continuer.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

A confirmation message appears and the sandbox&#39;s state changes to &quot;[!UICONTROL Resetting]&quot;. Once it has been provisioned by the system, its state will update to &quot;[!UICONTROL Active]&quot; or &quot;[!UICONTROL Failed]&quot;.

![](../images/ui/sandbox-resetting.png)

## Suppression d’un environnement de test

>[!NOTE]
>
>Cette fonctionnalité est disponible uniquement pour les environnements de test hors production. Il n’est pas possible de supprimer les environnements de test de production.

La suppression d’un environnement de test hors production supprime définitivement toutes les ressources associées à cet environnement de test, y compris les autorisations.

Pour supprimer un environnement de test dans l’interface utilisateur, cliquez sur **[!UICONTROL Environnements de test]** dans le menu de navigation de gauche, puis cliquez sur l’environnement de test que vous souhaitez supprimer. Dans la boîte de dialogue qui apparaît sur le côté droit de l’écran, cliquez sur **[!UICONTROL Supprimer l’environnement de test]**.

![](../images/ui/delete-sandbox-button.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Cliquez sur **[!UICONTROL Supprimer]** pour continuer.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

Un message de confirmation s’affiche et l’environnement de test est supprimé de l’espace de travail **[!UICONTROL Environnements de test]**.

## Étapes suivantes

Ce document vous a montré comment gérer les environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur la gestion des environnements de test à l’aide de l’API Sandbox, consultez le [guide de développement des environnements de test](../api/getting-started.md).
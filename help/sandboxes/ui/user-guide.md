---
keywords: Experience Platform ; accueil ; rubriques populaires ; guide de l’utilisateur sandbox ; guide sandbox
solution: Experience Platform
title: Guide de l’interface utilisateur Sandbox
topic: Guide de l’utilisateur
description: Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux environnements de test dans l’interface utilisateur d’Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 48%

---


# Guide de l’interface utilisateur Sandbox

Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux environnements de test dans l’interface utilisateur d’Adobe Experience Platform.

## Affichage des environnements de test

Dans l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Sandbox]** dans le volet de navigation de gauche pour ouvrir le tableau de bord **[!UICONTROL Sandbox]**. Le tableau de bord répertorie tous les environnements de test disponibles pour votre organisation, y compris le type d’environnement de test (production ou développement) et l’état (actif, en cours de création, supprimé ou en échec).

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

La boîte de dialogue **[!UICONTROL Créer un environnement de test]** s’affiche et vous invite à fournir un titre et un nom d’affichage à votre environnement de test. Le **titre d’affichage** est prévu pour être lu par un utilisateur et doit être suffisamment descriptif pour permettre son identification rapide. Le sandbox **[!UICONTROL Name]** est un identifiant en minuscules qui doit être utilisé dans les appels d&#39;API et doit donc être unique et concis. Le sandbox **[!UICONTROL Name]** ne doit être composé que de caractères alphanumériques et de tirets **(-)**, il doit commencer par une lettre et comporter au maximum 256 caractères.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer]**.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Étant donné que vous êtes limité à la création d’environnement de test de type hors production, l’option **[!UICONTROL type]** est verrouillée sur « hors production » et ne peut pas être modifiée.

Une fois le sandbox créé, actualisez la page et le nouveau sandbox apparaît dans le tableau de bord **[!UICONTROL Sandbox]** avec l’état &quot;[!UICONTROL Création]&quot;. Les nouveaux sandbox prennent environ 15 minutes pour être approvisionnés par le système, après quoi leur état passe à &quot;[!UICONTROL Principal]&quot;.

![](../images/ui/creating.png)

## Réinitialisation d’un environnement de test

>[!NOTE]
>
>Cette fonctionnalité est disponible uniquement pour les environnements de test hors production. Il n’est pas possible de réinitialiser les environnements de test de production.

La réinitialisation d’un environnement de test hors production supprime toutes les ressources associées à cet environnement de test (schémas, jeux de données, etc.) tout en conservant le nom et les autorisations associés de l’environnement de test. Cet environnement de test « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

Pour réinitialiser un sandbox dans l’interface utilisateur, sélectionnez **[!UICONTROL Sandbox]** dans le volet de navigation de gauche, puis sélectionnez le sandbox à réinitialiser. Dans la boîte de dialogue qui s’affiche sur le côté droit de l’écran, sélectionnez **[!UICONTROL Réinitialiser Sandbox]**.

![](../images/ui/reset-sandbox.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Réinitialiser]** pour continuer.

![](../images/ui/reset-confirm.png)

Un message de confirmation s’affiche et l’état du sandbox passe à &quot;**[!UICONTROL Réinitialisation]&quot;**. Une fois que le système l&#39;a configuré, son état est mis à jour vers **&quot;[!UICONTROL Principal]&quot;** ou **&quot;[!UICONTROL Échec]&quot;**.

![](../images/ui/resetting.png)

## Suppression d’un environnement de test

>[!NOTE]
>
>Cette fonctionnalité est disponible uniquement pour les environnements de test hors production. Il n’est pas possible de supprimer les environnements de test de production.

La suppression d’un environnement de test hors production supprime définitivement toutes les ressources associées à cet environnement de test, y compris les autorisations.

Pour supprimer un sandbox dans l’interface utilisateur, sélectionnez **[!UICONTROL Sandbox]** dans le volet de navigation de gauche, puis sélectionnez le sandbox à supprimer. Dans la boîte de dialogue qui s’affiche sur le côté droit de l’écran, sélectionnez **[!UICONTROL Supprimer le sandbox]**.

![](../images/ui/delete-sandbox.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Supprimer]** pour continuer.

![](../images/ui/delete-confirm.png)

Un message de confirmation s’affiche et l’environnement de test est supprimé de l’espace de travail **[!UICONTROL Environnements de test]**.

## Étapes suivantes

Ce document vous a montré comment gérer les environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur la gestion des environnements de test à l’aide de l’API Sandbox, consultez le [guide de développement des environnements de test](../api/getting-started.md).
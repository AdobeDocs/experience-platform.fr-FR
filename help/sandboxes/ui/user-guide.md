---
keywords: Experience Platform ; accueil ; rubriques populaires ; guide de l’utilisateur sandbox ; guide sandbox
solution: Experience Platform
title: Guide de l’interface utilisateur Sandbox
topic: Guide de l’utilisateur
description: Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux environnements de test dans l’interface utilisateur d’Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 28%

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

>[!NOTE]
>
>La fonctionnalité de sandbox de production multiple est en version bêta.

La vidéo suivante présente un aperçu rapide de l’utilisation des sandbox dans l’Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Pour créer un nouveau sandbox, sélectionnez le bouton **[!UICONTROL Créer un sandbox]** dans la partie supérieure droite de l’écran.

![](../images/ui/create-sandbox.png)

La boîte de dialogue **[!UICONTROL Créer un sandbox]** s&#39;affiche, vous invitant à fournir un type, un titre et un nom pour le sandbox. Si vous créez un sandbox de développement, sélectionnez **[!UICONTROL Développement]** dans le panneau déroulant qui s’affiche. Si vous créez un sandbox de production, sélectionnez **[!UICONTROL Production]**.

Le titre est destiné à être lisible par l&#39;homme et doit être suffisamment descriptif pour être facilement identifiable. Le nom du sandbox est un identifiant en minuscules utilisé dans les appels d’API et doit donc être unique et concis. Le nom du sandbox ne doit contenir que des caractères alphanumériques et des tirets (`-`), il doit commencer par une lettre et comporter au maximum 256 caractères.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer]**.

![](../images/ui/create-dialog.png)

Une fois le sandbox créé, actualisez la page et le nouveau sandbox apparaît dans le tableau de bord **[!UICONTROL Sandbox]** avec l’état &quot;[!UICONTROL Création]&quot;. Les nouveaux sandbox prennent environ 15 minutes pour être approvisionnés par le système, après quoi leur état passe à &quot;[!UICONTROL Principal]&quot;.

## Réinitialisation d’un environnement de test

>[!NOTE]
>
>Vous pouvez réinitialiser n’importe quel sandbox de production ou de développement de votre entreprise, à l’exception du sandbox de production par défaut.

La réinitialisation d’un sandbox de production ou de développement supprime toutes les ressources associées à ce sandbox (schémas, jeux de données, etc.), tout en conservant le nom du sandbox et les autorisations associées. Cet environnement de test « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

Sélectionnez le sandbox à réinitialiser à partir de la liste des sandbox. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Sandbox reset]**.

![](../images/ui/reset-sandbox.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Continuer]** pour continuer.

![](../images/ui/reset-confirm.png)

Dans la fenêtre de confirmation finale, saisissez le nom du sandbox dans la boîte de dialogue et sélectionnez **[!UICONTROL Réinitialiser]**.

![](../images/ui/reset-final-confirm.png)

## Suppression d’un environnement de test

>[!NOTE]
>
>Vous pouvez supprimer n’importe quel sandbox de production ou de développement de votre entreprise, à l’exception du sandbox de production par défaut.

La suppression d’un sandbox de production ou de développement supprime définitivement toutes les ressources associées à ce sandbox, y compris les autorisations.

Sélectionnez le sandbox à supprimer de la liste des sandbox. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Supprimer]**.

![](../images/ui/delete-sandbox.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Continuer]** pour continuer.

![](../images/ui/delete-confirm.png)

Dans la fenêtre de confirmation finale, saisissez le nom du sandbox dans la boîte de dialogue et sélectionnez **[!UICONTROL Supprimer]**.

![](../images/ui/delete-final-confirm.png)

## Étapes suivantes

Ce document vous a montré comment gérer les environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur la gestion des environnements de test à l’aide de l’API Sandbox, consultez le [guide de développement des environnements de test](../api/getting-started.md).
---
keywords: Experience Platform;gestion des balises;balises;
title: Gérer les balises unifiées
description: Ce document est consacré à la gestion des balises unifiées dans Adobe Experience Cloud.
source-git-commit: 6f9787909b8155d2bf032b4a42483f2cb4d44eb4
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 100%

---

# Guide de gestion des balises

Les balises permettent de gérer des taxonomies de métadonnées afin de classer les objets d’entreprise pour une découverte et un classement plus simples. Les balises permettent d’identifier les attributs taxonomiques importants des audiences utilisées par vos équipes. Ces dernières peuvent ainsi les trouver plus rapidement et également regrouper des audiences communes à l’aide d’un descripteur. Vous devez identifier les catégories de balises courantes, telles que les régions géographiques, les unités commerciales, les lignes de produits, les projets, les équipes, les périodes (trimestres, mois, années) ou toute autre catégorie qui peut aider à donner du sens à votre équipe et à faciliter la découverte d’audiences. 

## Créer une balise {#create-tag}

Pour créer une balise, sélectionnez **[!UICONTROL balises]** dans le volet de navigation de gauche, puis cliquez sur la catégorie de balises de votre choix.

![Sélection d’une catégorie de balises.](./images/tag-selection.png)

Sélectionnez **[!UICONTROL Créer une balise]** pour effectuer l’action éponyme.

![Création d’une balise.](./images/new-tag.png)

La boîte de dialogue **[!UICONTROL Créer une balise]** s’affiche et vous invite à saisir un nom de balise unique. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![La boîte de dialogue Créer une balise avec un nouveau nom de balise.](./images/create-tag-dialog.png)

La nouvelle balise a été créée avec succès et nous vous redirigeons vers l’écran des balises, où la nouvelle balise apparaît dans la liste.

![Balise nouvellement créée dans la catégorie de balises.](./images/new-tag-listed.png)

## Modifier une balise {#edit-tag}

Modifiez une balise pour corriger les fautes d’orthographe, ou appliquer la convention de nommage ou la terminologie la plus récente. La modification d’une balise conserve son association avec les objets où elle est actuellement appliquée.

Pour modifier une balise existante, procédez comme suit : dans la liste des catégories de balises, cliquez sur les points de suspension (`...`) en regard du nom de la balise que vous souhaitez modifier. Une liste déroulante affiche différentes commandes permettant de modifier, de déplacer ou d’archiver la balise. Sélectionnez **[!UICONTROL Modifier]** dans la liste déroulante.

![L’action Modifier est affichée dans la liste déroulante.](./images/edit-action.png)

La boîte de dialogue **[!UICONTROL Modifier la balise]** s’affiche et vous invite à modifier le nom de la balise. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![Boîte de dialogue Modifier la balise avec le nom de balise mis à jour.](./images/edit-dialog.png)

Le nom de la balise a été mis à jour. Nous vous redirigeons vers l’écran des balises, où la balise mise à jour apparaît dans la liste.

![Balise mise à jour dans la catégorie de balises.](./images/updated-tag-listed.png)

## Déplacer une balise entre catégories {#move-tag}

Les balises peuvent être déplacées vers d’autres catégories de balises. Le déplacement d’une balise conserve son association avec tous les objets où elle est actuellement appliquée.

Pour déplacer une balise existante, procédez comme suit : dans la liste des catégories de balises, cliquez sur les points de suspension (`...`) en regard du nom de la balise que vous souhaitez déplacer. Une liste déroulante affiche différentes commandes permettant de modifier, de déplacer ou d’archiver la balise. Cliquez sur **[!UICONTROL Modifier]** dans la liste déroulante.

![L’action Déplacer s’affiche dans la liste déroulante.](./images/move-action.png)

La boîte de dialogue **[!UICONTROL Déplacer la balise]** s’affiche et vous invite à sélectionner la catégorie de balises dans laquelle la balise sélectionnée doit être déplacée.

Vous pouvez faire défiler la liste et sélectionner la catégorie de votre choix ou utiliser la fonctionnalité de recherche en saisissant le nom de la catégorie. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Déplacer]**.

![La boîte de dialogue Déplacer la balise avec les critères de recherche pour trouver la catégorie de balises.](./images/move-dialog.png)

La balise a été déplacée avec succès et nous vous redirigeons vers l’écran des balises : la liste des balises mise à jour s’affiche et la balise n’y apparaît plus.

![Liste des balises mise à jour dans la catégorie de balises actuelle.](./images/current-tag-category.png)

La balise se trouve désormais dans la catégorie de balises précédemment sélectionnée.

![Liste des balises dans la catégorie de balises sélectionnée pour déplacer la balise.](./images/moved-to-tag-category.png)

## Archiver une balise {#archive-tag}

Le statut d’une balise peut être défini sur actif ou archivé. Les balises archivées ne sont pas supprimées des objets où elles ont déjà été appliquées, mais elles ne peuvent plus être appliquées aux nouveaux objets. Le statut d’une balise est le même dans tous les objets. Ceci s’avère particulièrement utile lorsque vous souhaitez conserver les associations actuelles entre la balise et ses objets, mais que vous ne souhaitez pas que la balise soit utilisée à l’avenir.

Pour archiver une balise existante, procédez comme suit : dans la liste des catégories de balises, sélectionnez les points de suspension (`...`) en regard du nom de la balise que vous souhaitez archiver. Une liste déroulante affiche différentes commandes permettant de modifier, de déplacer ou d’archiver la balise. Cliquez sur **[!UICONTROL Archiver]** dans la liste déroulante.

![Action d’archivage affichée dans la liste déroulante.](./images/archive-action.png)

La boîte de dialogue **[!UICONTROL Archiver la balise]** s’affiche et vous invite à confirmer l’opération. Cliquez sur **[!UICONTROL Archiver]**.

![La boîte de dialogue Archiver la balise s’affiche pour confirmer l’opération.](./images/archive-dialog.png)

La balise est archivée avec succès et nous vous redirigeons vers l’écran des balises. La liste des balises mise à jour affiche désormais le statut suivant pour la balise : `Archived`.

![Liste des balises mise à jour dans la catégorie de balises active, avec la balise affichant le statut Archivé.](./images/archive-status.png)

## Restaurer une balise archivée {#restore-archived-tag}

Si vous souhaitez appliquer une balise au statut `Archived` pour créer des objets, le statut de la balise doit être le suivant : `Active`. Si une balise archivée est restaurée, son statut passe à : `Active`.

Pour restaurer une balise archivée, procédez comme suit : dans la liste des catégories de balises, cliquez sur les points de suspension (`...`) en regard du nom de la balise à restaurer. Une liste déroulante affiche les commandes permettant de restaurer ou de supprimer la balise. Cliquez sur **[!UICONTROL Restaurer]** dans la liste déroulante.

![L’action de restauration s’affiche dans la liste déroulante.](./images/restore-action.png)

La boîte de dialogue **[!UICONTROL Restaurer la balise]** s’affiche et vous invite à confirmer l’opération. Cliquez sur **[!UICONTROL Restaurer]**.

![La boîte de dialogue Restaurer la balise s’affiche pour confirmer l’opération.](./images/restore-dialog.png)

La balise est restaurée avec succès et nous vous redirigeons vers l’écran des balises. Dans la liste des balises mise à jour qui s’affiche, la balise possède maintenant le statut suivant : `Active`.

![Liste des balises mise à jour dans la catégorie de balises active, avec la balise dotée du statut Actif.](./images/restored-active-status.png)

## Supprimer une balise {#delete-tag}

>[!NOTE]
>
>Seules les balises dont le statut est `Archived` et qui ne sont associées à aucun objet peuvent être supprimées.

La suppression d’une balise l’élimine complètement du système.

Pour supprimer une balise archivée, procédez comme suit : dans la liste des catégories de balises, cliquez sur les points de suspension (`...`) en regard du nom de la balise que vous souhaitez supprimer. Une liste déroulante affiche les commandes permettant de restaurer ou de supprimer la balise. Cliquez sur **[!UICONTROL Supprimer]** dans la liste déroulante.

![L’action Supprimer s’affiche dans la liste déroulante.](./images/delete-action.png)

La boîte de dialogue **[!UICONTROL Supprimer la balise]** s’affiche et vous invite à confirmer l’opération. Sélectionnez **[!UICONTROL Supprimer]**.

![La boîte de dialogue Supprimer la balise s’affiche pour confirmer l’opération.](./images/delete-dialog.png)

La balise a été supprimée avec succès et nous vous redirigeons vers l’écran des balises. La balise n’apparaît plus dans la liste et a été complètement supprimée du système.

![La liste des balises mise à jour dans la catégorie de balises active, qui ne contient plus la balise.](./images/deleted-updated-list.png)

## Afficher les objets balisés {#view-tagged}

Chaque balise comporte une page de détails, accessible à partir de l’inventaire des balises. Cette page répertorie tous les objets où la balise est actuellement appliquée. Les utilisateurs et les utilisatrices peuvent ainsi consulter en un seul endroit tous les objets associés à différentes applications et fonctionnalités.

Pour afficher la liste des objets balisés, recherchez la balise dans une catégorie de balises, puis sélectionnez la balise.

![Sélection d’une balise dans la catégorie de balises.](./images/view-tag-selection.png)

La page des [!UICONTROL Objets balisés] s’affiche.

![Inventaire des objets balisés.](./images/tagged-objects.png)

## Étapes suivantes

La gestion des balises n’a à présent plus de secret pour vous. Pour une présentation générale des balises dans Experience Platform, consultez la [documentation de présentation des balises](../overview.md).

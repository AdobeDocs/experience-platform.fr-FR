---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Création d’un rôle de contrôle d’accès basé sur les attributs
description: Ce document fournit des informations sur la gestion des rôles via l’interface Autorisations dans Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 74980c6108a32ec6736ab5892d89590e04e8a500
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 15%

---

# Gérer les rôles

Les rôles définissent l’accès d’un administrateur, d’un spécialiste ou d’un utilisateur final aux ressources de votre organisation. Dans un environnement de contrôle d’accès basé sur les rôles, la configuration de l’accès des utilisateurs est regroupée suivant les responsabilités et les besoins communs. Un rôle possède un jeu d’autorisations déterminé et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin.

## Créer un rôle {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Créer un rôle"
>abstract="Créez de nouveaux rôles pour mieux classer les utilisateurs interagissant avec votre instance Platform. Par exemple, vous pouvez créer un rôle pour une équipe marketing interne et lui appliquer le libellé Données réglementées en matière de santé (DSR), ce qui permet à votre équipe marketing interne d’accéder aux informations de santé protégées (ISP). Vous pouvez également créer un rôle pour une agence externe et refuser l’accès à ce rôle aux données ISP en vous abstenant d’appliquer le libellé RHD à ce rôle."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=fr" text="Gérer un rôle"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="Appliquer des libellés à un rôle"

Pour créer un nouveau rôle, sélectionnez l’onglet **[!UICONTROL Rôles]** dans la barre latérale et sélectionnez **[!UICONTROL Créer un rôle]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

La boîte de dialogue **[!UICONTROL Créer un nouveau rôle]** s’affiche et vous invite à saisir un nom et une description facultative.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Confirmer]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Sélectionnez ensuite les autorisations de ressources que vous souhaitez inclure dans le rôle à l’aide du menu déroulant.

![Autorisation FLAC ajouter rôle](../../images/flac-ui/flac-add-role-permission.png)

Pour ajouter des ressources supplémentaires, sélectionnez **[!UICONTROL Adobe Experience Platform]** dans le panneau de navigation de gauche, qui affiche une liste de ressources. Vous pouvez également saisir le nom de la ressource dans la barre de recherche du panneau de navigation de gauche.

![ajout-ressources-FLAC](../../images/flac-ui/flac-add-additional-resources.png)

Cliquez sur la ressource appropriée, faites-la glisser et déposez-la dans le panneau principal.

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

Sélectionnez les autorisations de ressources que vous souhaitez inclure dans le rôle à l’aide du menu déroulant. Répétez cette opération pour toutes les ressources que vous souhaitez inclure pour le rôle. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer et quitter]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Le nouveau rôle a été créé avec succès et vous êtes redirigé vers la page **[!UICONTROL Rôles]**, où le nouveau rôle apparaît dans la liste.

![rôle-FLAC enregistré](../../images/flac-ui/flac-role-saved.png)

Consultez les sections sur la [gestion des autorisations pour un rôle](#manage-permissions-for-a-role) pour plus d’informations sur la gestion des autorisations de rôle une fois qu’elles ont été créées.

La vidéo suivante est destinée à vous aider à comprendre la création d’un rôle et la gestion des utilisateurs et utilisatrices pour ce rôle.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Dupliquer un rôle

Pour dupliquer un rôle existant, sélectionnez-le dans l’onglet **[!UICONTROL Rôles]**. Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver le rôle à dupliquer.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Sélectionnez ensuite **[!UICONTROL Dupliquer]** dans le coin supérieur droit de l’écran.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

La boîte de dialogue **[!UICONTROL Dupliquer le rôle]** s’affiche, vous invitant à confirmer la duplication.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Ensuite, vous accédez à la page des détails du rôle dans laquelle vous pouvez modifier le nom et les autorisations du rôle. Les détails, les libellés et les sandbox sont dupliqués à partir du rôle précédent. Les utilisateurs devront être ajoutés à partir de l’onglet utilisateurs . Vous pouvez consulter le document [gérer les autorisations pour un rôle](permissions.md) pour en savoir plus sur l’ajout de détails, de libellés, de sandbox et d’utilisateurs à un rôle.

Cliquez sur la flèche de gauche pour revenir à l’onglet **[!UICONTROL Rôles]**.

![retour FLAC aux rôles](../../images/flac-ui/flac-return-to-roles.png)

Le nouveau rôle apparaît dans la liste de la page **[!UICONTROL Rôles]**.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Supprimer un rôle

Sélectionnez les points de suspension (`…`) en regard du nom d’un rôle. Une liste déroulante affiche alors les commandes permettant de modifier, supprimer ou dupliquer le rôle. Sélectionnez Supprimer dans la liste déroulante.

![suppression-rôle-FLAC](../../images/flac-ui/flac-role-delete.png)

La boîte de dialogue **[!UICONTROL Supprimer le rôle d’utilisateur]** s’affiche et vous invite à confirmer la suppression.

![Confirmer la suppression du rôle FLAC](../../images/flac-ui/flac-confirm-role-delete.png)

Vous revenez alors à l’onglet **[!UICONTROL Rôles]**.

## Étapes suivantes

Après avoir créé un nouveau rôle, vous pouvez passer à l’étape suivante pour [gérer les autorisations pour un rôle](permissions.md).

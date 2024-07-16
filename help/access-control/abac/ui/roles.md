---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: 'Contrôle d’accès basé sur les attributs : créer un rôle'
description: Ce document fournit des informations sur la gestion des rôles par le biais de l’interface Autorisations dans Adobe Experience Cloud.
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: d8f72bb5ae56daf5a41c763f821ca6306514bc48
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 15%

---

# Gérer les rôles

Les rôles définissent l’accès dont dispose un administrateur, un spécialiste ou un utilisateur final aux ressources de votre entreprise. Dans un environnement de contrôle d’accès basé sur les rôles, la configuration de l’accès des utilisateurs est regroupée suivant les responsabilités et les besoins communs. Un rôle possède un jeu d’autorisations déterminé et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin.

## Créer un rôle

Pour créer un nouveau rôle, sélectionnez l’onglet **[!UICONTROL Rôles]** dans la barre latérale et sélectionnez **[!UICONTROL Créer un rôle]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

La boîte de dialogue **[!UICONTROL Créer un nouveau rôle]** s’affiche, vous invitant à saisir un nom et une description facultative.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Confirmer]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Sélectionnez ensuite les autorisations de ressources que vous souhaitez inclure dans le rôle à l’aide du menu déroulant.

![Autorisation FLAC ajouter rôle](../../images/flac-ui/flac-add-role-permission.png)

Pour ajouter des ressources supplémentaires, sélectionnez **[!UICONTROL Adobe Experience Platform]** dans le panneau de navigation de gauche, qui affiche une liste des ressources. Vous pouvez également saisir le nom de la ressource dans la barre de recherche du panneau de navigation de gauche.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Cliquez et faites glisser la ressource concernée et déposez-la dans le panneau principal.

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

Sélectionnez les autorisations de ressources que vous souhaitez inclure dans le rôle à l’aide du menu déroulant. Répétez cette opération pour toutes les ressources que vous souhaitez inclure pour le rôle . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer et quitter]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Le nouveau rôle a été créé avec succès et vous êtes redirigé vers la page **[!UICONTROL Rôles]** où le nouveau rôle apparaîtra dans la liste.

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

Consultez les sections sur la [gestion des autorisations pour un rôle](#manage-permissions-for-a-role) pour plus d’informations sur la gestion des autorisations de rôle une fois qu’elles ont été créées.

La vidéo suivante est destinée à vous aider à comprendre comment créer un nouveau rôle et gérer les utilisateurs pour ce rôle.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Dupliquer un rôle

Pour dupliquer un rôle existant, sélectionnez le rôle dans l’onglet **[!UICONTROL Rôles]** . Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver le rôle que vous souhaitez dupliquer.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Ensuite, sélectionnez **[!UICONTROL Dupliquer]** en haut à droite de l’écran.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

La boîte de dialogue **[!UICONTROL Dupliquer le rôle]** s’affiche, vous invitant à confirmer la duplication.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Ensuite, vous accédez à la page des détails du rôle dans laquelle vous pouvez modifier le nom et les autorisations du rôle. Les environnements Détails, Étiquettes et Sandbox sont dupliqués à partir du rôle précédent. Les utilisateurs doivent être ajoutés depuis l&#39;onglet Utilisateurs . Vous pouvez afficher le document [gérer les autorisations pour un rôle](permissions.md) pour en savoir plus sur l’ajout de détails, d’étiquettes, de sandbox et d’utilisateurs à un rôle.

Cliquez sur la flèche gauche pour revenir à l’onglet **[!UICONTROL Rôles]** .

![flac-return-to-role](../../images/flac-ui/flac-return-to-roles.png)

Le nouveau rôle apparaîtra dans la liste de la page **[!UICONTROL Rôles]** .

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Suppression d’un rôle

Sélectionnez les points de suspension (`…`) en regard du nom d’un rôle et une liste déroulante affiche les commandes permettant de modifier, supprimer ou dupliquer le rôle. Sélectionnez Supprimer dans la liste déroulante.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

La boîte de dialogue **[!UICONTROL Supprimer le rôle utilisateur]** s’affiche et vous invite à confirmer la suppression.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Vous serez alors renvoyé à l&#39;onglet **[!UICONTROL Rôles]** .

## Étapes suivantes

Une fois un nouveau rôle créé, vous pouvez passer à l’étape suivante : [gérer les autorisations pour un rôle](permissions.md).

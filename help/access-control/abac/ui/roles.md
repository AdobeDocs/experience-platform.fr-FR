---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Création d’un rôle de contrôle d’accès basé sur les attributs
description: Gérez les rôles via l’interface Autorisations dans Adobe Experience Cloud.
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 14%

---

# Gérer les rôles

<!-- UPDATE ROLES WITH A MORE COMPREHENSIVE EXPLANATION -->

Pour commencer à gérer les rôles, accédez à **[!UICONTROL Permissions]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"} puis sélectionnez **[!UICONTROL Roles]** dans le panneau de gauche.

![Espace de travail Rôles dans Autorisations.](../../images/ui/roles/roles-overview.png)

## Créer un rôle {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Créer un rôle"
>abstract="Créez de nouveaux rôles pour mieux classer les personnes interagissant avec votre instance Experience Platform. Par exemple, vous pouvez créer un rôle pour une équipe marketing interne et lui appliquer le libellé RHD. Cela permettra à l’équipe d’accéder aux informations de santé protégées (ISP). Vous pouvez également créer un rôle pour une agence externe et refuser l’accès à ce rôle aux données ISP en vous abstenant d’appliquer le libellé RHD à ce rôle."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=fr" text="Gérer un rôle"
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="Appliquer des libellés à un rôle"

Pour créer un nouveau rôle, sélectionnez **[!UICONTROL Create role]**.

>[!TIP]
>
>Les rôles en lecture seule sont disponibles par défaut. Un rôle en lecture seule est un rôle qui permet à un utilisateur d’afficher les données, la configuration et les fonctionnalités de l’interface utilisateur sans avoir à modifier l’état du système. Les administrateurs ne peuvent pas modifier ces rôles, mais peuvent associer des utilisateurs aux rôles.

![Espace de travail du rôle avec l’option Créer un rôle mise en surbrillance.](../../images/ui/roles/roles-create-role.png)

La boîte de dialogue **[!UICONTROL Create new role]** s’affiche. Saisissez un **[!UICONTROL Name]** pour le rôle et, éventuellement, un **[!UICONTROL Description]**, puis sélectionnez **[!UICONTROL Confirm]**.

![La boîte de dialogue Créer des rôles avec le nom et la description renseignés et l’option Confirmer mise en surbrillance.](../../images/ui/roles/roles-create-new-role.png)

L’espace de travail **[!UICONTROL Resources]** s’affiche. Recherchez la ressource dont vous avez besoin en faisant défiler l’écran ou en saisissant le nom de la ressource dans la barre de recherche du panneau de gauche. Ajoutez des ressources en sélectionnant l’icône ![Plus](/help/images/icons/plus.png) en regard du nom de la ressource.

![Espace de travail Ressources avec l’option Ajouter d’une ressource individuelle mise en surbrillance.](../../images/ui/roles/roles-resources.png)

<!-- ADD IN NOTE ABOUT THE DEFAULT SANDBOX - THIS SHOULD BE MENTIONED IN THE HIGHER LEVEL DOCS, WE MAY BE ABLE TO LINK TO IT -->

La ressource est ajoutée à l’espace de travail principal. Sélectionnez la liste déroulante à côté du nom de la ressource, puis sélectionnez les autorisations que vous souhaitez ajouter au rôle. Vous pouvez les choisir individuellement, sélectionner des **[!UICONTROL Add all]** ou rechercher des autorisations spécifiques en saisissant le nom de l’autorisation dans la barre de recherche.

![Espace de travail Ressources avec le menu déroulant d’une ressource individuelle développé et mis en surbrillance.](../../images/ui/roles/roles-resources-permissions.png)

Continuez à sélectionner toutes les ressources et les autorisations que vous souhaitez ajouter au rôle. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]**.

![Espace de travail Ressources avec l’option Enregistrer mise en surbrillance.](../../images/ui/roles/roles-resources-permissions-save.png)

Vous recevrez une alerte indiquant que le rôle a été enregistré avec succès. Sélectionnez **[!UICONTROL Close]** pour revenir à l’espace de travail **[!UICONTROL Roles]**.

![L’espace de travail Ressources avec l’alerte de succès et l’option Fermer mise en surbrillance.](../../images/ui/roles/roles-resources-permissions-close.png)

Le nouveau rôle a été créé avec succès et vous êtes redirigé vers la page **[!UICONTROL Roles]**, où le nouveau rôle apparaît dans la liste.

<!-- The following video is intended to support your understanding of creating a new role and managing users for that role.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on) -->

## Dupliquer un rôle

La duplication d’un rôle entraîne la copie sur les détails, les autorisations, les libellés et les sandbox. Les utilisateurs, les groupes d’utilisateurs et d’utilisatrices et les informations d’identification d’API **ne sont pas** copiés et devront être ajoutés manuellement au rôle.

Pour dupliquer un rôle existant, recherchez le rôle que vous souhaitez dupliquer dans l’onglet **[!UICONTROL Roles]** . Sélectionnez l’icône ![&#x200B; Plus &#x200B;](/help/images/icons/more.png) à côté du nom du rôle, puis sélectionnez **[!UICONTROL Duplicate]** dans le menu déroulant.

![Espace de travail Rôles avec le menu déroulant d’un rôle développé et l’option Dupliquer mise en surbrillance.](../../images/ui/roles/role-duplicate.png)

La boîte de dialogue de confirmation de duplication s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer la duplication du rôle. Le nouveau rôle sera enregistré sous le même nom avec `_Copy` ajouté comme suffixe.

![Boîte de dialogue de confirmation en double avec l’option Confirmer mise en surbrillance.](../../images/ui/roles/role-duplicate-confirm.png)

Vous pouvez également dupliquer un rôle depuis l’espace de travail d’un rôle individuel. Sélectionnez le rôle que vous souhaitez dupliquer dans l’espace de travail **[!UICONTROL Roles]**, puis sélectionnez **[!UICONTROL Duplicate]**.

![Espace de travail d’un rôle individuel avec l’option Dupliquer mise en surbrillance.](../../images/ui/roles/role-duplicate-alt.png)

La boîte de dialogue de confirmation de duplication s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer la duplication du rôle. Vous serez redirigé vers le nouveau rôle.

![Boîte de dialogue de confirmation en double avec l’option Confirmer mise en surbrillance.](../../images/ui/roles/role-duplicate-alt-confirm.png)

## Supprimer un rôle

Pour supprimer un rôle, recherchez le rôle que vous souhaitez supprimer dans l’onglet **[!UICONTROL Roles]** . Sélectionnez l’icône ![&#x200B; Plus &#x200B;](/help/images/icons/more.png) à côté du nom du rôle, puis sélectionnez **[!UICONTROL Delete]** dans le menu déroulant.

![Espace de travail Rôles avec le menu déroulant d’un rôle développé et l’option Dupliquer mise en surbrillance.](../../images/ui/roles/role-delete.png)

La boîte de dialogue de confirmation de suppression s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer la suppression du rôle.

![Boîte de dialogue de confirmation en double avec l’option Confirmer mise en surbrillance.](../../images/ui/roles/role-duplicate-confirm.png)

Vous pouvez également supprimer un rôle dans l’espace de travail d’un rôle individuel. Sélectionnez le rôle que vous souhaitez supprimer de l’espace de travail **[!UICONTROL Roles]**, puis sélectionnez **[!UICONTROL Delete]**.

![Espace de travail d’un rôle individuel avec l’option Supprimer mise en surbrillance.](../../images/ui/roles/role-delete-alt.png)

La boîte de dialogue de confirmation de suppression s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer la suppression du rôle.

![Boîte de dialogue de confirmation de suppression avec l’option Confirmer mise en surbrillance.](../../images/ui/roles/role-delete-alt-confirm.png)

<!-- ADD PERMISSIONS TO THIS PAGE -->

## Étapes suivantes

Après avoir créé un nouveau rôle, vous pouvez passer à l’étape suivante pour [gérer les autorisations pour un rôle](permissions.md).

---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Création d’un rôle de contrôle d’accès basé sur les attributs
description: Gérez les rôles via l’interface Autorisations dans Adobe Experience Cloud.
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
TQID: https://experienceleague.adobe.com/PxhSLqPYfsF5HEGhV4Arqy9JM9aZfD05GDIRyfk4Rwg
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: adf04a6a-050f-44bc-a52c-db79ccb22ebfid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: a16ec9c0-4484-4842-b9a0-5504cde38e6aid: a9b953c0-98db-499b-97f5-a0dc3290bda3id: a9eb38d5-9d89-492f-af4e-b968a07f2d91id: d175cb4c-5781-454e-a826-bf6dff786265id: d21bd11d-08df-4cd6-ad8f-cb59a09de5c0
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12bid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 798
ht-degree: 16%

---

# Gérer les rôles

<!-- UPDATE ROLES WITH A MORE COMPREHENSIVE EXPLANATION -->

Pour commencer à gérer les rôles, accédez à **[!UICONTROL Autorisations]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"} et sélectionnez **[!UICONTROL Rôles]** dans le panneau de gauche.

![Espace de travail Rôles dans Autorisations.](../../images/ui/roles/roles-overview.png)

## Créer un rôle {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Créer un rôle"
>abstract="Créez de nouveaux rôles pour mieux classer les personnes interagissant avec votre instance Experience Platform. Par exemple, vous pouvez créer un rôle pour une équipe marketing interne et lui appliquer le libellé RHD. Cela permettra à l’équipe d’accéder aux informations de santé protégées (ISP). Vous pouvez également créer un rôle pour une agence externe et refuser l’accès à ce rôle aux données ISP en vous abstenant d’appliquer le libellé RHD à ce rôle."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=fr" text="Gérer un rôle"
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="Appliquer des libellés à un rôle"

Pour créer un nouveau rôle, sélectionnez **[!UICONTROL Créer un rôle]**.

>[!TIP]
>
>Les rôles en lecture seule sont disponibles par défaut. Un rôle en lecture seule est un rôle qui permet à un utilisateur d’afficher les données, la configuration et les fonctionnalités de l’interface utilisateur sans avoir à modifier l’état du système. Les administrateurs ne peuvent pas modifier ces rôles, mais peuvent associer des utilisateurs aux rôles.

![Espace de travail du rôle avec l’option Créer un rôle mise en surbrillance.](../../images/ui/roles/roles-create-role.png)

La boîte de dialogue **[!UICONTROL Créer un rôle]** s’affiche. Saisissez un **[!UICONTROL Nom]** pour le rôle et, éventuellement, un **[!UICONTROL Description]**, puis sélectionnez **[!UICONTROL Confirmer]**.

![La boîte de dialogue Créer des rôles avec le nom et la description renseignés et l’option Confirmer mise en surbrillance.](../../images/ui/roles/roles-create-new-role.png)

L’espace de travail **[!UICONTROL Ressources]** s’affiche. Recherchez la ressource dont vous avez besoin en faisant défiler l’écran ou en saisissant le nom de la ressource dans la barre de recherche du panneau de gauche. Ajoutez des ressources en sélectionnant l’icône ![Plus](/help/images/icons/plus.png) en regard du nom de la ressource.

![Espace de travail Ressources avec l’option Ajouter d’une ressource individuelle mise en surbrillance.](../../images/ui/roles/roles-resources.png)

<!-- ADD IN NOTE ABOUT THE DEFAULT SANDBOX - THIS SHOULD BE MENTIONED IN THE HIGHER LEVEL DOCS, WE MAY BE ABLE TO LINK TO IT -->

La ressource est ajoutée à l’espace de travail principal. Sélectionnez la liste déroulante à côté du nom de la ressource, puis sélectionnez les autorisations que vous souhaitez ajouter au rôle. Vous pouvez les choisir individuellement, sélectionner **[!UICONTROL Ajouter tout]** ou rechercher des autorisations spécifiques en saisissant le nom de l’autorisation dans la barre de recherche.

![Espace de travail Ressources avec le menu déroulant d’une ressource individuelle développé et mis en surbrillance.](../../images/ui/roles/roles-resources-permissions.png)

Continuez à sélectionner toutes les ressources et les autorisations que vous souhaitez ajouter au rôle. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Espace de travail Ressources avec l’option Enregistrer mise en surbrillance.](../../images/ui/roles/roles-resources-permissions-save.png)

Vous recevrez une alerte indiquant que le rôle a été enregistré avec succès. Sélectionnez **[!UICONTROL Fermer]** pour revenir à l’espace de travail **[!UICONTROL Rôles]**.

![L’espace de travail Ressources avec l’alerte de succès et l’option Fermer mise en surbrillance.](../../images/ui/roles/roles-resources-permissions-close.png)

Le nouveau rôle a été créé avec succès et vous êtes redirigé vers la page **[!UICONTROL Rôles]**, où le nouveau rôle apparaît dans la liste.

<!-- 
The following video is intended to support your understanding of creating a new role and managing users for that role.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on) 
-->

## Dupliquer un rôle

La duplication d’un rôle entraîne la copie sur les détails, les autorisations, les libellés et les sandbox. Les utilisateurs, les groupes d’utilisateurs et d’utilisatrices et les informations d’identification d’API **ne sont pas** copiés et devront être ajoutés manuellement au rôle.

Pour dupliquer un rôle existant, recherchez le rôle que vous souhaitez dupliquer dans l’onglet **[!UICONTROL Rôles]**. Sélectionnez l’icône ![Plus](/help/images/icons/more.png) à côté du nom du rôle, puis sélectionnez **[!UICONTROL Dupliquer]** dans le menu déroulant.

![Espace de travail Rôles avec le menu déroulant d’un rôle développé et l’option Dupliquer mise en surbrillance.](../../images/ui/roles/role-duplicate.png)

La boîte de dialogue de confirmation de duplication s’affiche. Sélectionnez **[!UICONTROL Confirmer]** pour terminer la duplication du rôle. Le nouveau rôle sera enregistré sous le même nom avec `_Copy` ajouté comme suffixe.

![Boîte de dialogue de confirmation en double avec l’option Confirmer mise en surbrillance.](../../images/ui/roles/role-duplicate-confirm.png)

Vous pouvez également dupliquer un rôle depuis l’espace de travail d’un rôle individuel. Sélectionnez le rôle que vous souhaitez dupliquer dans l’espace de travail **[!UICONTROL Rôles]** puis sélectionnez **[!UICONTROL Dupliquer]**.

![Espace de travail d’un rôle individuel avec l’option Dupliquer mise en surbrillance.](../../images/ui/roles/role-duplicate-alt.png)

La boîte de dialogue de confirmation de duplication s’affiche. Sélectionnez **[!UICONTROL Confirmer]** pour terminer la duplication du rôle. Vous serez redirigé vers le nouveau rôle.

![Boîte de dialogue de confirmation en double avec l’option Confirmer mise en surbrillance.](../../images/ui/roles/role-duplicate-alt-confirm.png)

## Supprimer un rôle

Pour supprimer un rôle, recherchez le rôle que vous souhaitez supprimer dans l’onglet **[!UICONTROL Rôles]**. Sélectionnez l’icône ![ Plus ](/help/images/icons/more.png) à côté du nom du rôle, puis sélectionnez **[!UICONTROL Supprimer]** dans le menu déroulant.

![Espace de travail Rôles avec le menu déroulant d’un rôle développé et l’option Dupliquer mise en surbrillance.](../../images/ui/roles/role-delete.png)

La boîte de dialogue de confirmation de suppression s’affiche. Sélectionnez **[!UICONTROL Confirmer]** pour terminer la suppression du rôle.

![Boîte de dialogue de confirmation en double avec l’option Confirmer mise en surbrillance.](../../images/ui/roles/role-duplicate-confirm.png)

Vous pouvez également supprimer un rôle dans l’espace de travail d’un rôle individuel. Sélectionnez le rôle que vous souhaitez supprimer de l’espace de travail **[!UICONTROL Rôles]** puis sélectionnez **[!UICONTROL Supprimer]**.

![Espace de travail d’un rôle individuel avec l’option Supprimer mise en surbrillance.](../../images/ui/roles/role-delete-alt.png)

La boîte de dialogue de confirmation de suppression s’affiche. Sélectionnez **[!UICONTROL Confirmer]** pour terminer la suppression du rôle.

![Boîte de dialogue de confirmation de suppression avec l’option Confirmer mise en surbrillance.](../../images/ui/roles/role-delete-alt-confirm.png)

<!-- ADD PERMISSIONS TO THIS PAGE -->

## Étapes suivantes

Après avoir créé un nouveau rôle, vous pouvez passer à l’étape suivante pour [gérer les autorisations pour un rôle](permissions.md).

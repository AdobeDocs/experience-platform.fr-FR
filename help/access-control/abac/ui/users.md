---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des utilisateurs du contrôle d’accès basé sur les attributs
description: Gérez les utilisateurs et les groupes d’utilisateurs via l’interface Autorisations dans Adobe Experience Cloud.
exl-id: 16450867-040a-4be1-a6c0-f03d0a1b90ba
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 7%

---

# Gestion des utilisateurs et ajout de groupes d’utilisateurs {#manage-users}

>[!CONTEXTUALHELP]
>id="platform_permissions_users_about"
>title="Que sont les utilisateurs et utilisatrices ?"
>abstract="Il s’agit de personnes qui ont accès à Experience Platform. Leur accès aux ressources d’une organisation est géré par l’intermédiaire de rôles."
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/abac/permissions-ui/roles" text="Gérer les rôles"

Les utilisateurs sont les personnes qui ont accès à Adobe Experience Platform. L’accès d’un utilisateur individuel aux ressources d’une organisation est géré au moyen de [rôles](./roles.md){target="_blank"}. Une entreprise peut également créer des [groupes d’utilisateurs](#user-groups) pour offrir un accès transparent à plusieurs utilisateurs et utilisatrices en même temps. Les utilisateurs sont gérés dans Admin Console et les utilisateurs associés à la carte de produit Adobe Experience Platform apparaissent dans la liste des utilisateurs d’Experience Platform.

## Gérer les utilisateurs et les utilisatrices

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform users. To add users to Experience Platform, navigate to Adobe Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add users through the Admin Console, follow the [adding users to Experience Platform](...){#target="_blank"} guide.
-->

Pour afficher les utilisateurs de votre organisation, accédez à **[!UICONTROL Permissions]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Sélectionnez **[!UICONTROL Users]** dans le panneau de gauche.

![Espace de travail Utilisateurs dans Autorisations.](../../images/ui/users/users-overview.png){zoomable="yes"}

Une liste d’utilisateurs s’affiche. Sélectionnez l’utilisateur que vous souhaitez afficher dans la liste. Vous pouvez également utiliser la barre de recherche pour rechercher un utilisateur en saisissant son nom ou son adresse e-mail.

L’onglet **[!UICONTROL Details]** donne un aperçu de l’utilisateur. L’aperçu affiche le **[!UICONTROL Name]**, le **[!UICONTROL Preferred languages]**, le **[!UICONTROL Account Type]**, le **[!UICONTROL Authentication ID]**, le **[!UICONTROL Email]**, le statut de **[!UICONTROL Email verified]**, le **[!UICONTROL Country code]** et le **[!UICONTROL Phone number]** de l’utilisateur ou de l’utilisatrice.

![Espace de travail Détails d’un utilisateur.](../../images/ui/users/user-details.png){zoomable="yes"}

Sélectionnez l’onglet **[!UICONTROL Roles]** pour afficher les rôles affectés à l’utilisateur.

![Espace de travail Rôles d’un utilisateur.](../../images/ui/users/user-roles.png){zoomable="yes"}

### Ajouter un rôle à un utilisateur {#add-user-role}

Pour ajouter un rôle à l’utilisateur, sélectionnez **[!UICONTROL Add Roles]**.

![Espace de travail du rôle de l’utilisateur avec l’option Ajouter des rôles mise en surbrillance.](../../images/ui/users/user-add-roles.png){zoomable="yes"}

La boîte de dialogue **[!UICONTROL Add Roles]** s’affiche. Sélectionnez le ou les rôles que vous souhaitez ajouter à l’utilisateur, puis sélectionnez **[!UICONTROL Save]**.

![La boîte de dialogue Ajouter des rôles avec les rôles sélectionnés et l’option d’enregistrement mise en surbrillance.](../../images/ui/users/user-roles-add-roles-confirm.png){zoomable="yes"}

### Supprimer un rôle d’un utilisateur {#remove-user-role}

Pour supprimer un rôle de l’utilisateur ou de l’utilisatrice, sélectionnez le **X** en regard du nom du rôle.

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW

>[!NOTE]
>
>Role's that have been added to a user through a user group cannot be removed through the user's role workspace. Role's that have been added through a user group will have an [!Info icon](/help/images/icons/info.png) beside the **X** containing information about the associated user group. To remove the role, the role would need to be [removed from the user group](#remove-user-group-role).
-->

![Espace de travail Rôles d’un utilisateur avec l’option de suppression du rôle mise en surbrillance.](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

Une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer la suppression du rôle.

![La boîte de dialogue de confirmation pour supprimer un rôle avec l’option Confirmer mise en surbrillance.](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

## Gestion des groupes d’utilisateurs {#user-groups}

Les groupes d’utilisateurs consistent en plusieurs utilisateurs qui ont été regroupés et qui disposent des accès pour exécuter les mêmes fonctions.

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform user groups. To add user groups to Experience Platform, navigate to Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add user groups in the Admin Console, follow the [adding user groups to Experience Platform](...){#target="_blank"} guide.
 -->

Pour afficher les utilisateurs de votre organisation, accédez à **[!UICONTROL Permissions]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}.Sélectionnez **[!UICONTROL Groups]** dans la section **[!UICONTROL Users]** du panneau de gauche.

![L’espace de travail Groupes d’utilisateurs dans Autorisations.](../../images/ui/users/user-groups-overview.png){zoomable="yes"}

Une liste de groupes d’utilisateurs s’affiche. Sélectionnez le groupe que vous souhaitez afficher dans la liste.

L’onglet **[!UICONTROL Details]** donne un aperçu du groupe d’utilisateurs. La vue d’ensemble affiche les **[!UICONTROL Name]**, **[!UICONTROL Description]**, **[!UICONTROL User Count]** et **[!UICONTROL Admin count]** des groupes.

![Espace de travail Détails du groupe d’utilisateurs.](../../images/ui/users/user-group-details.png){zoomable="yes"}

Sélectionnez l’onglet **[!UICONTROL Users]** pour afficher la liste des utilisateurs affectés au groupe.

![Espace de travail Utilisateurs d’un groupe d’utilisateurs.](../../images/ui/users/user-group-users.png){zoomable="yes"}

Sélectionnez l’onglet **[!UICONTROL Roles]** pour afficher la liste des rôles actuellement affectés au groupe.

![Espace de travail Rôles d’un groupe d’utilisateurs.](../../images/ui/users/user-group-roles.png){zoomable="yes"}

### Ajouter des rôles à un groupe d’utilisateurs {#add-user-group-role}

Pour ajouter un nouveau rôle au groupe, sélectionnez **[!UICONTROL Add Roles]**.

![Espace de travail Rôles d’un groupe d’utilisateurs avec l’option Ajouter des rôles mise en surbrillance.](../../images/ui/users/user-group-add-roles.png){zoomable="yes"}

La boîte de dialogue **[!UICONTROL Add Roles]** s’affiche. Sélectionnez le ou les rôles que vous souhaitez ajouter, puis sélectionnez **[!UICONTROL Save]**. Les rôles seront ajoutés pour tous les utilisateurs appartenant au groupe d’utilisateurs.

![La boîte de dialogue Ajouter des rôles avec un rôle sélectionné et l’option Enregistrer mise en surbrillance.](../../images/ui/users/user-group-add-roles-select.png){zoomable="yes"}

### Supprimer des rôles d’un groupe d’utilisateurs {#remove-user-group-role}

Pour supprimer un rôle du groupe d’utilisateurs, sélectionnez le **X** en regard du nom du rôle.

![Espace de travail Rôles d’un groupe d’utilisateurs avec l’option de suppression d’un rôle mise en surbrillance.](../../images/ui/users/user-group-remove-role.png){zoomable="yes"}

Une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer la suppression du rôle.

![La boîte de dialogue de confirmation pour supprimer un rôle avec l’option Confirmer mise en surbrillance.](../../images/ui/users/user-group-remove-role-confirm.png){zoomable="yes"}

## Informations d’identification de l’API

>[!IMPORTANT]
>
>Seuls les administrateurs système ont la possibilité d’afficher et de gérer les informations d’identification d’API dans les autorisations.

Pour utiliser les API d’Experience Platform en tant qu’utilisateur ou développeur, un administrateur système doit ajouter des informations d’identification d’API en plus du jeu d’autorisations donné à un rôle. Les autorisations vous permettent d’affecter aux rôles des informations d’identification d’API créées précédemment et affectées au produit Experience Platform. Pour obtenir un guide complet sur la création et l’attribution des informations d’identification d’API, ainsi que les autorisations nécessaires, reportez-vous au tutoriel détaillé dans [Authentification et accès aux API Experience Platform](/help/landing/api-authentication.md){target="_blank"}.

Pour afficher les informations d’identification d’API de votre organisation associées à Experience Platform, accédez à **[!UICONTROL Permissions]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Sélectionnez **[!UICONTROL API Credentials]** dans la section **[!UICONTROL Users]** du panneau de gauche.

![Espace de travail Informations d’identification de l’API dans Autorisations.](../../images/ui/users/api-credentials-overview.png){zoomable="yes"}

>[!NOTE]
>
> Pour afficher les informations d’identification de l’API de votre organisation pour tous les produits de votre organisation ou pour plus d’informations sur les informations d’identification, sélectionnez **[!UICONTROL Edit in admin console]**.

Une liste des informations d’identification d’API s’affiche. Sélectionnez les informations d’identification d’API à afficher dans la liste.

L’onglet **[!UICONTROL Details]** donne un aperçu des informations d’identification de l’API. La vue d’ensemble affiche le **[!UICONTROL Name]**, la date de **[!UICONTROL Modified]**, l’attribut de **[!UICONTROL Modified By]**, la date de **[!UICONTROL Created]**, l’attribut de **[!UICONTROL Created by]**, la **[!UICONTROL API key]**, la **[!UICONTROL Technical ID]** et la **[!UICONTROL Email]** des informations d’identification.

![Espace de travail des détails des informations d’identification de l’API.](../../images/ui/users/api-credential-details.png){zoomable="yes"}

Sélectionnez l’onglet **[!UICONTROL Roles]** . Une liste des rôles associés aux informations d’identification d’API s’affiche.

![Espace de travail des rôles d’informations d’identification d’API.](../../images/ui/users/api-credential-roles.png){zoomable="yes"}

### Ajouter un rôle à des informations d’identification d’API {#add-api-credential-role}

Pour ajouter un rôle aux informations d’identification d’API, sélectionnez **[!UICONTROL Add Roles]**.

![Espace de travail des informations d’identification de l’API avec l’option Ajouter des rôles mise en surbrillance.](../../images/ui/users/api-credential-add-roles.png){zoomable="yes"}

La boîte de dialogue **[!UICONTROL Add Roles]** s’affiche. Sélectionnez le ou les rôles que vous souhaitez ajouter à l’utilisateur, puis sélectionnez **[!UICONTROL Save]**.

![La boîte de dialogue Ajouter des rôles avec les rôles sélectionnés et l’option d’enregistrement mise en surbrillance.](../../images/ui/users/api-credential-add-roles-select.png){zoomable="yes"}

### Supprimer un rôle d’informations d’identification d’API {#remove-api-credential-role}

Pour supprimer un rôle des informations d’identification de l’API, sélectionnez le **X** en regard du nom des informations d’identification de l’API.

![Espace de travail Rôles d’informations d’identification d’API avec l’option de suppression d’un rôle mise en surbrillance.](../../images/ui/users/api-credential-remove-role.png){zoomable="yes"}

Une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer la suppression du rôle.

![La boîte de dialogue de confirmation pour supprimer un rôle avec l’option Confirmer mise en surbrillance.](../../images/ui/users/api-credential-remove-role-confirm.png){zoomable="yes"}

## Étapes suivantes

Vous savez maintenant comment afficher les détails et les rôles d’un utilisateur, d’un groupe d’utilisateurs et d’informations d’identification d’API. Pour en savoir plus sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../overview.md).

<!--
The following video is intended to support your understanding of developer and API credentials.

>[!VIDEO](https://video.tv.adobe.com/v/3426407/?learn=on)
-->
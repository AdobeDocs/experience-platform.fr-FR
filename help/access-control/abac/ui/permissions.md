---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des autorisations de rôle du contrôle d’accès basé sur les attributs
description: Ce document fournit des informations sur la configuration des autorisations pour un rôle dans l’interface Autorisations d’Adobe Experience Cloud.
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 37%

---

# Gestion des autorisations pour un rôle {#manage-role-permissions}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Que sont les rôles ?"
>abstract="Les rôles définissent l’accès d’un administrateur, d’une administratrice, d’un ou d’une spécialiste ou encore d’un utilisateur final ou d’une utilisatrice finale, aux ressources de votre organisation. Ils catégorisent les personnes interagissant avec votre instance Experience Platform et constituent les blocs de construction des politiques de contrôle d’accès. Un rôle possède un jeu d’autorisations déterminé et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=fr" text="Gérer les rôles"

>[!IMPORTANT]
>
>Le contrôle d’accès utilise un identifiant d’utilisateur (un identifiant unique interne attribué à un utilisateur) pour accorder des autorisations. Lorsqu’une organisation est migrée d’Adobe ID vers Business ID, toutes les autorisations définies pour ses utilisateurs seront perdues car l’identifiant d’utilisateur change et le contrôle d’accès utilisera l’identifiant d’utilisateur nouvellement généré. Si votre entreprise est migrée vers un Business ID, contactez votre représentant Adobe pour migrer votre identifiant d’utilisateur d’Adobe ID vers un Business ID.

La zone dédiée aux autorisations dans Experience Cloud permet aux administrateurs de définir des rôles d’utilisateur et des politiques d’accès. Ils peuvent ainsi gérer les autorisations d’accès aux fonctionnalités et objets dans une application de produit.

Grâce aux autorisations, vous pouvez créer et gérer des rôles, ainsi qu’attribuer les autorisations de ressource souhaitées pour ces rôles. Les autorisations vous permettent également de gérer les libellés, les sandbox et les utilisateurs associés à un rôle spécifique.

Immédiatement après la [création d’un nouveau rôle](#create-a-new-role), vous revenez sur l’onglet **[!UICONTROL Roles]** . Si vous modifiez les autorisations d’un rôle existant, sélectionnez le rôle dans l’onglet **[!UICONTROL Roles]** . Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver un rôle.

## Filtrer les rôles

Sélectionnez l’icône en forme d’entonnoir (![icône filtre](/help/images/icons/filter.png)) pour afficher une liste de contrôles de filtre afin de limiter les résultats.

![Tableau de bord Rôles dans l’interface utilisateur Autorisations avec la section des rôles de filtre mise en surbrillance.](../../images/flac-ui/flac-filters.png)

Les filtres suivants sont disponibles pour les rôles dans l’interface utilisateur :

| Filtre | Description |
| --- | --- |
| [!UICONTROL Created between] | Sélectionnez une date de début et/ou une date de fin pour définir une période en fonction de laquelle filtrer les résultats. |
| [!UICONTROL Created by] | Filtrez par créateur de rôle en sélectionnant un utilisateur dans le menu déroulant. |
| [!UICONTROL Modified between] | Sélectionnez une date de début et/ou une date de fin pour définir une période en fonction de laquelle filtrer les résultats. |
| [!UICONTROL Modified by] | Vous pouvez filtrer par modificateur de rôle en sélectionnant un utilisateur dans le menu déroulant. |

Pour supprimer un filtre, sélectionnez « X » sur l’icône de pilule du filtre en question, ou sélectionnez **[!UICONTROL Clear all]** pour supprimer tous les filtres.

![Tableau de bord Rôles de l’interface utilisateur Autorisations avec le X et Effacer toutes les sélections en surbrillance sur les filtres sélectionnés.](../../images/flac-ui/flac-clear-filters.png)

## Détails du rôle {#role-details}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Vue d’ensemble des rôles"
>abstract="La boîte de dialogue de la vue d’ensemble des rôles affiche les ressources et les sandbox auxquelles un rôle donné peut accéder. Vous pouvez gérer les libellés, les personnes, les groupes de personnes, ainsi que les informations d’identification d’API pour le rôle en accédant à l’onglet correspondant dans l’espace de travail du rôle."
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-labels-for-a-role" text="Gérer les libellés d’un rôle"
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-users-for-a-role" text="Gérer les personnes utilisant un rôle"

Sélectionnez le rôle dans l’onglet **[!UICONTROL Roles]** qui ouvre le tableau de bord de [!UICONTROL Details] du rôle.

![L’espace de travail Détails du rôle sélectionné s’affiche avec les informations de présentation en surbrillance.](../../images/flac-ui/flac-details.png)

Le tableau de bord [!UICONTROL Details] fournit une vue d’ensemble du rôle. La vue d’ensemble affiche le nom du rôle, la description, le créateur et la dernière modification, ainsi que les dates de création et de modification. Elle affiche également les autorisations associées au rôle et la liste des sandbox attribués. Le nom et la description du rôle peuvent être modifiés si nécessaire.

## Gérer les libellés d’un rôle

Sélectionnez l’onglet **[!UICONTROL Labels]** pour ouvrir l’espace de travail libellés des rôles, puis sélectionnez **[!UICONTROL Add labels]** pour affecter des libellés au rôle.

![L’espace de travail Libellés du rôle s’affiche avec l’onglet Libellés et le bouton Ajouter des libellés en surbrillance.](../../images/flac-ui/flac-labels.png)

La boîte de dialogue **[!UICONTROL Apply Access and Data Governance Labels]** s’affiche, présentant une liste de libellés. La liste affiche le nom du libellé, le nom convivial, la catégorie et sa description.

Sélectionnez dans la liste les libellés que vous souhaitez ajouter au rôle, puis sélectionnez **[!UICONTROL Save]**

![La boîte de dialogue Appliquer l’accès et Libellés de gouvernance des données affiche un libellé sélectionné.](../../images/flac-ui/flac-add-labels.png)

Les libellés ajoutés apparaissent sous l’onglet **[!UICONTROL Labels]** .

![Espace de travail Libellés du rôle avec le libellé ajouté mis en surbrillance.](../../images/flac-ui/flac-added-labels.png)

Pour supprimer un libellé d’un rôle, sélectionnez-le, puis sélectionnez **[!UICONTROL Remove Labels]**.

![Espace de travail Libellés du rôle avec un rôle sélectionné et l’option Supprimer les libellés mise en surbrillance.](../../images/flac-ui/flac-delete-labels.png)

## Gestion des sandbox pour un rôle

Sélectionnez l’onglet **[!UICONTROL Details]** et accédez à la section **[!UICONTROL Sandboxes]** . Sélectionnez **[!UICONTROL View All]** pour afficher la liste complète des sandbox ajoutés au rôle.

![Espace de travail Détails du rôle avec la section Sandbox mise en surbrillance.](../../images/flac-ui/flac-sandboxes.png)

Pour ajouter d’autres sandbox à un rôle, sélectionnez **[!UICONTROL Edit]** dans le coin supérieur droit de l’interface utilisateur.

![Espace de travail Détails du rôle avec l’option Modifier mise en surbrillance.](../../images/flac-ui/flac-add-sandboxes.png)

L’écran suivant vous invite à choisir les ressources de sandbox à inclure dans le rôle à l’aide de la liste déroulante. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]** puis **[!UICONTROL Close]**.

![Tableau de bord des ressources du rôle avec le menu déroulant des ressources du sandbox en surbrillance.](../../images/flac-ui/flac-add-role-permission.png)

## Gérer les personnes utilisant un rôle

Sélectionnez l’onglet **[!UICONTROL Users]** pour ouvrir les rôles [!UICONTROL Users] l’espace de travail, puis sélectionnez **[!UICONTROL Add Users]** pour affecter des utilisateurs au rôle.

![L’espace de travail Utilisateurs du rôle s’affiche avec l’onglet Utilisateurs et l’option Ajouter des utilisateurs en surbrillance.](../../images/flac-ui/flac-users.png)

La boîte de dialogue **[!UICONTROL Add Users]** s’affiche. Sélectionnez dans la liste les utilisateurs que vous souhaitez ajouter au rôle. Vous pouvez également utiliser la barre de recherche pour rechercher un utilisateur en saisissant son nom ou son adresse électronique, puis sélectionner **[!UICONTROL Save]**

![La boîte de dialogue Ajouter des utilisateurs avec un utilisateur sélectionné et la barre de recherche et l’option d’enregistrement mises en surbrillance.](../../images/flac-ui/flac-add-users.png)

Les utilisateurs ajoutés apparaissent sous l’onglet **[!UICONTROL Users]** .

![Espace de travail Utilisateurs du rôle affichant les utilisateurs ajoutés au rôle.](../../images/flac-ui/flac-added-users.png)

Pour supprimer un utilisateur d’un rôle, sélectionnez l’icône **X** en regard du nom de l’utilisateur.

![Espace de travail Utilisateurs du rôle présentant un utilisateur avec l’option X mise en surbrillance.](../../images/flac-ui/flac-remove-users.png)

La vidéo suivante est destinée à vous aider à comprendre la création d’un rôle et la gestion des utilisateurs et utilisatrices pour ce rôle.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Gérer les informations d’identification d’API pour un rôle {#manage-api-credentials-for-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_apicredentials_about"
>title="Que sont les informations d’identification d’API ?"
>abstract="Les informations d’identification d’API sont attribuées aux rôles pour accorder aux utilisateurs et utilisatrices, et aux développeurs et développeuses, l’accès aux API Experience Platform. Grâce aux API Experience Platform, vous pouvez effectuer par programmation des opérations CRUD (créer, lire, mettre à jour, supprimer) de base sur les données, telles que la configuration des attributs calculés, l’accès aux données/entités, l’export des données, la suppression des données ou lots inutiles, etc."
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/landing/platform-apis/api-guide" text="Guide de l’API Experience Platform"

>[!IMPORTANT]
>
> Pour utiliser et gérer les informations d’identification d’API dans [!UICONTROL Permissions], les utilisateurs doivent disposer de droits d’administrateur système.

Pour utiliser les API d’Experience Platform en tant qu’utilisateur ou développeur, un administrateur système doit ajouter des informations d’identification d’API en plus du jeu d’autorisations donné à un rôle. Pour obtenir un guide complet sur la création et l’attribution des informations d’identification d’API, ainsi que les autorisations nécessaires, reportez-vous au tutoriel détaillé dans [Authentification et accès aux API Experience Platform](../../../landing/api-authentication.md#generate-credentials).

Sélectionnez l’onglet **[!UICONTROL API credentials]** pour ouvrir l’espace de travail Rôles API > Informations d’identification , puis sélectionnez **[!UICONTROL Add API credentials]** pour affecter les informations d’identification API au rôle.

![Espace de travail des informations d’identification de l’API du rôle avec l’option Ajouter des informations d’identification mise en surbrillance.](../../images/flac-ui/flac-api-credentials.png)

La boîte de dialogue **[!UICONTROL Add API credentials]** s’affiche. Sélectionnez dans la liste les informations d’identification d’API à ajouter au rôle, puis sélectionnez **[!UICONTROL Save]**

![La boîte de dialogue Ajouter des informations d’identification d’API avec des informations d’identification sélectionnées et l’option Enregistrer mise en surbrillance.](../../images/flac-ui/flac-add-api-credentials.png)

Les informations d’identification d’API ajoutées apparaissent sous **[!UICONTROL API credentials]** onglet .

![Espace de travail des informations d’identification de l’API du rôle avec les informations d’identification ajoutées affichées.](../../images/flac-ui/flac-added-api-credentials.png)

Pour supprimer des informations d’identification d’API d’un rôle, sélectionnez l’icône **X** à côté du nom des informations d’identification d’API.

![Espace de travail des informations d’identification de l’API du rôle avec l’option X pour supprimer des informations d’identification en surbrillance.](../../images/flac-ui/flac-remove-api-credentials.png)

La boîte de dialogue **[!UICONTROL Remove API credentials]** s’affiche, vous invitant à confirmer la suppression. Sélectionnez **[!UICONTROL Confirm]** pour terminer la suppression des informations d’identification sélectionnées.

![La fenêtre contextuelle Supprimer des informations d’identification vous invitant à confirmer la suppression des informations d’identification est mise en surbrillance.](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Vous revenez alors à l’onglet **[!UICONTROL API credentials]** .

## Gérer des groupes d’utilisateurs et d’utilisatrices pour un rôle {#manage-user-groups}

>[!CONTEXTUALHELP]
>id="platform_permissions_usergroups_about"
>title="Que sont les groupes d’utilisateurs et d’utilisatrices ?"
>abstract="Les groupes d’utilisateurs et d’utilisatrices sont des ensembles d’utilisateurs et d’utilisatrices qui partagent l’accès aux mêmes fonctions. L’accès aux ressources au sein d’une organisation est géré par l’intermédiaire de rôles affectés à des groupes d’utilisateurs et d’utilisatrices."
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/abac/permissions-ui/roles" text="Gérer les rôles"

Les groupes d’utilisateurs consistent en plusieurs utilisateurs qui ont été regroupés et qui disposent des accès pour exécuter les mêmes fonctions.

Sélectionnez l’onglet **[!UICONTROL User groups]** pour ouvrir l’espace de travail des groupes d’utilisateurs du rôle, puis sélectionnez **[!UICONTROL Add Groups]** pour affecter des groupes d’utilisateurs au rôle.

![Espace de travail Groupes d’utilisateurs du rôle avec l’option Ajouter des groupes ](../../images/flac-ui/flac-user-groups.png)

La boîte de dialogue **[!UICONTROL Add Groups]** s’affiche. Sélectionnez dans la liste les groupes d’utilisateurs que vous souhaitez ajouter au rôle. Vous pouvez également utiliser la barre de recherche pour rechercher le groupe d’utilisateurs en saisissant le nom du groupe, puis sélectionner **[!UICONTROL Save]**

![La boîte de dialogue Ajouter des groupes avec un groupe d’utilisateurs sélectionné et l’option de recherche et d’enregistrement mise en surbrillance.](../../images/flac-ui/flac-add-user-groups.png)

Le groupe d’utilisateurs ajouté s’affiche sous l’onglet **[!UICONTROL User groups]** .

![Espace de travail Groupes d’utilisateurs du rôle affichant la liste des groupes d’utilisateurs ajoutés.](../../images/flac-ui/flac-added-user-groups.png)

Pour supprimer un groupe d’utilisateurs d’un rôle, sélectionnez l’icône **X** à côté du nom du groupe d’utilisateurs.

![Espace de travail Groupes d’utilisateurs du rôle avec l’option X pour supprimer un groupe d’utilisateurs spécifique en surbrillance.](../../images/flac-ui/flac-remove-user-groups.png)

La boîte de dialogue **[!UICONTROL Remove user group]** s’affiche, vous invitant à confirmer la suppression. Sélectionnez **[!UICONTROL Confirm]** pour supprimer le groupe d’utilisateurs sélectionné.

![La fenêtre contextuelle permettant de supprimer un groupe d’utilisateurs s’affiche et est mise en surbrillance.](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Vous revenez alors à l’onglet **[!UICONTROL User groups]** .

## Ajout d’utilisateurs à Experience Platform

En tant qu’administrateur système, vous pouvez accorder l’accès développeur à un utilisateur afin qu’il puisse [créer des intégrations](../../../landing/api-authentication.md#generate-credentials) dans Adobe Developer Console.

Pour ajouter un utilisateur Experience Platform, connectez-vous à [Admin Console](https://adminconsole.adobe.com) et sélectionnez **[!UICONTROL Add users]**.

![Tableau de bord Adobe Admin Console avec l’option Ajouter des utilisateurs mise en surbrillance.](../../images/flac-ui/product-profile-add-users.png)

La boîte de dialogue **[!UICONTROL Add users to your team]** s’affiche. Saisissez l’adresse e-mail, le prénom (facultatif) et le nom de l’utilisateur (facultatif). Sélectionnez ensuite **[!UICONTROL Products]**.

![La boîte de dialogue Ajouter des utilisateurs à votre équipe avec l’option Champs utilisateur et Produits mise en surbrillance.](../../images/flac-ui/product-profile-add-users-to-your-team.png)

La boîte de dialogue **[!UICONTROL Select products]** s’affiche. Sélectionnez **[!UICONTROL Adobe Experience Platform]**.

![La boîte de dialogue de sélection des produits avec Adobe Experience Platform mis en surbrillance.](../../images/flac-ui/product-profile-select-product.png)

La boîte de dialogue **[!UICONTROL Select product profiles]** s’affiche. Sélectionnez **[!UICONTROL AEP-Default-All-Users]** puis sélectionnez **[!UICONTROL Save]**.

![La boîte de dialogue Sélectionner des profils de produit avec AEP-Default-All-Users sélectionné et Appliquer en surbrillance.](../../images/flac-ui/product-profile-select-product-profiles.png)

Vérifiez les informations, puis sélectionnez **[!UICONTROL Save]** pour ajouter l’utilisateur.

![La boîte de dialogue Ajouter des utilisateurs à votre équipe affiche les informations sur l’utilisateur et les sélections sélectionnées, ainsi que l’option Enregistrer mise en surbrillance](../../images/flac-ui/product-profile-save-user.png).

## Étapes suivantes

Une fois les autorisations établies, vous pouvez passer à l’étape suivante de [gestion des utilisateurs](users.md).

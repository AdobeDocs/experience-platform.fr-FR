---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des autorisations de rôle du contrôle d’accès basé sur les attributs
description: Ce document fournit des informations sur le contrôle d’accès basé sur les attributs dans Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Gestion des autorisations pour un rôle

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible dans une version limitée pour les clients de santé basés aux États-Unis. Cette fonctionnalité sera disponible pour tous les clients Real-time Customer Data Platform une fois qu’elle sera entièrement publiée.

Immédiatement après [création d’un nouveau rôle](#create-a-new-role), vous revenez au **[!UICONTROL Rôles]** . Si vous modifiez les autorisations d’un rôle existant, sélectionnez le rôle dans la **[!UICONTROL Rôles]** . Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver un rôle.

## Filtrage des rôles

Sélectionnez l’icône d’entonnoir (![Icône Filtrer](../../images/icon.png)) pour afficher une liste de contrôles de filtre afin de limiter les résultats.

![flac-filters](../../images/flac-ui/flac-filters.png)

Les filtres suivants sont disponibles pour les rôles dans l’interface utilisateur :

| Filtrer | Description |
| --- | --- |
| [!UICONTROL Créé entre] | Sélectionnez une date de début et/ou une date de fin pour définir une période en fonction de laquelle filtrer les résultats. |
| [!UICONTROL Créé par] | Filtrez par créateur de rôles en sélectionnant un utilisateur dans la liste déroulante. |
| [!UICONTROL Modifié entre] | Sélectionnez une date de début et/ou une date de fin pour définir une période en fonction de laquelle filtrer les résultats. |
| [!UICONTROL Modified by] | Vous pouvez filtrer par modificateur de rôle en sélectionnant un utilisateur dans la liste déroulante. |

Pour supprimer un filtre, sélectionnez le &quot;X&quot; sur l’icône de pilule du filtre en question, ou sélectionnez **[!UICONTROL Effacer tout]** pour supprimer tous les filtres.

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## Détails du rôle

Sélectionnez le rôle dans la **[!UICONTROL Rôles]** qui ouvre la page des détails du rôle.

![flac-details](../../images/flac-ui/flac-details.png)

L’onglet Détails présente un aperçu du rôle. La présentation affiche le nom du rôle, la description du rôle, le nom de l’utilisateur qui a créé et modifié le rôle, la date de création et de modification du rôle, ainsi que les autorisations associées au rôle. Le nom du rôle et sa description peuvent être modifiés, si nécessaire.

## Gestion des libellés d’un rôle

Sélectionnez la **[!UICONTROL Étiquettes]** pour ouvrir la page libellés des rôles, puis sélectionnez **[!UICONTROL Ajouter des étiquettes]** pour affecter des libellés au rôle.

![flac-libellés](../../images/flac-ui/flac-labels.png)

Les libellés sont répertoriés sur cette page. La liste affiche le nom du libellé, le nom convivial, la catégorie et sa description.

Sélectionnez les libellés de la liste que vous souhaitez ajouter au rôle, puis sélectionnez **[!UICONTROL Enregistrer]**

![flac-add-libellés](../../images/flac-ui/flac-add-labels.png)

Les libellés ajoutés apparaissent sous **[!UICONTROL Étiquettes]** .

![flac-added-libellés](../../images/flac-ui/flac-added-labels.png)

Pour supprimer un libellé d’un rôle, sélectionnez l’option **X** en regard du nom des étiquettes.

![flac-delete-libellés](../../images/flac-ui/flac-delete-labels.png)

## Gestion des environnements de test pour le rôle

Sélectionnez la **[!UICONTROL Environnements de test]** pour ouvrir la page sandbox des rôles. Vous trouverez ici une liste des environnements de test qui ont été ajoutés au rôle .

![flac-sandbox](../../images/flac-ui/flac-sandboxes.png)

Pour ajouter d’autres environnements de test à une sélection de rôle **[!UICONTROL Modifier]**.

![flac-add-sandbox](../../images/flac-ui/flac-add-sandboxes.png)

L’écran suivant vous invite à choisir les autorisations de ressources qui existent dans les environnements de test à inclure dans le rôle à l’aide de la liste déroulante. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer et quitter]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## Gestion des utilisateurs pour le rôle

Sélectionnez la **[!UICONTROL Utilisateurs]** pour ouvrir la page rôles utilisateurs, puis sélectionnez **[!UICONTROL Ajout d’utilisateurs]** pour affecter des utilisateurs au rôle.

![flac-users](../../images/flac-ui/flac-users.png)

Sélectionnez les utilisateurs dans la liste que vous souhaitez ajouter au rôle. Vous pouvez également utiliser la barre de recherche pour rechercher un utilisateur en saisissant son nom ou son adresse électronique, puis sélectionner **[!UICONTROL Enregistrer]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

Les utilisateurs ajoutés apparaissent sous **[!UICONTROL Utilisateurs]** .

![flac-added-users](../../images/flac-ui/flac-added-users.png)

Pour supprimer un utilisateur d’un rôle, sélectionnez l’option **X** en regard du nom des utilisateurs.

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

## Gestion des informations d’identification d’API pour le rôle

Sélectionnez la **[!UICONTROL Informations d’identification de l’API]** pour ouvrir la page des informations d’identification de l’API des rôles, puis sélectionnez **[!UICONTROL Ajout des informations d’identification d’API]** pour attribuer des informations d’identification d’API au rôle.

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

Sélectionnez les informations d’identification de l’API dans la liste que vous souhaitez ajouter au rôle, puis sélectionnez **[!UICONTROL Enregistrer]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

Ajout des informations d’identification d’API sous **[!UICONTROL Informations d’identification de l’API]** .

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

Pour supprimer des informations d’identification d’API d’un rôle, sélectionnez l’option **X** en regard du nom des informations d’identification de l’API.

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

Le **[!UICONTROL Suppression des informations d’identification d’API]** s’affiche, vous invitant à confirmer la suppression.

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Vous revenez alors à la variable **[!UICONTROL Informations d’identification de l’API]** .

## Gestion des groupes d’utilisateurs pour les rôles

Les groupes d’utilisateurs sont plusieurs utilisateurs qui ont été regroupés et qui ont l’accès pour exécuter les mêmes fonctions.

Sélectionnez la **[!UICONTROL Groupes d’utilisateurs]** pour ouvrir la page groupes d’utilisateurs des rôles, puis sélectionnez **[!UICONTROL Ajout de groupes]** pour affecter des groupes d’utilisateurs au rôle.

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

Sélectionnez les groupes d’utilisateurs dans la liste que vous souhaitez ajouter au rôle. Vous pouvez également utiliser la barre de recherche pour rechercher le groupe d’utilisateurs en saisissant le nom du groupe, puis sélectionnez **[!UICONTROL Enregistrer]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

Le groupe d’utilisateurs ajouté apparaît sous **[!UICONTROL Groupes d’utilisateurs]** .

![flac-added-user-groups](../../images/flac-ui/flac-added-user-groups.png)

Pour supprimer un groupe d’utilisateurs d’un rôle, sélectionnez l’option **X** en regard du nom du groupe d’utilisateurs.

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

Le **[!UICONTROL Suppression d’un groupe d’utilisateurs]** s’affiche, vous invitant à confirmer la suppression.

![flac-confirm-user-groups -delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Vous revenez alors à la variable **[!UICONTROL Groupes d’utilisateurs]** .

## Étapes suivantes

Une fois les autorisations établies, vous pouvez passer à l’étape suivante pour [gestion des utilisateurs](users.md).

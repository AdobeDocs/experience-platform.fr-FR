---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des stratégies de contrôle d’accès
description: Ce document fournit des informations sur la gestion des stratégies de contrôle d’accès via l’interface Autorisations de Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 86%

---

# Gestion des stratégies de contrôle d’accès

Les politiques de contrôle d&#39;accès sont des déclarations qui rassemblent les attributs pour établir les actions permises et non autorisées. Les stratégies d’accès peuvent être locales ou globales et peuvent remplacer d’autres stratégies.

>[!IMPORTANT]
>
>Les stratégies d’accès ne doivent pas être confondues avec les stratégies d’utilisation des données, qui contrôlent la manière dont les données sont utilisées dans Adobe Experience Platform au lieu des utilisateurs de votre entreprise qui y ont accès. Consultez le guide de création [stratégies d’utilisation des données](../../../data-governance/policies/create.md) pour plus d’informations.

## Création d’une stratégie

Pour créer une stratégie, sélectionnez l’onglet **[!UICONTROL Stratégies]** dans la barre latérale et sélectionnez **[!UICONTROL Créer une stratégie]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

La boîte de dialogue **[!UICONTROL Créer une stratégie]** s’affiche, vous invitant à saisir un nom et une description facultative. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Confirmer]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

À l’aide de la flèche de liste déroulante, choisissez si vous souhaitez **Autoriser l’accès à** (![flac-allow-access-to](../../images/flac-ui/flac-permit-access-to.png)) une ressource ou **Refuser l’accès à** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) une ressource.

Sélectionnez ensuite la ressource que vous souhaitez inclure dans la stratégie à l’aide du menu déroulant et recherchez le type d’accès, en lecture ou en écriture.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Ensuite, à l’aide de la flèche déroulante, sélectionnez la condition que vous souhaitez appliquer à cette stratégie, **La valeur suivante est vraie :** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) ou **La valeur suivante est fausse :** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Sélectionnez l’icône Plus pour **Ajouter une expression de correspondances** ou **Ajouter un groupe d’expressions** pour la ressource.

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Dans la liste déroulante, sélectionnez la **Ressource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Ensuite, sélectionnez dans la liste déroulante les **Correspondances**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Sélectionnez ensuite dans la liste déroulante le type de libellé (**[!UICONTROL Libellé principal]** ou **[!UICONTROL Libellé personnalisé]**) pour correspondre au libellé attribué à l’utilisateur ou l’utilisatrice dans les rôles.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Enfin, sélectionnez la **Sandbox** à laquelle vous souhaitez appliquer les conditions de la stratégie, à l’aide du menu déroulant.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Sélectionnez **Ajouter une ressource** pour ajouter d’autres ressources. Une fois l’opération terminée, sélectionnez **[!UICONTROL Enregistrer et quitter]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

La nouvelle stratégie a été créée avec succès et vous êtes redirigé vers l’onglet **[!UICONTROL Stratégies]**, où la nouvelle stratégie apparaît dans la liste.

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Modification d’une stratégie

Pour modifier une stratégie existante, sélectionnez-la dans l’onglet **[!UICONTROL Stratégies]**. Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver la stratégie à modifier.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Sélectionnez ensuite les points de suspension (`…`) à côté du nom des stratégies. Une liste déroulante affiche alors les commandes permettant de modifier, désactiver, supprimer ou dupliquer le rôle. Sélectionnez Modifier dans la liste déroulante.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

L’écran des autorisations de stratégie s’affiche. Effectuez les mises à jour, puis sélectionnez **[!UICONTROL Enregistrer et quitter]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

La stratégie a été mise à jour avec succès et vous êtes redirigé vers l’onglet **[!UICONTROL Stratégies]**.

## Duplication de stratégie

Pour dupliquer une stratégie existante, sélectionnez-la dans l’onglet **[!UICONTROL Stratégies]**. Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver la stratégie à modifier.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Sélectionnez ensuite les points de suspension (`…`) à côté du nom des stratégies. Une liste déroulante affiche alors les commandes permettant de modifier, désactiver, supprimer ou dupliquer le rôle. Sélectionnez Dupliquer dans la liste déroulante.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

La boîte de dialogue **[!UICONTROL Dupliquer une stratégie]** s’affiche, vous invitant à confirmer la duplication.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

La nouvelle stratégie apparaît dans la liste sous la forme d’une copie de l’originale sur l’onglet **[!UICONTROL Stratégies]**.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Supprimer une politique

Pour supprimer une politique existante, sélectionnez-la dans l’onglet **[!UICONTROL Politiques]**. Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver la politique à supprimer.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Sélectionnez ensuite les points de suspension (`…`) à côté du nom des politiques, et une liste déroulante affiche les contrôles permettant de modifier, désactiver, supprimer ou dupliquer le rôle. Sélectionnez Supprimer dans la liste déroulante.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

La boîte de dialogue **[!UICONTROL Supprimer une politique d’utilisateur]** s’affiche, vous invitant à confirmer la suppression.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

Vous revenez alors à l’onglet **[!UICONTROL Politiques]** et une fenêtre contextuelle de confirmation de suppression s’affiche.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Activer une politique

Pour activer une politique existante, sélectionnez-la dans l’onglet **[!UICONTROL Politiques]**. Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver la politique à supprimer.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Sélectionnez ensuite les points de suspension (`…`) à côté du nom des politiques, et une liste déroulante affiche les contrôles permettant de modifier, désactiver, supprimer ou dupliquer le rôle. Sélectionnez Activer dans la liste déroulante.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

La boîte de dialogue **[!UICONTROL Activer une politique d’utilisateur]** s’affiche, vous invitant à confirmer l’activation.

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

Vous revenez alors à l’onglet **[!UICONTROL Politiques]** et une fenêtre contextuelle de confirmation de l’activation s’affiche. Le statut de la politique s’affiche comme actif.

![flac-policy-activated](../../images/flac-ui/flac-policy-activated.png)

## Étapes suivantes

Après avoir créé une nouvelle politique, vous pouvez passer à l’étape suivante pour [gérer les autorisations pour un rôle](permissions.md).

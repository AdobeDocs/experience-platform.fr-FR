---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Contrôle d’accès basé sur les attributs Création d’une stratégie
description: Ce document fournit des informations sur le contrôle d’accès basé sur les attributs dans Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Gestion des stratégies

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible dans une version limitée pour les clients de santé basés aux États-Unis. Cette fonctionnalité sera disponible pour tous les clients Real-time Customer Data Platform une fois qu’elle sera entièrement publiée.

Les politiques sont des déclarations qui réunissent des attributs pour établir des actions permises et non admissibles. Les stratégies peuvent être locales ou globales et peuvent remplacer d’autres stratégies.

## Création d’une stratégie

Pour créer une nouvelle stratégie, sélectionnez l’option **[!UICONTROL Stratégies]** dans la barre latérale et sélectionnez **[!UICONTROL Créer une stratégie]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

Le **[!UICONTROL Création d’une stratégie]** s’affiche, vous invitant à saisir un nom et une description facultative. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Confirmer]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

À l’aide de la flèche de liste déroulante, choisissez si vous souhaitez **Autoriser l’accès à** (![flac-allow-access-to](../../images/flac-ui/flac-permit-access-to.png)) d’une ressource ou **Refuser l’accès à** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) une ressource.

Sélectionnez ensuite la ressource que vous souhaitez inclure dans la stratégie à l’aide du menu déroulant et recherchez le type d’accès, en lecture ou en écriture.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Ensuite, à l’aide de la flèche déroulante, sélectionnez la condition que vous souhaitez appliquer à cette stratégie, **La valeur suivante est vraie :** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) ou **Les éléments suivants sont faux :** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Sélectionnez l’icône Plus pour **Ajouter une expression de correspondance** ou **Ajouter un groupe d’expressions** pour la ressource.

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Dans la liste déroulante, sélectionnez la variable **Ressource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Ensuite, sélectionnez la variable **Correspond à**.

![flac-policy-matches-menu-déroulant](../../images/flac-ui/flac-policy-matches-dropdown.png)

Sélectionnez ensuite la liste déroulante **Utilisateur**.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Enfin, sélectionnez l’option **Sandbox** que vous souhaitez appliquer aux conditions de la stratégie, à l’aide du menu déroulant.

![flac-policy-sandbox-menu-déroulant](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Sélectionner **Ajouter une ressource** pour ajouter d’autres ressources. Une fois l’opération terminée, sélectionnez **[!UICONTROL Enregistrer et quitter]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

La nouvelle stratégie a été créée avec succès et vous êtes redirigé vers le **[!UICONTROL Stratégies]** , où la nouvelle stratégie apparaît dans la liste.

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Modification d’une stratégie

Pour modifier une stratégie existante, sélectionnez-la dans le **[!UICONTROL Stratégies]** . Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver la stratégie à modifier.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Sélectionnez ensuite les points de suspension (`…`) en regard du nom des stratégies et une liste déroulante affiche les commandes permettant de modifier, désactiver, supprimer ou dupliquer le rôle. Sélectionnez Modifier dans la liste déroulante.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

L’écran des autorisations de stratégie s’affiche. Effectuez les mises à jour, puis sélectionnez **[!UICONTROL Enregistrer et quitter]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

La stratégie a été mise à jour avec succès et vous êtes redirigé vers le **[!UICONTROL Stratégies]** .

## Duplication d’une stratégie

Pour dupliquer une stratégie existante, sélectionnez-la dans le **[!UICONTROL Stratégies]** . Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver la stratégie à modifier.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Sélectionnez ensuite les points de suspension (`…`) en regard d’un nom de stratégie, et une liste déroulante affiche les commandes permettant de modifier, désactiver, supprimer ou dupliquer le rôle. Sélectionnez dupliquer dans la liste déroulante.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

Le **[!UICONTROL Duplication de stratégie]** s’affiche, vous invitant à confirmer la duplication.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

La nouvelle stratégie apparaît dans la liste sous la forme d’une copie de l’original sur la page **[!UICONTROL Stratégies]** .

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Suppression d’une stratégie

Pour supprimer une stratégie existante, sélectionnez-la dans le **[!UICONTROL Stratégies]** . Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver la stratégie à supprimer.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Sélectionnez ensuite les points de suspension (`…`) en regard d’un nom de stratégie, et une liste déroulante affiche les commandes permettant de modifier, désactiver, supprimer ou dupliquer le rôle. Sélectionnez Supprimer dans la liste déroulante.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

Le **[!UICONTROL Suppression d’une stratégie d’utilisateur]** s’affiche, vous invitant à confirmer la suppression.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

Vous revenez alors au **[!UICONTROL policies]** et une fenêtre contextuelle de confirmation de suppression s’affiche.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Activation d’une stratégie

Pour activer une stratégie existante, sélectionnez-la dans le **[!UICONTROL Stratégies]** . Vous pouvez également utiliser l’option de filtrage pour filtrer les résultats afin de trouver la stratégie à supprimer.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Sélectionnez ensuite les points de suspension (`…`) en regard d’un nom de stratégie, et une liste déroulante affiche les commandes permettant de modifier, d’activer, de supprimer ou de dupliquer le rôle. Sélectionnez Activer dans la liste déroulante.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

Le **[!UICONTROL Activation de la stratégie utilisateur]** s’affiche, vous invitant à confirmer l’activation.

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

Vous revenez alors au **[!UICONTROL policies]** et une fenêtre contextuelle de confirmation de l’activation s’affiche. L’état de la stratégie s’affiche comme principal.

![activé par flac-policy](../../images/flac-ui/flac-policy-activated.png)

## Étapes suivantes

Une fois une nouvelle stratégie créée, vous pouvez passer à l’étape suivante [gestion des autorisations pour un rôle](permissions.md).

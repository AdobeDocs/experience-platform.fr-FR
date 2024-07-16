---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des stratégies de contrôle d’accès
description: Ce document fournit des informations sur la gestion des stratégies de contrôle d’accès via l’interface Autorisations de Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 7cafe1f7e9dd6789db4199631cb605be666ce48a
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 11%

---

# Gestion des stratégies de contrôle d’accès

Les politiques de contrôle d&#39;accès sont des déclarations qui rassemblent les attributs pour établir les actions permises et non autorisées. Les stratégies d’accès peuvent être locales ou globales et peuvent remplacer d’autres stratégies. Adobe fournit une stratégie par défaut qui peut être activée immédiatement ou dès que votre entreprise est prête à commencer à contrôler l’accès à des objets spécifiques en fonction de libellés. La stratégie par défaut utilise les libellés appliqués aux ressources pour refuser l’accès, sauf si les utilisateurs disposent d’un rôle avec un libellé correspondant.

>[!IMPORTANT]
>
>Les stratégies d’accès ne doivent pas être confondues avec les stratégies d’utilisation des données, qui contrôlent la manière dont les données sont utilisées dans Adobe Experience Platform au lieu des utilisateurs de votre entreprise qui y ont accès. Pour plus d’informations, consultez le guide sur la création de [stratégies d’utilisation des données](../../../data-governance/policies/create.md) .

<!-- ## Create a new policy

To create a new policy, select the **[!UICONTROL Policies]** tab in the sidebar and select **[!UICONTROL Create Policy]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

The **[!UICONTROL Create a new policy]** dialog appears, prompting you to enter a name, and an optional description. When finished, select **[!UICONTROL Confirm]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Using the dropdown arrow select if you would like to **Permit access to** (![flac-permit-access-to](../../images/flac-ui/flac-permit-access-to.png)) a resource or **Deny access to** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) a resource.

Next, select the resource that you would like to include in the policy using the dropdown menu and search access type, read or write.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Next, using the dropdown arrow select the condition you would like to apply to this policy, **The following being true** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) or **The following being false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Select the plus icon to **Add matches expression** or **Add expression group** for the resource. 

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Using the dropdown, select the **Resource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Next, using the dropdown select the **Matches**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Next, using the dropdown, select the type of label (**[!UICONTROL Core label]** or **[!UICONTROL Custom label]**) to match the label assigned to the User in roles.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Finally, select the **Sandbox** that you would like the policy conditions to apply to, using the dropdown menu.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Select **Add resource** to add more resources. Once finished, select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The new policy is successfully created, and you are redirected to the **[!UICONTROL Policies]** tab, where you will see the newly created policy appear in the list. 

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Edit a policy

To edit an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to the policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select edit from the dropdown.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

The policy permissions screen appears. Make the updates then select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The policy is successfully updated, and you are redirected to the **[!UICONTROL Policies]** tab.

## Duplicate a policy

To duplicate an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select duplicate from the dropdown.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

The **[!UICONTROL Duplicate policy]** dialog appears, prompting you to confirm the duplication. 

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

The new policy appears in the list as a copy of the original on the **[!UICONTROL Policies]** tab.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Delete a policy

To delete an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to delete.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select delete from the dropdown.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

The **[!UICONTROL Delete user policy]** dialog appears, prompting you to confirm the deletion. 

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

You are returned to the **[!UICONTROL policies]** tab and a confirmation of deletion pop over appears.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png) -->

## Configuration d’une stratégie pour un environnement de test

>[!IMPORTANT]
>
>Par défaut, la fonction [!UICONTROL Inclusion automatique] est activée pour tous les clients, ce qui signifie que tous les environnements de test sont ajoutés à la stratégie.

>[!NOTE]
>
>La stratégie **[!UICONTROL Default-Label-Based-Access-Control-Policy]** est actuellement la seule disponible pour la configuration.

Pour afficher les environnements de test associés à une stratégie, sélectionnez la stratégie dans l’onglet **[!UICONTROL Stratégies]** .

![Page Stratégies présentant la liste des stratégies existantes disponibles.](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Sélectionnez ensuite la stratégie, puis l’onglet **[!UICONTROL Sandbox]** . Une liste des environnements de test associés à la stratégie s’affiche.

![Page Stratégies présentant la liste des stratégies existantes disponibles.](../../images/flac-ui/abac-policies-sandboxes-tab.png)

### Ajouter une stratégie à tous les environnements de test

Utilisez la bascule **[!UICONTROL Auto-include]** de l’onglet **[!UICONTROL Sandbox]** pour activer la stratégie pour tous les environnements de test.

![Onglet [!UICONTROL Sandbox] présentant le bouton d’activation/désactivation [!UICONTROL Auto-include].](../../images/flac-ui/abac-policies-auto-include.png)

La boîte de dialogue **[!UICONTROL Activer l’inclusion automatique]** s’affiche et vous invite à confirmer votre sélection. Sélectionnez **[!UICONTROL Activer]** pour terminer le paramètre de configuration.

![ La boîte de dialogue [!UICONTROL Activer l’inclusion automatique] surlignant [!UICONTROL Activer].](../../images/flac-ui/abac-policies-auto-include-enable.png)

>[!SUCCESS]
>
>La stratégie est activée pour tous les environnements de test existants et sera automatiquement ajoutée à tous les nouveaux environnements de test lorsqu’ils seront disponibles.

### Ajouter une stratégie pour sélectionner des environnements de test

>[!IMPORTANT]
>
>Les futurs environnements de test ne seront pas inclus par défaut dans la stratégie si le bouton d’inclusion automatique [!UICONTROL  est désactivé. ] Vous devrez gérer et ajouter manuellement des environnements de test à la stratégie.

Utilisez la bascule **[!UICONTROL Auto-include]** de l’onglet **[!UICONTROL Sandbox]** pour désactiver la stratégie pour tous les environnements de test.

![Onglet [!UICONTROL Sandbox] présentant le bouton d’activation/désactivation [!UICONTROL Auto-include].](../../images/flac-ui/abac-policies-auto-include.png)

Dans l’onglet **[!UICONTROL Sandbox]** , sélectionnez **[!UICONTROL Ajouter des sandbox]** pour sélectionner les environnements de test auxquels cette stratégie s’appliquera.

![Onglet [!UICONTROL Sandbox] présentant une liste d’environnements de test ajoutés à la stratégie.](../../images/flac-ui/abac-policies-sandboxes-tab-add.png)

Une liste des environnements de test s’affiche. Sélectionnez l’environnement de test à ajouter dans la liste. Vous pouvez également utiliser la barre de recherche pour rechercher l’environnement de test. Sélectionnez **[!UICONTROL Enregistrer]**.

![La page [!UICONTROL Ajouter des environnements de test] qui affiche la liste des environnements de test existants à ajouter à la stratégie.](../../images/flac-ui/abac-policies-sandboxes-list.png)

>[!SUCCESS]
>
>Les environnements de test sélectionnés ont bien été ajoutés à la stratégie.

### Suppression d’environnements de test d’une stratégie

Pour supprimer un environnement de test, sélectionnez l’icône **X** en regard du nom de l’environnement de test.

![L’onglet [!UICONTROL Environnements de test] présentant une liste d’environnements de test, mettant en surbrillance le [!UICONTROL X] à supprimer.](../../images/flac-ui/abac-policies-remove-sandbox-x.png)

La boîte de dialogue **[!UICONTROL Supprimer]** s’affiche et vous invite à confirmer votre sélection. Sélectionnez **[!UICONTROL Confirmer]** pour terminer la suppression.

![ La boîte de dialogue [!UICONTROL Supprimer] surlignant [!UICONTROL Confirmer].](../../images/flac-ui/abac-policies-remove-sandbox.png)

>[!SUCCESS]
>
>L’environnement de test sélectionné a été supprimé de la stratégie.

## Activer une politique

Pour activer une stratégie existante, sélectionnez-la dans l’onglet **[!UICONTROL Stratégies]** .

![flac-policy-select](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Sélectionnez ensuite les points de suspension (`…`) à côté du nom des politiques, et une liste déroulante affiche les contrôles permettant de modifier, désactiver, supprimer ou dupliquer le rôle. Sélectionnez Activer dans la liste déroulante.

![flac-policy-activate](../../images/abac-end-to-end-user-guide/abac-policies-activate.png)

La boîte de dialogue **[!UICONTROL Activer la stratégie]** s’affiche et vous invite à confirmer l’activation.

![flac-policy-activate-confirm](../../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)


Vous revenez alors à l’onglet **[!UICONTROL Politiques]** et une fenêtre contextuelle de confirmation de l’activation s’affiche. Le statut de la politique s’affiche comme actif.

![flac-policy-activated](../../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

## Étapes suivantes

Une fois qu’une stratégie est activée, vous pouvez passer à l’étape suivante : [gérer les autorisations pour un rôle](permissions.md).

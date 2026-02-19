---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des politiques de contrôle d’accès
description: Gérez les politiques de contrôle d’accès via l’interface Autorisations dans Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: b0094920720c54990953f79de32ab95c2a5c7e1c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 12%

---

# Gestion des politiques de contrôle d’accès

Les politiques de contrôle d’accès sont des instructions qui rassemblent des attributs pour établir des actions admissibles et non admissibles. Adobe fournit une politique par défaut qui peut être activée immédiatement ou lorsque votre organisation est prête à commencer à contrôler l’accès à des objets spécifiques en fonction de [&#x200B; libellés &#x200B;](./labels.md){target="_blank"}. La politique par défaut, **[!UICONTROL Default-Label-Based-Access-Control-Policy]**, utilise les libellés appliqués aux ressources pour refuser l’accès à moins que les utilisateurs et utilisatrices ne soient dans un rôle avec un libellé correspondant.

>[!IMPORTANT]
>
>Les politiques de contrôle d’accès ne doivent pas être confondues avec les politiques d’utilisation des données, qui contrôlent la manière dont les données sont utilisées dans Adobe Experience Platform. Pour plus d’informations, consultez le guide sur la création de [politiques d’utilisation des données](../../../data-governance/policies/create.md){target="_blank"}.

## Configuration de la politique d’un sandbox {#configure-policy}

>[!NOTE]
>
>La politique **[!UICONTROL Default-Label-Based-Access-Control-Policy]** est actuellement la seule disponible pour configuration.

Pour commencer à configurer une politique, accédez à **[!UICONTROL Permissions]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Sélectionnez **[!UICONTROL Policies]** dans le panneau de gauche. Sélectionnez le **[!UICONTROL Default-Label-Based-Access-Control-Policy]** dans la liste.

![Espace de travail Politiques affichant une liste des politiques existantes.](../../images/ui/policies/policies-home.png){zoomable="yes"}

L’espace de travail Détails de la politique s’affiche. Sélectionnez le **[!UICONTROL Sandboxes]**. Une liste des sandbox associés à la politique s’affiche.

![Espace de travail du sandbox de la politique présentant une liste des sandbox associés.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Ajouter une politique à tous les sandbox {#add-policy-to-all}

>[!IMPORTANT]
>
>Par défaut, **[!UICONTROL Auto-include]** est activé, ce qui signifie que tous les sandbox actuels et futurs sont automatiquement ajoutés à la politique.

Désactivez la fonction **[!UICONTROL Auto-include]** pour empêcher l’ajout automatique de futurs sandbox à la politique. Le fait de désactiver la fonctionnalité **ne supprime pas** les sandbox de la politique.

![Onglet Sandbox de la politique avec le bouton (bascule) Inclusion automatique mis en surbrillance et à l’état « désactivé ».](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Si **[!UICONTROL Auto-include]** n’est pas actif dans une politique, vous pouvez réactiver à l’aide du bouton (bascule). La boîte de dialogue **[!UICONTROL Enable Auto-include]** s’affiche et vous invite à confirmer votre sélection. Sélectionnez **[!UICONTROL Enable]** pour terminer la configuration.

>[!NOTE]
>
>Tous les sandbox que vous avez supprimés de la politique lors de la désactivation de **[!UICONTROL Auto-include]** seront ajoutés à nouveau.

![Boîte de dialogue Activer l’inclusion automatique avec l’option Activer mise en surbrillance.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Sélection manuelle de sandbox pour une politique {#manually-select-sandboxes}

Pour ajouter ou supprimer manuellement des sandbox à une politique, le bouton (bascule) **[!UICONTROL Auto-include]** **doit** doit être désactivé.

#### Ajouter des sandbox

Pour ajouter des sandbox à une politique, sélectionnez **[!UICONTROL Add Sandboxes]**.

![Espace de travail de la politique avec l’option Ajouter des sandbox mise en surbrillance.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

La boîte de dialogue **[!UICONTROL Add Sandboxes]** s’affiche. Sélectionnez le ou les sandbox à ajouter à la politique, puis sélectionnez **[!UICONTROL Save]**.

![La boîte de dialogue Ajouter des sandbox avec un sandbox sélectionné et l’option Enregistrer mise en surbrillance.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Si tous les sandbox disponibles sont déjà ajoutés à la politique, un message « Vous n’avez rien dans votre bibliothèque » s’affiche dans la boîte de dialogue.

#### Supprimer des sandbox

Pour supprimer des sandbox d’une politique, recherchez le sandbox à supprimer de la liste, puis sélectionnez l’icône **X**.

![Liste sandbox de la politique avec un « x » en surbrillance pour supprimer un sandbox.](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

Une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer la suppression du sandbox de la politique.

![Boîte de dialogue de confirmation de sandbox avec l’option Confirmer mise en surbrillance.](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## Activer une politique {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Que sont les politiques ?"
>abstract="Les politiques sont des déclarations qui réunissent des attributs pour établir des actions autorisées et non autorisées. Chaque organisation s’accompagne d’une politique par défaut que vous devez activer pour commencer à contrôler l’accès à des objets spécifiques en fonction de libellés. Les libellés appliqués aux ressources refusent l’accès à moins qu’un rôle avec un libellé correspondant ne soient affecté aux utilisateurs et utilisatrices. Les politiques ne peuvent pas être modifiées ni supprimées, mais elles peuvent être activées ou désactivées."
>additional-url="https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Gérer les libellés"

Pour activer une politique existante, sélectionnez-la dans l’onglet **[!UICONTROL Policies]** de **[!UICONTROL Permissions]**. Le statut d’activation de la politique est visible sous la section **[!UICONTROL Status]** .

![Espace de travail Politiques avec le statut d’une politique en surbrillance.](../../images/ui/policies/policy-status.png){zoomable="yes"}

L’espace de travail des détails de la politique s’affiche. Sélectionnez **[!UICONTROL Activate]**.

![Espace de travail détaillé de la politique avec l’option Activer mise en surbrillance.](../../images/ui/policies/policy-activate.png){zoomable="yes"}

La boîte de dialogue **[!UICONTROL Activate Policy]** s’affiche. Sélectionnez **[!UICONTROL Confirm]** pour terminer l’activation de la politique.

![La boîte de dialogue Activer la politique avec l’option Confirmer mise en surbrillance.](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## Étapes suivantes

Une fois la politique activée, vous pouvez passer à l’étape suivante pour [gérer les autorisations pour un rôle](permissions.md).

<!--Policies are applied at the sandbox level to control which sandboxes enforce label-based access control. By default, the **[!UICONTROL Auto-include]** feature is turned on, which means all current and future sandboxes are automatically added to the policy. When **[!UICONTROL Auto-include]** is turned off, only the sandboxes you manually add will be subject to the policy's access control rules.

To begin configuring a policy's sandboxes, navigate to **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Select **[!UICONTROL Policies]** from the left panel, then select the **[!UICONTROL Default-Label-Based-Access-Control-Policy]** from the list.

The policy's details workspace appears. Select the **[!UICONTROL Sandboxes]** tab to view the list of sandboxes associated with the policy and access the sandbox configuration options.

### Manage Auto-include {#manage-auto-include}

To control which sandboxes are included in a policy, you can toggle the **[!UICONTROL Auto-include]** feature on or off. When you toggle off **[!UICONTROL Auto-include]**, future sandboxes will not be automatically added to the policy. However, toggling off the feature **will not** remove any sandboxes that are already included in the policy.

To re-enable **[!UICONTROL Auto-include]**, use the toggle to turn it back on. The **[!UICONTROL Enable Auto-include]** dialog appears prompting you to confirm your selection. Select **[!UICONTROL Enable]** to complete the configuration setting.

>[!NOTE]
>
>When you re-enable **[!UICONTROL Auto-include]**, any sandboxes you previously removed from the policy will be re-added.

### Manually manage sandboxes {#manually-manage-sandboxes}

When **[!UICONTROL Auto-include]**is turned off, you can manually add or remove specific sandboxes from the policy. This gives you precise control over which sandboxes enforce the policy's access control rules.

>[!NOTE]
>
>To manually add or remove sandboxes, the **[!UICONTROL Auto-include]** toggle **must** be off.

**To add sandboxes:**

Select **[!UICONTROL Add Sandboxes]** from the policy's sandbox workspace.

The **[!UICONTROL Add Sandboxes]** dialog appears, displaying your library of available sandboxes. Select the sandbox(es) you wish to add to the policy and then select **[!UICONTROL Save]**.

>[!NOTE]
>
>If all available sandboxes are already included in the policy, you will see a "You have nothing in your library" message within the dialog.

**To remove sandboxes:**

Find the sandbox you wish to remove from the list and select the **X** icon next to its name.

A confirmation dialog will appear. Select **[!UICONTROL Confirm]** to finish removing the sandbox from the policy.

-->
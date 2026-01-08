---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;ABAC
title: Gestion des politiques de contrôle d’accès
description: Gérez les politiques de contrôle d’accès via l’interface Autorisations dans Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 10%

---

# Gestion des politiques de contrôle d’accès

Les politiques de contrôle d’accès sont des instructions qui rassemblent des attributs pour établir des actions admissibles et non admissibles. Adobe fournit une politique par défaut qui peut être activée immédiatement ou lorsque votre organisation est prête à commencer à contrôler l’accès à des objets spécifiques en fonction de [&#x200B; libellés &#x200B;](./labels.md){target="_blank"}. La politique par défaut, **[!UICONTROL Default-Label-Based-Access-Control-Policy]**, utilise les libellés appliqués aux ressources pour refuser l’accès à moins que les utilisateurs et utilisatrices ne soient dans un rôle avec un libellé correspondant.

>[!IMPORTANT]
>
>Les politiques de contrôle d’accès ne doivent pas être confondues avec les politiques d’utilisation des données, qui contrôlent la manière dont les données sont utilisées dans Adobe Experience Platform. Pour plus d’informations, consultez le guide sur la création de [politiques d’utilisation des données](../../../data-governance/policies/create.md){target="_blank"}.

## Configuration des sandbox pour une politique {#configure-policy}

Les politiques sont appliquées au niveau du sandbox pour contrôler quels sandbox appliquent le contrôle d’accès basé sur les libellés. Par défaut, la fonction **[!UICONTROL Auto-include]** est activée, ce qui signifie que tous les sandbox actuels et futurs sont automatiquement ajoutés à la politique. Lorsque **[!UICONTROL Auto-include]** est désactivé, seuls les sandbox que vous ajoutez manuellement sont soumis aux règles de contrôle d’accès de la politique.

>[!NOTE]
>
>La politique **[!UICONTROL Default-Label-Based-Access-Control-Policy]** est actuellement la seule disponible pour configuration.

Pour configurer les sandbox d’une politique, accédez à **[!UICONTROL Permissions]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Sélectionnez **[!UICONTROL Policies]** dans le panneau de gauche, puis sélectionnez le **[!UICONTROL Default-Label-Based-Access-Control-Policy]** dans la liste.

![Espace de travail Politiques affichant une liste des politiques existantes.](../../images/ui/policies/policies-home.png){zoomable="yes"}

L’espace de travail Détails de la politique s’affiche. Sélectionnez l’onglet **[!UICONTROL Sandboxes]** pour afficher la liste des sandbox associés à la politique et accéder aux options de configuration des sandbox.

![Espace de travail du sandbox de la politique présentant une liste des sandbox associés.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Gérer l’inclusion automatique {#manage-auto-include}

>[!IMPORTANT]
>
>Par défaut, **[!UICONTROL Auto-include]** est activé, ce qui signifie que tous les sandbox actuels et futurs sont automatiquement ajoutés à la politique.

Pour contrôler quels sandbox sont inclus dans une politique, vous pouvez activer ou désactiver la fonction **[!UICONTROL Auto-include]**. Lorsque vous désactivez cette option, **[!UICONTROL Auto-include]** sandbox futurs ne sont pas automatiquement ajoutés à la politique. Toutefois, le fait de désactiver la fonctionnalité **ne supprime pas** les sandbox déjà inclus dans la politique.

![Onglet Sandbox de la politique avec le bouton (bascule) Inclusion automatique mis en surbrillance et à l’état « désactivé ».](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Pour réactiver le **[!UICONTROL Auto-include]**, utilisez le bouton (bascule) pour le réactiver. La boîte de dialogue **[!UICONTROL Enable Auto-include]** s’affiche et vous invite à confirmer votre sélection. Sélectionnez **[!UICONTROL Enable]** pour terminer la configuration.

>[!NOTE]
>
>Lorsque vous réactivez **[!UICONTROL Auto-include]**, tous les sandbox que vous avez précédemment supprimés de la politique sont à nouveau ajoutés.

![Boîte de dialogue Activer l’inclusion automatique avec l’option Activer mise en surbrillance.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Gestion manuelle des sandbox {#manually-manage-sandboxes}

Lorsque l’option **[!UICONTROL Auto-include]** est désactivée, vous pouvez ajouter ou supprimer manuellement des sandbox spécifiques de la politique. Vous avez ainsi un contrôle précis sur les sandbox qui appliquent les règles de contrôle d’accès de la politique.

>[!NOTE]
>
>Pour ajouter ou supprimer manuellement des sandbox, le bouton (bascule) **[!UICONTROL Auto-include]** **doit** doit être désactivé.

**Pour ajouter des sandbox :**

Sélectionnez **[!UICONTROL Add Sandboxes]** dans l’espace de travail Sandbox de la politique.

![Espace de travail de la politique avec l’option Ajouter des sandbox mise en surbrillance.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

La boîte de dialogue **[!UICONTROL Add Sandboxes]** s’affiche, affichant votre bibliothèque de sandbox disponibles. Sélectionnez le ou les sandbox à ajouter à la politique, puis sélectionnez **[!UICONTROL Save]**.

![La boîte de dialogue Ajouter des sandbox avec un sandbox sélectionné et l’option Enregistrer mise en surbrillance.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Si tous les sandbox disponibles sont déjà inclus dans la politique, un message « Vous n’avez rien dans votre bibliothèque » s’affiche dans la boîte de dialogue.

**Pour supprimer des sandbox :**

Recherchez le sandbox à supprimer de la liste et sélectionnez l’icône **X** en regard de son nom.

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

---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;
title: Guide complet du contrôle d’accès basé sur les attributs
description: Ce document fournit un guide complet sur le contrôle d’accès basé sur les attributs dans Adobe Experience Platform
role: Developer
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 12%

---

# Guide complet du contrôle d’accès basé sur les attributs

Utilisez le contrôle d’accès basé sur les attributs sur Adobe Experience Platform pour vous offrir, ainsi qu’aux autres clients soucieux de la confidentialité des marques, une plus grande flexibilité en matière de gestion de l’accès utilisateur. L’accès à des objets individuels, tels que des champs de schéma et des audiences, peut être accordé avec des politiques basées sur les attributs et le rôle de l’objet. Cette fonctionnalité vous permet d’accorder ou de révoquer l’accès à des objets individuels pour des utilisateurs Experience Platform spécifiques au sein de votre organisation.

Cette fonctionnalité vous permet de classer les champs de schéma, les audiences, etc. avec des libellés qui définissent l’utilisation de l’organisation ou des données. Vous pouvez appliquer les mêmes libellés aux parcours, aux offres et aux autres objets dans Adobe Journey Optimizer. En parallèle, les administrateurs peuvent définir des politiques d’accès relatives aux champs de schéma du modèle de données d’expérience (XDM) et mieux gérer les utilisateurs ou les groupes (utilisateurs internes, externes ou tiers) pouvant accéder à ces champs.

>[!NOTE]
>
>Ce document se concentre sur le cas d’utilisation des politiques de contrôle d’accès. Si vous tentez de configurer des politiques pour régir l’**utilisation** des données plutôt que de déterminer à qui les utilisateurs d’Experience Platform ont accès, consultez plutôt le guide complet sur la [gouvernance des données](../../data-governance/e2e.md) .

## Commencer

Ce tutoriel nécessite une connaissance pratique des composants Experience Platform suivants :

* [[!DNL Experience Data Model (XDM)] Système](../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [Service de segmentation Adobe Experience Platform](../../segmentation/home.md) : moteur de segmentation de [!DNL Experience Platform] utilisé pour créer des segments d’audience à partir de vos profils clients en fonction du comportement et des attributs des clients.

### Présentation du cas d’utilisation

Vous allez passer en revue un exemple de workflow de contrôle d’accès basé sur les attributs dans lequel vous allez créer et attribuer des rôles, des libellés et des politiques afin de configurer si vos utilisateurs peuvent ou non accéder à des ressources spécifiques de votre organisation. Ce guide utilise un exemple de restriction de l’accès aux données sensibles pour démontrer le workflow. Ce cas d’utilisation est décrit ci-dessous :

Vous êtes un prestataire de soins de santé et souhaitez configurer l’accès aux ressources de votre entreprise.

* Votre équipe de marketing interne devrait pouvoir accéder aux données **[!UICONTROL ISP/données réglementées en matière de santé]**.
* Votre organisme externe ne devrait pas être en mesure d&#39;accéder aux données **[!UICONTROL ISP/données réglementées en matière de santé]**.

Pour ce faire, vous devez configurer des rôles, des ressources et des politiques.

Tu pourras :

* [Étiqueter les rôles pour vos utilisateurs](#label-roles) : utilisez l&#39;exemple d&#39;un fournisseur de soins de santé (ACME Business Group) dont le groupe marketing travaille avec des agences externes.
* [Étiqueter vos ressources (champs et audiences de schéma)](#label-resources) : attribuez le libellé **[!UICONTROL ISP/Données de santé réglementées]** aux ressources et audiences de schéma.
* [Activer la politique qui les liera](#policy) : activez la politique par défaut pour empêcher l’accès aux champs de schéma et aux audiences en connectant les libellés de vos ressources aux libellés de votre rôle. Les utilisateurs avec les libellés correspondants auront alors accès au champ et au segment du schéma dans tous les sandbox.

## Autorisations

[!UICONTROL Autorisations] est la zone d’Experience Cloud dans laquelle les administrateurs peuvent définir des rôles utilisateur et des politiques afin de gérer les autorisations pour les fonctionnalités et objets d’une application de produit.

Grâce aux [!UICONTROL autorisations], vous pouvez créer et gérer des rôles et attribuer les autorisations de ressources souhaitées pour ces rôles. Les [!UICONTROL autorisations] vous permettent également de gérer les libellés, les sandbox et les utilisateurs associés à un rôle spécifique.

Contactez votre administrateur système pour obtenir l’accès si vous ne disposez pas des privilèges d’administrateur.

Une fois que vous disposez des privilèges d’administrateur, accédez à [Adobe Experience Cloud](https://experience.adobe.com/) et connectez-vous à l’aide de vos informations d’identification Adobe. Une fois la connexion effectuée, la page **[!UICONTROL Aperçu]** s’affiche pour l’organisation pour laquelle vous disposez de droits d’administrateur. Cette page affiche les produits auxquels votre organisation est abonnée, ainsi que d’autres contrôles permettant d’ajouter des utilisateurs et des administrateurs à l’organisation. Sélectionnez **[!UICONTROL Autorisations]** pour ouvrir l’espace de travail en vue de votre intégration Experience Platform.

![Image illustrant le produit Autorisations sélectionné dans Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

L’espace de travail Autorisations de l’interface utilisateur d’Experience Platform s’affiche, s’ouvrant sur la page **[!UICONTROL Aperçu]**.

## Appliquer des libellés à un rôle {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Que sont les libellés ?"
>abstract="Utilisez les libellés pour classer et consulter les jeux de données et les champs en fonction des politiques d’utilisation qui s’appliquent à ces données. Adobe Experience Platform fournit plusieurs libellés d’utilisation des données <strong>de base</strong> définis par Adobe, qui couvrent un large éventail de restrictions courantes applicables à la gouvernance des données. Les libellés <strong>S</strong> (Sensibles) tels que DSR (données réglementées en matière de santé) servent à catégoriser les données qui font référence aux informations de santé protégées (ISP). Vous pouvez également définir vos propres libellés personnalisés en fonction des besoins de votre entreprise."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=fr#understanding-data-usage-labels" text="Présentation des libellés d’utilisation des données"

Les rôles sont des moyens de classer les types d’utilisateurs interagissant avec votre instance Experience Platform et sont des blocs élémentaires des politiques de contrôle d’accès. Un rôle possède un jeu d’autorisations déterminé et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès dont ils ont besoin.

Pour commencer, sélectionnez **[!UICONTROL Rôles]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Entité professionnelle ACME]**.

![Image montrant l’entité professionnelle ACME sélectionnée dans Rôles](../images/abac-end-to-end-user-guide/abac-select-role.png)

Sélectionnez ensuite **[!UICONTROL Libellés]** puis sélectionnez **[!UICONTROL Ajouter des libellés]**.

![Image illustrant la sélection de l’option Ajouter des libellés dans l’onglet Libellés ](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Une liste de tous les libellés de votre organisation s’affiche. Sélectionnez **[!UICONTROL RHD]** pour ajouter l’étiquette pour **[!UICONTROL ISP/données réglementées en matière de santé]** puis sélectionnez **[!UICONTROL Enregistrer]**.

![Image illustrant le libellé RHD sélectionné et enregistré](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Lors de l’ajout d’un groupe d’organisations à un rôle, tous les utilisateurs de ce groupe seront ajoutés au rôle. Toute modification apportée au groupe d’organisations (utilisateurs supprimés ou ajoutés) sera automatiquement mise à jour dans le rôle.

## Application de libellés aux champs de schéma {#label-resources}

Maintenant que vous avez configuré un rôle d’utilisateur avec le libellé [!UICONTROL RHD], l’étape suivante consiste à ajouter ce même libellé aux ressources que vous souhaitez contrôler pour ce rôle.

Dans le volet de navigation supérieur, sélectionnez le **sélecteur d’applications**, représenté par l’icône ![sélecteur d’applications](/help/images/icons/apps.png), puis sélectionnez **[!UICONTROL Experience Platform]**.

![Image montrant la sélection d’Experience Platform dans le menu déroulant du sélecteur d’applications](../images/abac-end-to-end-user-guide/abac-select-experience-platform.png)

Sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL ACME Healthcare]** dans la liste des schémas qui s’affichent.

![Image illustrant le schéma ACME Healthcare sélectionné dans l’onglet Schémas ](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Sélectionnez ensuite **[!UICONTROL Libellés]** pour afficher une liste qui affiche les champs associés à votre schéma. À partir de là, vous pouvez attribuer des libellés à un ou plusieurs champs à la fois. Sélectionnez les champs **[!UICONTROL Glucose sanguin]** et **[!UICONTROL Niveau d’insuline]**, puis sélectionnez **[!UICONTROL Appliquer l’accès et les étiquettes de gouvernance des données]**.

![Image montrant les valeurs Glycémie et Niveau d’insuline sélectionnés et appliquant l’accès et les étiquettes de gouvernance des données sélectionnées](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

La boîte de dialogue **[!UICONTROL Modifier les libellés]** s’affiche et vous permet de choisir les libellés à appliquer aux champs du schéma. Pour ce cas d’utilisation, sélectionnez l’étiquette **[!UICONTROL ISP/données réglementées en matière de santé]** puis sélectionnez **[!UICONTROL Enregistrer]**.

![Image illustrant le libellé RHD sélectionné et enregistré](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Lorsqu’un libellé est ajouté à un champ, il est appliqué à la ressource parent de ce champ (une classe ou un groupe de champs). Si la classe parent ou le groupe de champs est utilisé par d’autres schémas, ces schémas hériteront du même libellé.

## Application de libellés aux audiences

>[!NOTE]
>
>Toute audience qui utilise un attribut étiqueté doit également être étiquetée si vous souhaitez lui appliquer les mêmes restrictions d’accès.

Une fois que vous avez terminé d’étiqueter vos champs de schéma, vous pouvez commencer à étiqueter vos audiences.

Sélectionnez **[!UICONTROL Audiences]** dans le volet de navigation de gauche, sous la section **[!UICONTROL Clients]**. Une liste des audiences disponibles dans votre organisation s’affiche. Dans cet exemple, les deux audiences suivantes doivent être étiquetées , car elles contiennent des données d’intégrité sensibles :

* Glycémie >100
* Insuline &lt; 50

Sélectionnez **[!UICONTROL Glucose sanguin > 100]** (en fonction du nom de l’audience et non de la case à cocher) pour commencer à libeller l’audience.

![Image montrant la glycémie >100 sélectionnée dans l’onglet Audiences](../images/abac-end-to-end-user-guide/abac-select-audience.png)

L’écran **[!UICONTROL Détails]** du segment s’affiche. Sélectionnez **[!UICONTROL Gérer l’accès]**.

![Image illustrant la sélection de Gère l’accès](../images/abac-end-to-end-user-guide/abac-audience-fields-manage-access.png)

La boîte de dialogue **[!UICONTROL Appliquer l’accès et les libellés de gouvernance des données]** s’affiche et vous permet de choisir les libellés à appliquer à l’audience. Pour ce cas d’utilisation, sélectionnez l’étiquette **[!UICONTROL ISP/données réglementées en matière de santé]** puis sélectionnez **[!UICONTROL Enregistrer]**.

![Image montrant la sélection du libellé RHD et l’enregistrement sélectionné](../images/abac-end-to-end-user-guide/abac-select-audience-labels.png)

Répétez les étapes ci-dessus avec **[!UICONTROL Insuline &lt;50]**.

>[!NOTE]
>
> Attribuez les libellés créés dans l’espace de travail [!UICONTROL Autorisations] (comme les libellés de segment ci-dessus) à divers objets dans Adobe Journey Optimizer à l’aide de [Contrôle d’accès au niveau de l’objet](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/access-control/object-based-access). »

## Activer la politique de contrôle d’accès {#policy}

La politique de contrôle d’accès par défaut utilise des libellés pour définir les rôles utilisateur ayant accès à des ressources Experience Platform spécifiques. Dans cet exemple, l’accès aux champs de schéma et aux audiences sera refusé dans tous les sandbox pour les utilisateurs qui ne disposent pas d’un rôle avec les libellés correspondants dans le champ de schéma.

Pour activer la politique de contrôle d’accès, sélectionnez [!UICONTROL Autorisations] dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Politiques]**.

![ Liste des politiques affichées ](../images/abac-end-to-end-user-guide/abac-policies-page.png)

Sélectionnez ensuite les points de suspension (`...`) à côté du **[!UICONTROL Default-Field-Level-Access-Control-Policy]**. Une liste déroulante affiche alors les commandes permettant de modifier, activer, supprimer ou dupliquer le rôle. Sélectionnez **[!UICONTROL Activer]** dans la liste déroulante.

![Liste déroulante pour activer la politique](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

La boîte de dialogue Activer la politique s’affiche et vous invite à confirmer l’activation. Sélectionnez **[!UICONTROL Confirmer]**.

![Activer la boîte de dialogue Politique](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

Une confirmation d’activation de la politique est reçue et vous revenez à la page [!UICONTROL Politiques].

![Activer la confirmation de politique](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=fr" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=fr#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=fr#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Experience Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.
a
To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Experience Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Étapes suivantes

Vous avez terminé l’application des libellés à un rôle, des champs de schéma et des audiences. L’agence externe affectée à ces rôles ne peut pas afficher ces libellés et leurs valeurs dans la vue schéma, jeu de données et profil. L’utilisation de ces champs est également limitée dans la définition de segment lors de l’utilisation du créateur de segments.

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](./overview.md).

La vidéo suivante est destinée à vous aider à comprendre le contrôle d’accès basé sur les attributs et explique comment configurer des rôles, des ressources et des politiques.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)

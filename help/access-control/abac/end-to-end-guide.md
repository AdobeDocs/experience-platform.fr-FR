---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;
title: Guide de bout en bout du contrôle d’accès basé sur les attributs
description: Ce document fournit un guide de bout en bout sur le contrôle d’accès basé sur les attributs dans Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: f7a8f9a5eb0ef3c961f9524057ff01564f88dec3
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 7%

---

# Guide de bout en bout du contrôle d’accès basé sur les attributs

Le contrôle d’accès basé sur les attributs est une fonctionnalité de Adobe Experience Platform qui offre une plus grande flexibilité aux marques soucieuses de la confidentialité pour gérer l’accès des utilisateurs. Les objets individuels tels que les champs de schéma et les segments peuvent être affectés à des rôles utilisateur. Cette fonctionnalité vous permet d’accorder ou de révoquer l’accès à des objets individuels pour des utilisateurs de Platform spécifiques de votre entreprise.

Cette fonctionnalité vous permet de classer les champs de schéma, les segments, etc. avec des libellés qui définissent les portées d’utilisation des données ou de l’organisation. Dans Adobe Journey Optimizer, vous pouvez appliquer ces mêmes étiquettes aux parcours et aux offres. En parallèle, les administrateurs peuvent définir des stratégies d’accès concernant les champs de schéma XDM et mieux gérer les utilisateurs ou les groupes (utilisateurs internes, externes ou tiers) pouvant accéder à ces champs.

## Prise en main

Ce tutoriel nécessite une connaissance pratique des composants Platform suivants :

* [[!DNL Experience Data Model (XDM)] Système](../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [Service de segmentation Adobe Experience Platform](../../segmentation/home.md) : moteur de segmentation de [!DNL Platform] utilisé pour créer des segments d’audience à partir de vos profils clients en fonction du comportement et des attributs des clients.

### Présentation du cas d’utilisation

Ce guide utilise un exemple de cas pratique de limitation de l’accès aux données sensibles pour démontrer le workflow. Vous accédez à un exemple de workflow de contrôle d’accès basé sur les attributs dans lequel vous allez créer et affecter des rôles, des libellés et des stratégies afin de configurer si vos utilisateurs peuvent ou non accéder à certaines ressources de votre organisation. Ce cas pratique est décrit ci-dessous :

Vous êtes un prestataire de santé et vous souhaitez configurer l’accès aux ressources de votre entreprise.

* Votre équipe marketing interne doit pouvoir accéder à **[!UICONTROL PHI/Données d’intégrité réglementées]** data.
* Votre agence externe ne doit pas pouvoir accéder à **[!UICONTROL PHI/Données d’intégrité réglementées]** data.

Pour ce faire, vous devez configurer les rôles, les ressources et les stratégies.

Vous allez :

* [Étiqueter les rôles de vos utilisateurs]{#label-roles}: Utilisez l’exemple d’un prestataire de santé (ACME Business Group) dont le groupe marketing travaille avec des agences externes.
* [Étiqueter vos ressources (champs de schéma et segments)]{#label-resources}: Attribuez le **[!UICONTROL PHI/Données d’intégrité réglementées]** libellé aux ressources de schéma et aux segments.
* [Créez la stratégie qui les reliera.]{#policy}: Créez une stratégie pour lier les libellés de vos ressources aux libellés de votre rôle qui refusent l’accès aux champs de schéma et aux segments. Cela refusera l’accès au champ de schéma et au segment dans tous les environnements de test pour les utilisateurs qui n’ont pas de libellés correspondants.

## Autorisations

[!UICONTROL La zone dédiée aux autorisations dans Experience Cloud permet aux administrateurs de définir des rôles d’utilisateur et des stratégies d’accès. Ils peuvent ainsi gérer les autorisations d’accès aux fonctionnalités et objets dans une application de produit.]

Via [!UICONTROL Autorisations], vous pouvez créer et gérer des rôles, ainsi qu’affecter les autorisations de ressources souhaitées pour ces rôles. [!UICONTROL Les autorisations vous permettent également de gérer les libellés, les sandbox et les utilisateurs associés à un rôle spécifique.]

Si vous ne disposez pas de droits d’administrateur, contactez votre administrateur système pour obtenir l’accès.

Une fois que vous disposez des droits d’administrateur, accédez à [Adobe Experience Cloud](https://experience.adobe.com/) et connectez-vous à l’aide de vos informations d’identification d’Adobe. Une fois connecté, l’événement **[!UICONTROL Présentation]** s’affiche pour votre organisation pour laquelle vous disposez des droits d’administrateur. Cette page présente les produits auxquels votre organisation est abonnée, ainsi que d’autres contrôles permettant d’ajouter des utilisateurs et des administrateurs à l’organisation dans son ensemble. Sélectionner **[!UICONTROL Autorisations]** pour ouvrir l’espace de travail de votre intégration Platform.

![Image montrant le produit Autorisations sélectionné dans Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

L’espace de travail Autorisations de l’interface utilisateur de Platform s’affiche, s’ouvrant sur la fenêtre **[!UICONTROL Rôles]** page.

## Application d’étiquettes à un rôle {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Que sont les étiquettes ?"
>abstract="Les libellés vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Platform fournit plusieurs libellés d’utilisation des données &quot;de base&quot; définis par l’Adobe, qui couvrent un large éventail de restrictions courantes applicables à la gouvernance des données. Par exemple, les étiquettes Sensibles &quot;S&quot; telles que RHD (données d’intégrité réglementées) vous permettent de catégoriser les données qui font référence aux informations d’intégrité protégées (PHI). Vous pouvez également définir vos propres étiquettes personnalisées qui répondent aux besoins de votre entreprise."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="Présentation des libellés d’utilisation des données"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Créer un libellé"
>abstract="Vous pouvez créer vos propres étiquettes personnalisées en fonction des besoins de votre entreprise. Les étiquettes personnalisées peuvent être utilisées pour appliquer à vos données des configurations de gouvernance des données et de contrôle d’accès."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="Gestion des libellés personnalisés"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Quels sont les rôles ?"
>abstract="Les rôles sont des moyens de catégoriser les types d’utilisateurs qui interagissent avec votre instance Platform et sont des blocs élémentaires des stratégies de contrôle d’accès. Un rôle possède un ensemble donné d’autorisations et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="Gestion des rôles"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Créer un nouveau rôle"
>abstract="Vous pouvez créer un nouveau rôle pour mieux classer les utilisateurs qui accèdent à votre instance Platform. Par exemple, vous pouvez créer un rôle pour une équipe de marketing interne et appliquer le libellé du RHD à ce rôle, ce qui permettra à votre équipe de marketing interne d’accéder aux informations d’intégrité protégées (PHI). Vous pouvez également créer un rôle pour une agence externe et refuser l’accès à ce rôle aux données d’identification personnelle en n’appliquant pas le libellé du RHD à ce rôle."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="Création d’un rôle"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Présentation des rôles"
>abstract="La boîte de dialogue de présentation des rôles affiche les ressources et les environnements de test auxquels un rôle donné est autorisé à accéder."

Les rôles sont des moyens de catégoriser les types d’utilisateurs qui interagissent avec votre instance Platform et sont des blocs élémentaires des stratégies de contrôle d’accès. Un rôle possède un ensemble donné d’autorisations et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès dont ils ont besoin.

Pour commencer, sélectionnez **[!UICONTROL ACME Business Group]** de la **[!UICONTROL Rôles]** page.

![Image montrant le rôle métier ACME sélectionné dans les rôles](../images/abac-end-to-end-user-guide/abac-select-role.png)

Ensuite, sélectionnez **[!UICONTROL Étiquettes]** puis sélectionnez **[!UICONTROL Ajouter des étiquettes]**.

![Image affichant l’option Ajouter des libellés sélectionnée dans l’onglet Étiquettes](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Une liste de tous les libellés de votre organisation s’affiche. Sélectionner **[!UICONTROL RHD]** pour ajouter le libellé de **[!UICONTROL PHI/Données d’intégrité réglementées]**. Autoriser l’affichage d’une coche bleue en regard du libellé pendant quelques instants, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Image montrant l&#39;étiquette du disque dur en cours de sélection et d&#39;enregistrement](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

## Application de libellés aux champs de schéma {#label-resources}

Maintenant que vous avez configuré un rôle d’utilisateur avec la fonction [!UICONTROL RHD] , l’étape suivante consiste à ajouter le même libellé aux ressources que vous souhaitez contrôler pour ce rôle.

Sélectionner **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL ACME Health Care]** dans la liste des schémas qui s’affichent.

![Image montrant le schéma ACME Health care sélectionné dans l’onglet Schémas](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Ensuite, sélectionnez **[!UICONTROL Étiquettes]** pour afficher une liste qui affiche les champs associés à votre schéma. À partir de là, vous pouvez attribuer des étiquettes à un ou plusieurs champs à la fois. Sélectionnez la **[!UICONTROL BloodGluglucose]** et **[!UICONTROL InsulinLevel]** puis sélectionnez **[!UICONTROL Modification des étiquettes de gouvernance]**.

![Image montrant BloodGluglucose et InsulinLevel sélectionnés et les étiquettes de gouvernance de modification sélectionnées](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

Le **[!UICONTROL Modifier les libellés]** s’affiche, vous permettant de choisir les libellés à appliquer aux champs du schéma. Pour ce cas pratique, sélectionnez la variable **[!UICONTROL PHI/Données d’intégrité réglementées]** libellé, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Image montrant l&#39;étiquette du disque dur en cours de sélection et d&#39;enregistrement](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Lorsqu’un libellé est ajouté à un champ, il est appliqué à la ressource parent de ce champ (une classe ou un groupe de champs). Si la classe ou le groupe de champs parent est utilisé par d’autres schémas, ces derniers hériteront du même libellé.

## Application d’étiquettes aux segments

Une fois que vous avez terminé l’étiquetage de vos champs de schéma, vous pouvez commencer à les libeller.

Sélectionner **[!UICONTROL Segments]** dans le volet de navigation de gauche. Une liste des segments disponibles dans votre organisation s’affiche. Dans cet exemple, les deux segments suivants doivent être étiquetés, car ils contiennent des données d’intégrité sensibles :

* Glucide sanguin > 100
* Insuline &lt;50

Sélectionner **[!UICONTROL Glucide sanguin > 100]** pour commencer à libeller le segment.

![Image montrant le glucose dans le sang >100 sélectionné depuis l’onglet Segments](../images/abac-end-to-end-user-guide/abac-select-segment.png)

Le segment **[!UICONTROL Détails]** s’affiche. Sélectionner **[!UICONTROL Gérer l’accès]**.

![Image montrant la sélection de l’accès Manages](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

Le **[!UICONTROL Modifier les libellés]** s’affiche, vous permettant de choisir les libellés à appliquer au segment. Pour ce cas pratique, sélectionnez la variable **[!UICONTROL PHI/Données d’intégrité réglementées]** libellé, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Image montrant la sélection du libellé RHD et de l&#39;enregistrement sélectionné](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Répétez les étapes ci-dessus avec **[!UICONTROL Insuline &lt;50]**.

## Création d’une stratégie de contrôle d’accès {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Que sont les politiques ?"
>abstract="Les politiques sont des déclarations qui réunissent des attributs pour établir des actions permises et non admissibles. Chaque organisation s’accompagne d’une stratégie par défaut que vous devez activer afin de définir des règles pour les ressources telles que les segments et les champs de schéma. Les stratégies par défaut ne peuvent pas être modifiées ni supprimées. Toutefois, les stratégies par défaut peuvent être activées ou désactivées."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Gestion des stratégies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Création d’une stratégie"
>abstract="Créez une stratégie pour définir les actions que vos utilisateurs peuvent ou ne peuvent pas entreprendre par rapport à vos segments et champs de schéma."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Création d’une stratégie"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configuration des actions autorisées et non autorisées pour une stratégie"
>abstract="Sélectionnez Autoriser l’accès à pour configurer les actions autorisées que vos utilisateurs peuvent effectuer par rapport aux ressources. Sélectionnez Refuser l’accès à pour configurer les actions non autorisées que vos utilisateurs ne peuvent pas effectuer par rapport aux ressources."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Modification d’une stratégie"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configuration des autorisations pour une ressource"
>abstract="Une ressource est la ressource ou l’objet auquel un utilisateur peut ou ne peut pas accéder. Les ressources peuvent être des segments ou des schémas. Vous pouvez configurer des autorisations d’écriture, de lecture ou de suppression pour les segments et les champs de schéma."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Editer les conditions"
>abstract="Appliquez des instructions conditionnelles à votre stratégie pour configurer l’accès des utilisateurs à certaines ressources. Sélectionnez l’option Correspondre à tous pour exiger des utilisateurs qu’ils possèdent les mêmes libellés qu’une ressource pour pouvoir y accéder. Sélectionnez l’option Faire correspondre n’importe lequel pour exiger uniquement que les utilisateurs disposent d’un rôle avec un seul libellé correspondant à une ressource. Les libellés peuvent être définis comme des libellés principaux ou personnalisés, avec des libellés principaux représentant les libellés créés et fournis par des libellés d’Adobe et personnalisés représentant les libellés que vous avez créés pour votre organisation."

Les stratégies de contrôle d’accès utilisent des étiquettes pour définir les rôles utilisateur ayant accès à des ressources Platform spécifiques. Les stratégies peuvent être locales ou globales et peuvent remplacer d’autres stratégies. Dans cet exemple, l’accès aux champs de schéma et aux segments sera refusé dans tous les environnements de test pour les utilisateurs qui ne disposent pas des libellés correspondants dans le champ de schéma.

Pour créer une stratégie de contrôle d’accès, sélectionnez **[!UICONTROL Autorisations]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Stratégies]**. Ensuite, sélectionnez **[!UICONTROL Création d’une stratégie]**.

![Image montrant l’option Créer une stratégie sélectionnée dans les autorisations](../images/abac-end-to-end-user-guide/abac-create-policy.png)

Le **[!UICONTROL Création d’une stratégie]** s’affiche, vous invitant à saisir un nom et une description facultative. Sélectionner **[!UICONTROL Confirmer]** lorsque vous avez terminé.

![Image de la boîte de dialogue Créer une nouvelle stratégie et de la sélection de l’option Confirmer](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

Pour refuser l’accès aux champs du schéma, utilisez la flèche de liste déroulante et sélectionnez **[!UICONTROL Refuser l’accès à]** puis sélectionnez **[!UICONTROL Aucune ressource sélectionnée]**. Ensuite, sélectionnez **[!UICONTROL Champ de schéma]** puis sélectionnez **[!UICONTROL Tous]**.

![Image montrant Refuser l’accès et les ressources sélectionnées](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

Le tableau ci-dessous présente les conditions disponibles lors de la création d’une stratégie :

| Conditions | Description |
| --- | --- |
| Les éléments suivants sont faux : | Lorsque l’option &quot;Refuser l’accès à&quot; est définie, l’accès est restreint si l’utilisateur ne répond pas aux critères sélectionnés. |
| La valeur suivante est vraie : | Lorsque &quot;Autoriser l’accès à&quot; est défini, l’accès est autorisé si l’utilisateur répond aux critères sélectionnés. |
| Correspond à n’importe quel | L’utilisateur dispose d’un libellé correspondant à n’importe quel libellé appliqué à une ressource. |
| Correspond à tous les | L’utilisateur dispose de toutes les étiquettes qui correspondent à toutes les étiquettes appliquées à une ressource. |
| Libellé principal | Un libellé principal est un libellé défini par Adobe disponible dans toutes les instances Platform. |
| Libellé personnalisé | Une étiquette personnalisée est une étiquette qui a été créée par votre organisation. |

Sélectionner **[!UICONTROL Les éléments suivants sont faux :]** puis sélectionnez **[!UICONTROL Aucun attribut sélectionné]**. Sélectionnez ensuite l’utilisateur **[!UICONTROL Libellé principal]**, puis sélectionnez **[!UICONTROL Correspond à tous les]**. Sélectionner la ressource **[!UICONTROL Libellé principal]** et enfin sélectionner **[!UICONTROL Ajouter une ressource]**.

![Image montrant les conditions sélectionnées et Ajouter la ressource sélectionnée](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>Une ressource est la ressource ou l’objet auquel un sujet peut ou ne peut pas accéder. Les ressources peuvent être des segments ou des schémas.

Pour refuser l’accès aux segments, utilisez la flèche de liste déroulante et sélectionnez **[!UICONTROL Refuser l’accès à]** puis sélectionnez **[!UICONTROL Aucune ressource sélectionnée]**. Ensuite, sélectionnez **[!UICONTROL Segment]** puis sélectionnez **[!UICONTROL Tous]**.

Sélectionner **[!UICONTROL Les éléments suivants sont faux :]** puis sélectionnez **[!UICONTROL Aucun attribut sélectionné]**. Sélectionnez ensuite l’utilisateur **[!UICONTROL Libellé principal]**, puis sélectionnez **[!UICONTROL Correspond à tous les]**. Sélectionner la ressource **[!UICONTROL Libellé principal]** et enfin sélectionner **[!UICONTROL Enregistrer]**.

![Image montrant les conditions sélectionnées et Enregistrer en cours de sélection](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Sélectionner **[!UICONTROL Activer]** pour activer la stratégie, une boîte de dialogue s’affiche, vous invitant à confirmer l’activation. Sélectionner **[!UICONTROL Confirmer]** puis sélectionnez **[!UICONTROL Fermer]**.

![Image montrant la stratégie en cours d’activation ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## Étapes suivantes

Vous avez terminé l’application des libellés à un rôle, à des champs de schéma et à des segments. L’agence externe affectée à ces rôles ne peut pas afficher ces libellés et leurs valeurs dans le schéma, le jeu de données et la vue de profil. Ces champs ne peuvent pas non plus être utilisés dans la définition de segment lors de l’utilisation du créateur de segments.

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](./overview.md).

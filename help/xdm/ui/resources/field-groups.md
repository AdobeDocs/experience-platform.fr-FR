---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;groupe de champs;groupes de champs;
solution: Experience Platform
title: Création et modification de groupes de champs de schéma dans l’interface utilisateur
description: Découvrez comment créer et modifier des groupes de champs de schéma dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 716250b8bcfa1b2d9c868aa80b3122da401553b9
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Création et modification de groupes de champs de schéma dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), les groupes de champs de schéma sont des composants réutilisables qui définissent un ou plusieurs champs qui implémentent certaines fonctions, telles que les détails personnels, les préférences de l’hôtel ou l’adresse. Les groupes de champs sont destinés à être inclus dans le cadre d’un schéma qui met en oeuvre une classe compatible.

Un groupe de champs définit la ou les classes avec lesquelles il est compatible, en fonction du comportement des données représentées par le groupe de champs (enregistrement ou série temporelle). Cela signifie que tous les groupes de champs ne sont pas disponibles pour toutes les classes.

Adobe Experience Platform fournit de nombreux groupes de champs standard qui couvrent un large éventail de cas d’utilisation marketing. Cependant, vous pouvez également créer et modifier vos propres groupes de champs personnalisés pour définir des concepts supplémentaires liés à votre entreprise dans vos schémas XDM. Ce guide explique comment créer, modifier et gérer des groupes de champs personnalisés pour votre organisation dans l’interface utilisateur de Platform.

## Conditions préalables

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la section [Présentation de XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform, et de [principes de base de la composition des schémas](../../schema/composition.md) pour savoir comment les groupes de champs contribuent aux schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les différentes capacités de la fonction [!DNL Schema Editor].

## Créer un groupe de champs {#create}

Pour créer un nouveau groupe de champs, vous devez d’abord sélectionner un schéma auquel le groupe de champs sera ajouté. Vous pouvez choisir de [créer un nouveau schéma](./schemas.md#create) ou [sélectionner un schéma existant à modifier ;](./schemas.md#edit).

Une fois que le schéma est ouvert dans le [!DNL Schema Editor], sélectionnez **[!UICONTROL Ajouter]** en regard de [!UICONTROL Groupes de champs] dans le rail de gauche.

![](../../images/ui/resources/field-groups/add-field-group.png)

Une boîte de dialogue s’affiche, affichant une liste des groupes de champs existants pour votre organisation. Dans la partie supérieure de la boîte de dialogue, sélectionnez **[!UICONTROL Créer un groupe de champs]**. Vous pouvez fournir ici un **[!UICONTROL Nom d’affichage]** et **[!UICONTROL Description]** pour le groupe de champs. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Ajouter un groupe de champs]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

Le [!DNL Schema Editor] réapparaît, avec le nouveau groupe de champs répertorié dans le rail de gauche. Puisqu’il s’agit d’un nouveau groupe de champs, il ne fournit actuellement aucun champ au schéma et le canevas reste donc inchangé. Vous pouvez maintenant commencer. [ajout de champs au groupe de champs](#add-fields).

## Modifier un groupe de champs existant {#edit}

>[!NOTE]
>
>Seuls les groupes de champs personnalisés définis par votre organisation peuvent être entièrement modifiés et personnalisés. Pour les groupes de champs principaux définis par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte de schémas individuels. Voir la section sur [modification des noms d’affichage des champs de schéma](./schemas.md#display-names) pour plus d’informations.
>
>Une fois qu’un groupe de champs personnalisé a été enregistré et utilisé dans un schéma pour l’ingestion de données, seules des modifications supplémentaires peuvent être apportées par la suite au groupe de champs. Voir [règles d’évolution des schémas](../../schema/composition.md#evolution) pour plus d’informations.

Pour modifier un groupe de champs existant, vous devez d’abord ouvrir un schéma qui utilise le groupe de champs dans le [!DNL Schema Editor]. Vous pouvez [sélectionner un schéma existant à modifier ;](./schemas.md#edit), ou vous pouvez [créer un nouveau schéma](./schemas.md#create) et ajoutez le groupe de champs en question.

Une fois le schéma ouvert dans l’éditeur, vous pouvez commencer. [ajout de champs au groupe de champs](#add-fields).

## Ajouter des champs à un groupe de champs {#add-fields}

>[!NOTE]
>
>Cette section porte sur l’ajout de champs à des groupes de champs personnalisés. Pour plus d’informations sur l’ajout de champs personnalisés à des groupes de champs standard, reportez-vous à la section [guide de l’interface utilisateur des schémas](./schemas.md#custom-fields-for-standard-groups).

Pour ajouter des champs à un groupe de champs personnalisé dans le [!DNL Schema Editor], sélectionnez tout d’abord le nom du groupe de champs dans le rail de gauche, puis sélectionnez la variable **plus (+)** en regard du nom du schéma dans la zone de travail.

![](../../images/ui/resources/field-groups/add-field.png)

A **[!UICONTROL Nouveau champ]** apparaît dans la zone de travail et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Consultez le guide sur la [définition des champs dans l’interface utilisateur](../fields/overview.md#define) pour connaître les étapes spécifiques à la configuration et à l’ajout du champ au groupe de champs.

Continuez à ajouter autant de champs que nécessaire au groupe de champs. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et le groupe de champs.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Si le même groupe de champs est déjà utilisé dans d&#39;autres schémas, les champs nouvellement ajoutés apparaîtront automatiquement dans ces schémas.

## Étapes suivantes

Ce guide explique comment créer et modifier des groupes de champs à l’aide de l’interface utilisateur de Platform. Pour plus d’informations sur les fonctionnalités de la variable [!UICONTROL Schémas] workspace, voir [[!UICONTROL Schémas] présentation de workspace](../overview.md).

Pour savoir comment gérer des groupes de champs à l’aide du [!DNL Schema Registry] API, voir [guide d’entrée des groupes de champs](../../api/field-groups.md).

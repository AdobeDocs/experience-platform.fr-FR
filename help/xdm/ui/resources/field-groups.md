---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;XDM system;experience data model;ui;workspace;field group;field groups;
solution: Experience Platform
title: Création et modification de groupes de champs de Schéma dans l’interface utilisateur
description: Découvrez comment créer et modifier des groupes de champs de schéma dans l’interface utilisateur de l’Experience Platform.
topic: Guide de l’utilisateur
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---


# Création et modification de groupes de champs de schéma dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), les groupes de champs de schéma sont des composants réutilisables qui définissent un ou plusieurs champs qui implémentent certaines fonctions telles que les détails personnels, les préférences de l’hôtel ou l’adresse. Les groupes de champs doivent être inclus dans un schéma qui met en oeuvre une classe compatible.

Un groupe de champs définit la ou les classes avec lesquelles il est compatible, en fonction du comportement des données que le groupe de champs représente (enregistrement ou série chronologique). Cela signifie que tous les groupes de champs ne sont pas disponibles pour toutes les classes.

Adobe Experience Platform fournit de nombreux groupes de champs standard qui couvrent un large éventail de cas d’utilisation marketing. Cependant, vous pouvez également créer et modifier vos propres groupes de champs personnalisés pour définir des concepts supplémentaires liés à votre entreprise dans vos schémas XDM. Ce guide présente un aperçu de la manière de créer, de modifier et de gérer des groupes de champs personnalisés pour votre organisation dans l’interface utilisateur de la plate-forme.

## Conditions préalables  

Ce guide nécessite une bonne compréhension de XDM System. Pour une présentation du rôle de XDM dans l&#39;écosystème Experience Platform, voir [Présentation de XDM](../../home.md) et les [bases de la composition du schéma](../../schema/composition.md) pour savoir comment les groupes de champs contribuent aux schémas de XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur [la composition d&#39;un schéma dans l&#39;interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les diverses fonctionnalités du [!DNL Schema Editor].

## Créer un groupe de champs {#create}

Pour créer un groupe de champs, vous devez d’abord sélectionner un schéma auquel le groupe de champs sera ajouté. Vous pouvez choisir de [créer un nouveau schéma](./schemas.md#create) ou [sélectionner un schéma existant à modifier](./schemas.md#edit).

Une fois le schéma ouvert dans [!DNL Schema Editor], sélectionnez **[!UICONTROL Ajouter]** en regard de la section [!UICONTROL Groupes de champs] dans le rail de gauche.

![](../../images/ui/resources/field-groups/add-field-group.png)

Une boîte de dialogue s’affiche, présentant la liste des groupes de champs existants pour votre organisation. Près du haut de la boîte de dialogue, sélectionnez **[!UICONTROL Créer un nouveau groupe de champs]**. Vous pouvez fournir ici **[!UICONTROL Nom d’affichage]** et **[!UICONTROL Description]** pour le groupe de champs. Une fois terminé, sélectionnez **[!UICONTROL Ajouter le groupe de champs]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

Le [!DNL Schema Editor] réapparaît, avec le nouveau groupe de champs répertorié dans le rail de gauche. Comme il s’agit d’un nouveau groupe de champs, il ne fournit actuellement aucun champ au schéma et le canevas reste donc inchangé. Vous pouvez désormais début [l&#39;ajout de champs au groupe de champs](#add-fields).

## Modifier un groupe de champs existant {#edit}

>[!NOTE]
>
>Seuls les groupes de champs personnalisés définis par votre organisation peuvent être entièrement modifiés et personnalisés. Pour les groupes de champs principaux définis par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte de schémas individuels. Pour plus d&#39;informations, consultez la section [modification des noms d&#39;affichage pour les champs de schéma](./schemas.md#display-names).
>
>Une fois qu’un groupe de champs personnalisé a été enregistré et utilisé dans un schéma pour l’assimilation de données, seules des modifications supplémentaires peuvent être apportées au groupe de champs par la suite. Pour plus d&#39;informations, consultez les [règles d&#39;évolution des schémas](../../schema/composition.md#evolution).

Pour modifier un groupe de champs existant, vous devez d&#39;abord ouvrir un schéma qui utilise le groupe de champs dans [!DNL Schema Editor]. Vous pouvez [sélectionner un schéma existant à modifier](./schemas.md#edit) ou [créer un nouveau schéma](./schemas.md#create) et ajouter le groupe de champs en question.

Une fois le schéma ouvert dans l’éditeur, vous pouvez début [en ajoutant des champs au groupe de champs](#add-fields).

## Ajouter des champs à un groupe de champs {#add-fields}

Pour ajouter des champs à un groupe de champs dans le [!DNL Schema Editor], début en sélectionnant le nom du groupe de champs dans le rail de gauche, puis sélectionnez l&#39;icône **plus (+)** en regard du nom du schéma dans le canevas.

![](../../images/ui/resources/field-groups/add-field.png)

Un **[!UICONTROL nouveau champ]** apparaît dans le canevas et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Consultez le guide sur la [définition des champs dans l&#39;interface utilisateur](../fields/overview.md#define) pour connaître les étapes spécifiques de configuration et d&#39;ajout du champ au groupe de champs.

Continuez à ajouter autant de champs que nécessaire au groupe de champs. Une fois terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et le groupe de champs.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Si le même groupe de champs est déjà utilisé dans d’autres schémas, les champs nouvellement ajoutés s’affichent automatiquement dans ces schémas.

## Étapes suivantes

Ce guide explique comment créer et modifier des groupes de champs à l’aide de l’interface utilisateur de la plate-forme. Pour plus d&#39;informations sur les fonctionnalités de l&#39;espace de travail [!UICONTROL Schémas], consultez la présentation de l&#39;espace de travail [[!UICONTROL Schémas]](../overview.md).

Pour savoir comment gérer les groupes de champs à l&#39;aide de l&#39;API [!DNL Schema Registry], consultez le [guide du point de terminaison des groupes de champs](../../api/field-groups.md).
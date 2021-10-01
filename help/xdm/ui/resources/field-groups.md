---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;groupe de champs;groupes de champs;
solution: Experience Platform
title: Création et modification de groupes de champs de schéma dans l’interface utilisateur
description: Découvrez comment créer et modifier des groupes de champs de schéma dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Création et modification de groupes de champs de schéma dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), les groupes de champs de schéma sont des composants réutilisables qui définissent un ou plusieurs champs qui implémentent certaines fonctions, telles que les détails personnels, les préférences de l’hôtel ou l’adresse. Les groupes de champs sont destinés à être inclus dans le cadre d’un schéma qui met en oeuvre une classe compatible.

Un groupe de champs définit la ou les classes avec lesquelles il est compatible, en fonction du comportement des données représentées par le groupe de champs (enregistrement ou série temporelle). Cela signifie que tous les groupes de champs ne sont pas disponibles pour toutes les classes.

Adobe Experience Platform fournit de nombreux groupes de champs standard qui couvrent un large éventail de cas d’utilisation marketing. Cependant, vous pouvez également créer et modifier vos propres groupes de champs personnalisés pour définir des concepts supplémentaires liés à votre entreprise dans vos schémas XDM. Ce guide explique comment créer, modifier et gérer des groupes de champs personnalisés pour votre organisation dans l’interface utilisateur de Platform.

## Conditions préalables

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation de XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform et les [bases de la composition des schémas](../../schema/composition.md) pour la manière dont les groupes de champs contribuent aux schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur la [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) afin de vous familiariser avec les différentes fonctionnalités de [!DNL Schema Editor].

## Créer un groupe de champs {#create}

Pour créer un nouveau groupe de champs, vous devez d’abord sélectionner un schéma auquel le groupe de champs sera ajouté. Vous pouvez choisir de [créer un nouveau schéma](./schemas.md#create) ou [sélectionner un schéma existant à modifier](./schemas.md#edit).

Une fois le schéma ouvert dans la balise [!DNL Schema Editor], sélectionnez **[!UICONTROL Ajouter]** en regard de la section [!UICONTROL Groupes de champs] dans le rail de gauche.

![](../../images/ui/resources/field-groups/add-field-group.png)

Une boîte de dialogue s’affiche, affichant une liste des groupes de champs existants pour votre organisation. Près de la partie supérieure de la boîte de dialogue, sélectionnez **[!UICONTROL Créer un groupe de champs]**. Vous pouvez fournir ici **[!UICONTROL Nom d’affichage]** et **[!UICONTROL Description]** pour le groupe de champs. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Ajouter un groupe de champs]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

[!DNL Schema Editor] réapparaît, avec le nouveau groupe de champs répertorié dans le rail de gauche. Puisqu’il s’agit d’un nouveau groupe de champs, il ne fournit actuellement aucun champ au schéma et le canevas reste donc inchangé. Vous pouvez maintenant commencer [à ajouter des champs au groupe de champs](#add-fields).

## Modifier un groupe de champs existant {#edit}

>[!NOTE]
>
>Seuls les groupes de champs personnalisés définis par votre organisation peuvent être entièrement modifiés et personnalisés. Pour les groupes de champs principaux définis par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte de schémas individuels. Pour plus d’informations, reportez-vous à la section [Modification des noms d’affichage pour les champs de schéma](./schemas.md#display-names) .
>
>Une fois qu’un groupe de champs personnalisé a été enregistré et utilisé dans un schéma pour l’ingestion de données, seules des modifications supplémentaires peuvent être apportées par la suite au groupe de champs. Pour plus d’informations, consultez les [règles de l’évolution du schéma](../../schema/composition.md#evolution) .

Pour modifier un groupe de champs existant, vous devez d’abord ouvrir un schéma qui utilise le groupe de champs dans la balise [!DNL Schema Editor]. Vous pouvez [sélectionner un schéma existant à modifier](./schemas.md#edit), ou [créer un nouveau schéma](./schemas.md#create) et ajouter le groupe de champs en question.

Une fois le schéma ouvert dans l’éditeur, vous pouvez commencer [par ajouter des champs au groupe de champs](#add-fields).

## Ajouter des champs à un groupe de champs {#add-fields}

Pour ajouter des champs à un groupe de champs dans la balise [!DNL Schema Editor], commencez par sélectionner le nom du groupe de champs dans le rail de gauche, puis sélectionnez l’icône **plus (+)** en regard du nom du schéma dans la zone de travail.

![](../../images/ui/resources/field-groups/add-field.png)

Un **[!UICONTROL nouveau champ]** apparaît dans la zone de travail et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Consultez le guide sur la [définition des champs dans l’interface utilisateur](../fields/overview.md#define) pour connaître les étapes spécifiques à la configuration et à l’ajout du champ au groupe de champs.

Continuez à ajouter autant de champs que nécessaire au groupe de champs. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et le groupe de champs.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Si le même groupe de champs est déjà utilisé dans d&#39;autres schémas, les champs nouvellement ajoutés apparaîtront automatiquement dans ces schémas.

## Étapes suivantes

Ce guide explique comment créer et modifier des groupes de champs à l’aide de l’interface utilisateur de Platform. Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).

Pour savoir comment gérer les groupes de champs à l’aide de l’API [!DNL Schema Registry], consultez le [guide de point de terminaison des groupes de champs](../../api/field-groups.md).

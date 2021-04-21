---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;XDM system;experience data model;ui;workspace;mixin;mixins;
solution: Experience Platform
title: Création et modification de mixins dans l’interface utilisateur
description: Découvrez comment créer et modifier des mixins dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 240b857d-75ad-42fd-9249-050cbc5306a9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 5%

---

# Création et modification de mixins dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), les mixins sont des composants réutilisables qui définissent un ou plusieurs champs qui implémentent certaines fonctions telles que les détails personnels, les préférences de l’hôtel ou l’adresse. Les mixins sont destinés à être inclus dans le cadre d’un schéma qui met en œuvre une classe compatible.

Un mixin définit la ou les classes avec lesquelles il est compatible, en fonction du comportement des données que le mixin représente (enregistrement ou série chronologique). Cela signifie que tous les mixins ne peuvent pas être utilisés pour toutes les classes.

Adobe Experience Platform fournit de nombreux mixins standard qui couvrent un large éventail de cas d’utilisation marketing. Cependant, vous pouvez également créer et modifier vos propres mixins personnalisés pour définir des concepts supplémentaires liés à votre entreprise dans vos schémas XDM. Ce guide présente un aperçu de la manière de créer, modifier et gérer des mixins personnalisés pour votre organisation dans l’interface utilisateur de la plate-forme.

## Conditions préalables

Ce guide nécessite une bonne compréhension de XDM System. Pour une présentation du rôle de XDM dans l&#39;écosystème Experience Platform, voir [Présentation de XDM](../../home.md) et les [bases de la composition du schéma](../../schema/composition.md) pour savoir comment les mixins contribuent aux schémas de XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur [la composition d&#39;un schéma dans l&#39;interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les diverses fonctionnalités du [!DNL Schema Editor].

## Création d’un nouveau mixin {#create}

Pour créer un nouveau mixin, vous devez d’abord sélectionner un schéma auquel le mixin sera ajouté. Vous pouvez choisir de [créer un nouveau schéma](./schemas.md#create) ou [sélectionner un schéma existant à modifier](./schemas.md#edit).

Une fois le schéma ouvert dans [!DNL Schema Editor], sélectionnez **[!UICONTROL Ajouter]** en regard de la section [!UICONTROL Mixins] dans le rail de gauche.

![](../../images/ui/resources/mixins/add-mixin-button.png)

Une boîte de dialogue s’affiche, présentant une liste de mixins existants pour votre organisation. Près du haut de la boîte de dialogue, sélectionnez **[!UICONTROL Créer un nouveau mixin]**. Vous pouvez fournir ici **[!UICONTROL Nom d’affichage]** et **[!UICONTROL Description]** pour le mixin. Une fois terminé, sélectionnez **[!UICONTROL Ajouter le mixin]**.

![](../../images/ui/resources/mixins/create-mixin.png)

Le [!DNL Schema Editor] réapparaît, le nouveau mixin étant répertorié dans le rail de gauche. Comme il s’agit d’un tout nouveau mixin, il ne fournit actuellement aucun champ au schéma et la trame reste donc inchangée. Vous pouvez désormais début [l’ajout de champs au mixin](#add-fields).

## Modifier un mixin existant {#edit}

>[!NOTE]
>
>Seuls les mixins personnalisés définis par votre organisation peuvent être entièrement modifiés et personnalisés. Pour les mixins principaux définis par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte de schémas individuels. Pour plus d&#39;informations, consultez la section [modification des noms d&#39;affichage pour les champs de schéma](./schemas.md#display-names).
>
>Une fois qu&#39;un mixin personnalisé a été enregistré et utilisé dans un schéma pour l&#39;assimilation de données, seules des modifications additifs peuvent être apportées au mixin par la suite. Pour plus d&#39;informations, consultez les [règles d&#39;évolution des schémas](../../schema/composition.md#evolution).

Pour modifier un mixin existant, vous devez d’abord ouvrir un schéma qui utilise le mixin dans [!DNL Schema Editor]. Vous pouvez [sélectionner un schéma existant à modifier](./schemas.md#edit), ou [créer un nouveau schéma](./schemas.md#create) et ajouter le mixin en question.

Une fois le schéma ouvert dans l’éditeur, vous pouvez début [en ajoutant des champs au mixin](#add-fields).

## Ajouter des champs à un mixin {#add-fields}

Pour ajouter des champs à un mixin dans [!DNL Schema Editor], début en sélectionnant le nom du mixin dans le rail de gauche, puis sélectionnez l’icône **plus (+)** en regard du nom du schéma dans la trame.

![](../../images/ui/resources/mixins/add-field-button.png)

Un **[!UICONTROL nouveau champ]** apparaît dans le canevas et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Consultez le guide sur la [définition des champs dans l&#39;interface utilisateur](../fields/overview.md#define) pour connaître les étapes spécifiques de configuration et d&#39;ajout du champ au mixin.

Continuez à ajouter autant de champs que nécessaire au mixin. Une fois terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et le mixin.

![](../../images/ui/resources/mixins/complete-mixin.png)

Si le même mixin est déjà utilisé dans d’autres schémas, les champs nouvellement ajoutés apparaissent automatiquement dans ces schémas.

## Étapes suivantes

Ce guide explique comment créer et modifier des mixins à l’aide de l’interface utilisateur de la plate-forme. Pour plus d&#39;informations sur les fonctionnalités de l&#39;espace de travail [!UICONTROL Schémas], consultez la présentation de l&#39;espace de travail [[!UICONTROL Schémas]](../overview.md).

Pour savoir comment gérer les mixins à l&#39;aide de l&#39;API [!DNL Schema Registry], consultez le [guide des points de terminaison des mixins](../../api/mixins.md).

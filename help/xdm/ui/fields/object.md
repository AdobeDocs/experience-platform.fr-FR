---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;objet;champ;
solution: Experience Platform
title: Définition des champs d’objet dans l’interface utilisateur
description: Découvrez comment définir un champ de type objet dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Définition de champs d’objet dans l’interface utilisateur

Adobe Experience Platform vous permet de personnaliser entièrement la structure de vos classes XDM (Experience Data Model) personnalisées, de groupes de champs de schéma et de types de données. Pour organiser et imbriquer des champs associés dans des ressources XDM personnalisées, vous pouvez définir des champs de type objet pouvant contenir des sous-champs supplémentaires.

When [définition d’un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform, utilisez la méthode **[!UICONTROL Type]** , puis sélectionnez &quot;[!UICONTROL Objet]&quot; de la liste.

![](../../images/ui/fields/special/object.png)

Sélectionner **[!UICONTROL Appliquer]** pour ajouter l’objet au schéma. La zone de travail se met à jour pour afficher le nouveau champ avec la fonction [!UICONTROL Objet] type de données appliqué, y compris les contrôles pour modifier et ajouter des sous-champs à l’objet.

![](../../images/ui/fields/special/object-applied.png)

Pour ajouter un sous-champ, sélectionnez le champ **plus (+)** en regard du champ d’objet dans la zone de travail. Un nouveau champ s’affiche sous l’objet, avec des commandes permettant de configurer le sous-champ dans le rail de droite.

![](../../images/ui/fields/special/object-add-field.png)

Une fois que vous avez configuré le sous-champ et sélectionné **[!UICONTROL Appliquer]**, vous pouvez continuer à ajouter des champs à l’objet à l’aide du même processus. Vous pouvez également ajouter des sous-champs qui sont des objets eux-mêmes, ce qui vous permet d’imbriquer les champs aussi profondément que vous le souhaitez.

Une fois la construction de l’objet terminée, vous pouvez constater que vous souhaitez réutiliser sa structure dans différentes classes et groupes de champs. Dans ce cas, vous pouvez choisir de convertir l’objet en un type de données. Voir la section sur [conversion d’objets en types de données](../resources/data-types.md#convert) pour plus d’informations, voir le guide de l’interface utilisateur des types de données .

## Étapes suivantes

Ce guide explique comment définir un champ d’objet dans l’interface utilisateur. Consultez la présentation sur [définition des champs dans l’interface utilisateur](./overview.md#special) pour savoir comment définir d’autres types de champ XDM dans [!DNL Schema Editor].

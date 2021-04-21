---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;XDM system;experience data model;ui;workspace;object;field;
solution: Experience Platform
title: Définition des champs d’objet dans l’interface utilisateur
description: Découvrez comment définir un champ de type objet dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Définition des champs d’objet dans l’interface utilisateur

Adobe Experience Platform vous permet de personnaliser entièrement la structure de vos classes, mixins et types de données de modèle de données d’expérience (XDM) personnalisés. Pour organiser et imbriquer des champs associés dans des ressources XDM personnalisées, vous pouvez définir des champs de type objet qui peuvent contenir des sous-champs supplémentaires.

Lorsque [vous définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform, utilisez la liste déroulante **[!UICONTROL Type]** et sélectionnez &quot;[!UICONTROL Objet]&quot; dans la liste.

![](../../images/ui/fields/special/object.png)

Sélectionnez **[!UICONTROL Appliquer]** pour ajouter l’objet au schéma. Le canevas se met à jour pour afficher le nouveau champ avec le type de données [!UICONTROL Objet] appliqué, y compris les contrôles permettant de modifier et d&#39;ajouter des sous-champs à l&#39;objet.

![](../../images/ui/fields/special/object-applied.png)

Pour ajouter un sous-champ, sélectionnez l’icône **plus (+)** en regard du champ d’objet dans la trame. Un nouveau champ s’affiche sous l’objet, avec des commandes permettant de configurer le sous-champ dans le rail de droite.

![](../../images/ui/fields/special/object-add-field.png)

Une fois que vous avez configuré le sous-champ et sélectionné **[!UICONTROL Appliquer]**, vous pouvez continuer à ajouter des champs à l’objet à l’aide du même processus. Vous pouvez également ajouter des sous-champs qui sont des objets eux-mêmes, ce qui vous permet d’imbriquer des champs aussi profondément que vous le souhaitez.

![](../../images/ui/fields/special/object-nested.png)

Une fois la construction de l’objet terminée, vous pouvez réutiliser sa structure dans différentes classes et mixins. Dans ce cas, vous pouvez choisir de convertir l’objet en type de données. Pour plus d&#39;informations, consultez la section [conversion d&#39;objets en types de données](../resources/data-types.md#convert) du guide d&#39;interface utilisateur des types de données.

## Étapes suivantes

Ce guide explique comment définir un champ d’objet dans l’interface utilisateur. Consultez l&#39;aperçu sur [la définition des champs dans l&#39;interface utilisateur](./overview.md#special) pour savoir comment définir d&#39;autres types de champs XDM dans [!DNL Schema Editor].

---
keywords: Experience Platform ; interface utilisateur ; interface utilisateur ; tableaux de bord ; tableau de bord ; profils ; segments ; destinations ; utilisation de la licence
title: Utilisation de la bibliothèque de widgets pour Ajouter et créer des widgets de Tableau de bord
description: 'Ce guide fournit des instructions détaillées sur l’ajout de widgets standard et la création de widgets personnalisés pour la visualisation des données de tableau de bord dans Adobe Experience Platform. '
topic-legacy: guide
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 1%

---

# (bêta) Bibliothèque de widgets {#widget-library}

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez vue et interagir avec les données de votre entreprise à l’aide de plusieurs tableaux de bord. Vous pouvez également mettre à jour certains de ces tableaux de bord en ajoutant de nouveaux widgets à votre vue de tableau de bord. Outre les widgets standard fournis par Adobe, vous pouvez créer des widgets personnalisés et les partager dans toute votre organisation.

Ce guide fournit des instructions détaillées pour ajouter des widgets standard et créer des widgets personnalisés afin de personnaliser les informations affichées dans les tableaux de bord [!UICONTROL Profils] et [!UICONTROL Segments] de l&#39;interface utilisateur de la plate-forme.

Pour savoir comment modifier l&#39;emplacement et la taille des widgets dans les tableaux de bord [!UICONTROL Profils], [!UICONTROL Destinations] et [!UICONTROL Segments], consultez le [guide de modification des tableaux de bord](modify.md).

>[!NOTE]
>
>Les widgets affichés dans le tableau de bord [!UICONTROL Utilisation de la licence] ne peuvent pas être personnalisés. Pour en savoir plus sur ce tableau de bord unique, consultez la [documentation du tableau de bord d’utilisation des licences](guides/license-usage.md).

## Accès à la bibliothèque de widgets

Dans n’importe quel tableau de bord (par exemple, le tableau de bord Profils), vous pouvez sélectionner **[!UICONTROL Modifier le tableau de bord]** suivi de **[!UICONTROL Bibliothèque de widgets]** pour accéder à la bibliothèque de widgets.

>[!NOTE]
>
>Le bouton [!UICONTROL Bibliothèque de widgets] n&#39;apparaît qu&#39;une fois [!UICONTROL Modifier le tableau de bord] sélectionné.

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

La [!UICONTROL bibliothèque de widgets] contient deux onglets, [!UICONTROL Standard] et [!UICONTROL Personnalisé].

* L&#39;onglet **[!UICONTROL Standard]** contient des widgets créés par Adobe et vous permet de mettre à jour votre tableau de bord à l&#39;aide de ces mesures standard. Pour en savoir plus sur l&#39;ajout de widgets standard à votre tableau de bord, consultez la section [widgets standard](#standard-widgets) de ce guide.
* L&#39;onglet **[!UICONTROL Personnalisé]** vous permet de créer et de partager des widgets au sein de votre organisation. Pour obtenir des instructions complètes sur la création de vos propres widgets, consultez la section [widgets personnalisés](#custom-widgets) de ce guide.

![](images/customization/widget-library.png)

## Widgets standard {#standard-widgets}

L&#39;onglet **[!UICONTROL Standard]** contient des widgets créés par Adobe, ventilés en catégories. La sélection d’une catégorie affiche les widgets disponibles pour ce tableau de bord. Chaque widget s’affiche sous forme de carte, fournissant le titre, la description et un exemple de visualisation de la mesure.

>[!NOTE]
>
>Les widgets ne peuvent être ajoutés qu&#39;au tableau de bord correspondant à la catégorie sélectionnée. Par exemple, seuls les widgets de la catégorie [!UICONTROL Profils] peuvent être ajoutés au tableau de bord [!UICONTROL Profils].

![](images/customization/standard-widgets.png)

Pour choisir un widget standard à ajouter à votre tableau de bord, mettez le widget en surbrillance et cochez la case correspondante. Avec au moins un widget sélectionné, le bouton **[!UICONTROL Ajouter widget]** est illuminé.

>[!NOTE]
>
>Le compteur situé dans le coin supérieur droit de la bibliothèque de widgets affiche le nombre total de widgets sélectionnés.

Sélectionnez **[!UICONTROL Ajouter un widget]** pour ajouter les widgets sélectionnés à votre tableau de bord.

![](images/customization/add-widget.png)

## Widgets personnalisés {#custom-widgets}

>[!IMPORTANT]
>
>Votre organisation peut créer au maximum 20 widgets personnalisés dans la bibliothèque de widgets.

Pour personnaliser davantage l’aspect des tableaux de bord dans l’Experience Platform, vous pouvez créer des widgets et les partager avec d’autres utilisateurs de votre organisation. Dans la bibliothèque de widgets, sélectionnez l&#39;onglet **[!UICONTROL Personnalisé]** pour commencer à créer des widgets personnalisés. Dans l&#39;onglet [!UICONTROL Personnalisé], tous les widgets créés par votre organisation sont visibles. Dans cet exemple, aucun widget personnalisé n’a encore été créé.

![](images/customization/custom-widgets.png)

### Sélectionner des attributs

Pour créer des widgets personnalisés, les attributs de Profil client en temps réel doivent être identifiés afin de s’assurer que les données sont incluses dans l’instantané quotidien. Si votre organisation n’a sélectionné aucun attribut de Profil, le bouton [!UICONTROL Configurer le schéma] apparaît dans le coin supérieur droit de la bibliothèque de widgets.

Lorsqu’au moins un attribut personnalisé a été sélectionné, le bouton [!UICONTROL Modifier le schéma] s’affiche dans le coin supérieur droit de la bibliothèque de widgets. Sélectionnez **[!UICONTROL Modifier le schéma]** pour ouvrir la boîte de dialogue **[!UICONTROL Sélectionner le schéma d&#39;union]** pour vue les attributs sélectionnés et ajouter d&#39;autres attributs.

>[!IMPORTANT]
>
>Une organisation peut sélectionner un maximum de 20 attributs.

![](images/customization/edit-schema.png)

Pour sélectionner un attribut, accédez à l’attribut dans le schéma d’union (ou utilisez la recherche) et cochez la case en regard de l’attribut. La sélection de la case à cocher ajoute également l&#39;attribut à la liste **[!UICONTROL Attributs sélectionnés]** située sur le côté droit de la boîte de dialogue.

>[!NOTE]
>
>Pour qu’un attribut soit visible pour la sélection, il doit s’agir de l’un des éléments suivants : Chaîne, Date, Date-Heure, Boolean, Short, Long, Integer ou Byte. Les types de données de mappage et de Doublon ne sont pas pris en charge et sont grisés afin qu’ils ne puissent pas être sélectionnés.

Après avoir choisi les attributs à ajouter, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos attributs et revenir à l&#39;onglet widgets personnalisés.

Les attributs nouvellement sélectionnés sont disponibles après l&#39;instantané quotidien lors de l&#39;actualisation des données.

![](images/customization/select-attribute.png)

### Création d’un widget personnalisé

Pour créer un widget personnalisé, sélectionnez **[!UICONTROL Créer]** dans le centre de la bibliothèque de widgets ou si des widgets personnalisés ont déjà été créés, sélectionnez **[!UICONTROL Créer widget]** dans le coin supérieur droit de la bibliothèque de widgets.

![](images/customization/create-widget.png)

Dans la boîte de dialogue **[!UICONTROL Créer un widget]**, vous pouvez fournir un titre et une description pour votre nouveau widget et choisir l&#39;attribut que vous souhaitez que le widget affiche. Pour choisir un attribut, sélectionnez le bouton radio en regard de l’attribut à ajouter.

>[!NOTE]
>
>Un seul attribut peut être sélectionné par widget. En outre, si un widget a déjà été créé pour un attribut, celui-ci apparaît grisé.

![](images/customization/create-widget-dialog.png)

Une prévisualisation du nouveau widget s’affiche dans la boîte de dialogue, avec un graphique à barres horizontales contenant des données fictives.

>[!NOTE]
>
>La seule mesure actuellement prise en charge pour tous les attributs est le nombre de profils et la seule visualisation actuellement prise en charge pour les widgets personnalisés est un graphique à barres horizontales.
>
>Les données affichées dans l&#39;exemple de widget sont fournies à titre d&#39;illustration uniquement. La prévisualisation n’affiche pas les données réelles de votre organisation.

![](images/customization/create-widget-select-attribute.png)

Pour enregistrer votre nouveau widget et revenir à l&#39;onglet [!UICONTROL Personnalisé], sélectionnez **[!UICONTROL Créer]**. Votre nouveau widget peut désormais être ajouté à un tableau de bord en choisissant le widget dans la bibliothèque et en sélectionnant **[!UICONTROL Ajouter widget]**.

### Archivage d’un widget personnalisé

Une fois qu’un widget a été ajouté à la bibliothèque, il peut être archivé à l’aide du bouton **[!UICONTROL Archiver]**. Vous pouvez également modifier le widget pour mettre à jour les champs de titre ou de description.

## Étapes suivantes

Après avoir lu ce document, vous pouvez maintenant accéder à la [!UICONTROL bibliothèque de widgets] et l&#39;utiliser pour ajouter des widgets à un tableau de bord ou créer des widgets personnalisés pour votre organisation. Pour modifier la taille et l&#39;emplacement des widgets dans le tableau de bord, consultez le [guide de modification des tableaux de bord](modify.md).

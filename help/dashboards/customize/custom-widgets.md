---
keywords: Experience Platform;interface utilisateur;interface utilisateur;tableaux de bord;profils;segments;destinations;utilisation des licences;widgets;mesures
title: Création de widgets personnalisés pour les tableaux de bord
description: 'Ce guide fournit des instructions détaillées sur la création de widgets personnalisés à utiliser dans les tableaux de bord Adobe Experience Platform. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Création de widgets personnalisés pour les tableaux de bord

Dans Adobe Experience Platform, vous pouvez afficher et interagir avec les données de votre entreprise à l’aide de plusieurs tableaux de bord. Vous pouvez également mettre à jour certains tableaux de bord en ajoutant de nouveaux widgets à la vue de votre tableau de bord. Outre les widgets standard fournis par Adobe, vous pouvez créer des widgets personnalisés et les partager dans l’ensemble de votre organisation.

Ce guide fournit des instructions détaillées sur la création et l’ajout de widgets personnalisés aux tableaux de bord [!UICONTROL Profils], [!UICONTROL Segments] et [!UICONTROL Destinations] dans l’interface utilisateur de Platform.

Pour en savoir plus sur les widgets standard, reportez-vous au guide pour [ajouter des widgets standard à vos tableaux de bord](standard-widgets.md).

>[!NOTE]
>
>Les widgets affichés dans le tableau de bord [!UICONTROL Utilisation de la licence] ne peuvent pas être personnalisés. Pour en savoir plus sur ce tableau de bord unique, consultez la [documentation du tableau de bord d’utilisation des licences](../guides/license-usage.md).

## Bibliothèque de widgets {#widget-library}

Ce guide nécessite l’accès à la [!UICONTROL bibliothèque de widgets] dans Experience Platform. Pour en savoir plus sur la bibliothèque de widgets et sur la façon d’y accéder dans l’interface utilisateur, commencez par lire la [présentation de la bibliothèque de widgets](widget-library.md).

## Prise en main des widgets personnalisés

Dans la bibliothèque de widgets, l’onglet **[!UICONTROL Personnalisé]** vous permet de créer des widgets et de les partager avec d’autres utilisateurs de votre entreprise afin de personnaliser l’aspect de vos tableaux de bord.

>[!IMPORTANT]
>
>Votre entreprise peut créer 20 widgets personnalisés au maximum dans la bibliothèque de widgets.

Sélectionnez l’onglet **[!UICONTROL Personnalisé]** pour commencer à créer des widgets personnalisés ou pour afficher les widgets personnalisés déjà créés par votre entreprise.

![](../images/customization/custom-widgets.png)

## Création d’un widget personnalisé

Pour créer un widget personnalisé, sélectionnez **[!UICONTROL Créer]** dans le centre de la bibliothèque de widgets ou, si des widgets personnalisés ont déjà été créés, sélectionnez **[!UICONTROL Créer un widget]** dans le coin supérieur droit de la bibliothèque de widgets.

![](../images/customization/create-widget.png)

Dans la boîte de dialogue **[!UICONTROL Créer un widget]**, vous pouvez fournir un titre et une description pour votre nouveau widget et choisir l’attribut que vous souhaitez que le widget affiche.

>[!NOTE]
>
>La liste des attributs disponibles dépend du schéma configuré pour votre organisation. Pour en savoir plus sur la sélection d’attributs et la configuration de schéma, consultez le guide sur l’[édition du schéma afin de créer des widgets personnalisés](edit-schema.md).

Pour choisir un attribut, cliquez sur le bouton radio en regard de l’attribut que vous souhaitez ajouter.

>[!NOTE]
>
>Un seul attribut peut être sélectionné par widget un seul widget peut être créé par attribut. Si un widget a déjà été créé pour un attribut, l’attribut apparaît grisé.

![](../images/customization/create-widget-dialog.png)

## Aperçu d’un widget personnalisé

Un aperçu du nouveau widget s’affiche dans la boîte de dialogue, affichant un graphique en barres horizontal avec des données de simulation.

>[!NOTE]
>
>La seule mesure actuellement prise en charge pour tous les attributs est le nombre de profils et la seule visualisation actuellement prise en charge pour les widgets personnalisés est un graphique à barres horizontal.
>
>Les données affichées dans l’exemple de widget sont fournies à titre d’illustration uniquement. L’aperçu n’affiche pas les données réelles de votre entreprise.

![](../images/customization/create-widget-select-attribute.png)

Pour enregistrer votre nouveau widget et revenir à l’onglet [!UICONTROL Personnalisé], sélectionnez **[!UICONTROL Créer]**. Vous pouvez désormais ajouter votre nouveau widget à un tableau de bord en le sélectionnant dans la bibliothèque et en sélectionnant **[!UICONTROL Ajouter un widget]**.

## Archivage d’un widget personnalisé

Une fois qu’un widget a été ajouté à la bibliothèque, il peut être archivé à l’aide du bouton **[!UICONTROL Archiver]** . Vous pouvez également modifier le widget pour mettre à jour les champs de titre ou de description.

## Étapes suivantes

Après avoir lu ce document, vous pouvez accéder à la bibliothèque de widgets et l’utiliser pour créer et ajouter des widgets personnalisés pour votre organisation. Pour modifier la taille et l’emplacement des widgets qui apparaissent dans le tableau de bord, reportez-vous au [guide de modification des tableaux de bord](modify.md).

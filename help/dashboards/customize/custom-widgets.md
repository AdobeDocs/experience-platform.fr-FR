---
keywords: Experience Platform;interface utilisateur;interface utilisateur;tableaux de bord;profils;segments;destinations;utilisation des licences;widgets;mesures
title: Création de widgets personnalisés pour les tableaux de bord
description: 'Ce guide fournit des instructions détaillées sur la création de widgets personnalisés à utiliser dans les tableaux de bord Adobe Experience Platform. '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '902'
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

Pour créer un widget personnalisé, sélectionnez **[!UICONTROL Créer un widget]** dans le coin supérieur droit de la bibliothèque de widgets ou, s’il s’agit du premier widget personnalisé de votre entreprise, sélectionnez **[!UICONTROL Créer]** dans le centre de la bibliothèque de widgets.

![](../images/customization/create-widget.png)

Dans la boîte de dialogue **[!UICONTROL Créer un widget]**, fournissez un titre et une description pour votre nouveau widget et choisissez l’attribut que vous souhaitez que le widget affiche.

>[!NOTE]
>
>La liste des attributs disponibles dépend du schéma configuré pour votre organisation. Pour en savoir plus sur la sélection d’attributs et la configuration de schéma, consultez le guide sur l’[édition du schéma afin de créer des widgets personnalisés](edit-schema.md).

Pour choisir un attribut, cliquez sur le bouton radio en regard de l’attribut que vous souhaitez ajouter.

>[!NOTE]
>
>Un seul attribut peut être sélectionné par widget un seul widget peut être créé par attribut. Si un widget a déjà été créé pour un attribut, l’attribut apparaît grisé.

![](../images/customization/create-widget-dialog.png)

## Sélection d’une visualisation

Après avoir sélectionné un attribut, un aperçu du nouveau widget s’affiche dans la boîte de dialogue. L’intelligence artificielle permet de sélectionner automatiquement une visualisation qui correspond le mieux aux données d’attribut et de fournir des options de visualisation supplémentaires que vous pouvez sélectionner manuellement.

Selon l’attribut , l’IA recommande différentes options de visualisation. La liste complète des visualisations comprend :

* Graphique à barres horizontal : Les lignes horizontales sont utilisées pour représenter des valeurs.
* Graphique à barres vertical : Les lignes verticales sont utilisées pour représenter des valeurs.
* Graphique en anneau : Comme pour un graphique circulaire, les valeurs s’affichent sous la forme de parties ou de parties d’un tout.
* Graphique de dispersion : Utilise un axe horizontal et vertical pour indiquer les valeurs.
* Graphique en courbes : Les valeurs s’affichent sur une seule ligne pour afficher les modifications sur une période donnée.
* Carte de numéro : Affiche un nombre de résumé représentant une valeur de clé unique.
* Tableau de données : Les valeurs s’affichent sous forme de lignes dans un tableau.

>[!NOTE]
>
>La seule mesure actuellement prise en charge pour tous les attributs est le nombre de profils.
>
>Les données affichées dans l’exemple de widget sont fournies à titre d’illustration uniquement. L’aperçu n’affiche pas les données réelles de votre entreprise.

Pour enregistrer votre nouveau widget et revenir à l’onglet [!UICONTROL Personnalisé], sélectionnez **[!UICONTROL Créer]**.

![](../images/customization/create-widget-select-attribute.png)

Vous pouvez désormais ajouter votre nouveau widget à un tableau de bord en le sélectionnant dans la bibliothèque et en sélectionnant **[!UICONTROL Ajouter un widget]**.

![](../images/customization/custom-widgets-new.png)

## Masquage d’un widget personnalisé

Une fois qu’un widget a été ajouté à la bibliothèque, il peut être masqué en sélectionnant les points de suspension (`...`) sur la carte du widget, puis en sélectionnant **[!UICONTROL Masquer le widget]**. Vous pouvez également prévisualiser et modifier le widget à partir de la même liste déroulante.

Pour afficher les widgets qui ont été masqués, sélectionnez **[!UICONTROL Afficher les widgets masqués]** dans le coin supérieur droit de la bibliothèque de widgets.

>[!WARNING]
>
>Le masquage d’un widget dans la bibliothèque ne supprime pas le widget des tableaux de bord des utilisateurs individuels. Si un widget ne doit plus être utilisé dans votre organisation, veillez à le communiquer directement à tous les utilisateurs de Platform, car ils devront le supprimer de leurs tableaux de bord.

![](../images/customization/hide-widget.png)

## Modification d’un widget personnalisé

Vous pouvez modifier des widgets personnalisés dans la bibliothèque de widgets en sélectionnant les points de suspension (`...`) sur la carte de widget, puis en sélectionnant **[!UICONTROL Modifier]** dans le menu déroulant.

![](../images/customization/custom-widget-edit.png)

Dans la boîte de dialogue **[!UICONTROL Modifier le widget]**, vous pouvez modifier le titre et la description du widget, ainsi que prévisualiser et sélectionner différentes visualisations. Une fois vos modifications effectuées, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos modifications et revenir à l’onglet des widgets personnalisés.

>[!WARNING]
>
>La modification d’un widget dans la bibliothèque ne met pas à jour le widget pour les utilisateurs individuels. Si un widget a été mis à jour, veillez à le communiquer directement à tous les utilisateurs de Platform, car ils devront supprimer le widget obsolète de leurs tableaux de bord, puis sélectionner et ajouter le widget mis à jour à partir de la bibliothèque de widgets.

![](../images/customization/edit-widget.png)

## Étapes suivantes

Après avoir lu ce document, vous pouvez accéder à la bibliothèque de widgets et l’utiliser pour créer et ajouter des widgets personnalisés pour votre organisation. Pour modifier la taille et l’emplacement des widgets qui apparaissent dans le tableau de bord, reportez-vous au [guide de modification des tableaux de bord](modify.md).

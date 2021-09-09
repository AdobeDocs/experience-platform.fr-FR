---
keywords: Experience Platform;interface utilisateur;interface utilisateur;tableaux de bord;profils;segments;destinations;utilisation des licences
title: Modifier le schéma pour créer des widgets de tableau de bord personnalisés
description: 'Ce guide fournit des instructions étape par étape pour la sélection des attributs et la configuration du schéma de votre organisation afin de créer des widgets personnalisés pour les tableaux de bord Adobe Experience Platform. '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Modifier le schéma pour créer des widgets personnalisés

Pour créer des widgets personnalisés pour les tableaux de bord Adobe Experience Platform, vous devez d’abord identifier les attributs Real-time Customer Profile sur lesquels les widgets seront basés.

Ce guide fournit des instructions étape par étape pour la modification du schéma de votre organisation en sélectionnant des attributs afin de créer des widgets de tableau de bord personnalisés.

Une fois les attributs sélectionnés et le schéma configuré, vous pouvez suivre la procédure de [création de widgets personnalisés pour vos tableaux de bord](custom-widgets.md).

>[!NOTE]
>
>L’autorisation &quot;Gérer les tableaux de bord standard&quot; doit être accordée aux utilisateurs pour pouvoir modifier le schéma. Pour obtenir des instructions sur l’octroi des autorisations d’accès aux tableaux de bord, reportez-vous au [guide des autorisations des tableaux de bord](../permissions.md).

## Bibliothèque de widgets {#widget-library}

Ce guide nécessite l’accès à la [!UICONTROL bibliothèque de widgets] dans Experience Platform. Pour en savoir plus sur la bibliothèque de widgets et sur la façon d’y accéder dans l’interface utilisateur, commencez par lire la [présentation de la bibliothèque de widgets](widget-library.md).

## Modification du schéma

Dans la bibliothèque de widgets, l’onglet **[!UICONTROL Personnalisé]** vous permet de créer des widgets et de les partager avec d’autres utilisateurs de votre entreprise afin de personnaliser l’aspect de vos tableaux de bord.

Avant de pouvoir créer des widgets personnalisés, les attributs Real-time Customer Profile doivent être sélectionnés pour s’assurer que les données sont incluses dans l’instantané quotidien.

>[!IMPORTANT]
>
>Votre entreprise peut sélectionner 20 attributs au maximum.

Si votre organisation n’a sélectionné aucun attribut de profil, commencez par sélectionner **[!UICONTROL Modifier le schéma]** dans le coin supérieur droit de la bibliothèque de widgets.

Une fois qu’au moins un attribut personnalisé a été créé, sélectionnez **[!UICONTROL Modifier le schéma]** pour afficher les attributs sélectionnés et en ajouter d’autres.

![](../images/customization/edit-schema.png)

## Sélection d’un attribut

Pour sélectionner un attribut dans la boîte de dialogue **[!UICONTROL Sélectionner le champ de schéma d’union]**, accédez à l’attribut dans le schéma d’union (ou utilisez la recherche) et cochez la case en regard de l’attribut. Si vous cochez la case, l’attribut est également ajouté à la liste **[!UICONTROL Attributs sélectionnés]** située dans la partie droite de la boîte de dialogue.

>[!NOTE]
>
>Pour qu’un attribut soit visible pour la sélection, il doit s’agir de l’un des éléments suivants : Chaîne, Date, Date-Heure, Booléen, Court, Long, Entier ou Octet. Les types de données Carte et Double ne sont pas pris en charge et sont grisés afin qu’ils ne puissent pas être sélectionnés.

Après avoir choisi les attributs que vous souhaitez ajouter, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos attributs et revenir à l’onglet widgets personnalisés.

>[!WARNING]
>Les nouveaux attributs sélectionnés deviennent disponibles après l’instantané quotidien suivant l’actualisation des données.

![](../images/customization/select-attribute.png)

## Étapes suivantes

Après avoir lu ce guide, vous pouvez accéder à la bibliothèque de widgets et sélectionner les attributs Real-time Customer Profile pour configurer votre schéma. Une fois les attributs de profil sélectionnés, vous pouvez commencer [à créer des widgets personnalisés pour vos tableaux de bord](custom-widgets.md).
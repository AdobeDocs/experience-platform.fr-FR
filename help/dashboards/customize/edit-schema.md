---
keywords: Experience Platform;interface utilisateur;UI;tableaux de bord;tableau de bord;profils;segments;destinations;utilisation des licences
title: Modification du schéma pour créer des widgets de tableaux de bord personnalisés
description: Ce guide fournit des instructions détaillées relatives à la sélection des attributs et à la configuration du schéma de votre organisation dans le but de créer des widgets personnalisés pour les tableaux de bord d’Adobe Experience Platform.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
TQID: https://experienceleague.adobe.com/wzsVe7h8x3mxCzbF-xHMNxsbCZyoc1njuArukNFm-nU
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 508
ht-degree: 47%

---

# Modification du schéma pour créer des widgets personnalisés

Pour créer des widgets personnalisés pour les tableaux de bord Adobe Experience Platform, vous devez d’abord identifier les attributs du profil client en temps réel sur lesquels les widgets seront basés.

Ce guide fournit des instructions détaillées pour modifier le schéma de votre organisation en sélectionnant des attributs, afin de créer des widgets de tableaux de bord personnalisés.

Une fois les attributs sélectionnés et le schéma configuré, vous pouvez suivre la procédure de [création de widgets personnalisés pour vos tableaux de bord](custom-widgets.md).

>[!NOTE]
>
>Pour pouvoir modifier le schéma, les utilisateurs doivent disposer de l’autorisation « Gérer les tableaux de bord standard ». Pour obtenir des instructions sur l’octroi d’autorisations d’accès aux tableaux de bord, reportez-vous au [guide des autorisations des tableaux de bord](../permissions.md).

## Bibliothèque de widgets {#widget-library}

Ce guide nécessite l’accès à la [!UICONTROL bibliothèque de widgets] d’Experience Platform. Pour en savoir plus sur la bibliothèque de widgets et sur la façon d’y accéder dans l’interface utilisateur, commencez par lire la [présentation de la bibliothèque de widgets](widget-library.md).

## Modification du schéma

Dans la bibliothèque de widgets, l’onglet **[!UICONTROL Personnalisé]** vous permet de créer des widgets et de les partager avec d’autres utilisateurs de votre organisation afin de personnaliser l’aspect de vos tableaux de bord.

Avant de pouvoir créer des widgets personnalisés, vous devez sélectionner les attributs du profil client en temps réel pour vous assurer que les données sont incluses dans l’instantané quotidien.

>[!IMPORTANT]
>
>Votre organisation peut sélectionner jusqu’à 20 attributs.

Si votre organisation n’a sélectionné aucun attribut de profil, commencez par sélectionner **[!UICONTROL Configurer]** au centre de l’écran.

![Onglet personnalisé de l’espace de travail de la bibliothèque de widgets avec l’option Configurer mise en surbrillance.](../images/customization/configure-schema.png)

Après la création d’au moins un attribut personnalisé, sélectionnez **[!UICONTROL Modifier le schéma]** pour afficher les attributs sélectionnés et en ajouter d’autres.

![Onglet personnalisé de l’espace de travail de la bibliothèque de widgets avec l’option Modifier le schéma mise en surbrillance.](../images/customization/edit-schema.png)

## Sélection d’un attribut

Pour sélectionner un attribut dans la boîte de dialogue **[!UICONTROL Sélectionner le champ de schéma d’union]**, accédez à l’attribut dans le schéma d’union (ou utilisez la recherche) et cochez la case en regard de l’attribut. Si vous cochez la case, l’attribut est également ajouté à la liste **[!UICONTROL Attributs sélectionnés]** située dans la partie droite de la boîte de dialogue.

>[!NOTE]
>
>Pour qu’un attribut soit visible pour la sélection, il doit s’agir de l’un des éléments suivants : chaîne, date, date-heure, valeur booléenne, court, long, entier ou octet. Les types de données de mappage et double ne sont pas pris en charge et sont grisés afin d’empêcher leur sélection.

Après avoir choisi les attributs que vous souhaitez ajouter, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos attributs et revenir à l’onglet des widgets personnalisés.

>[!WARNING]
>Les attributs nouvellement sélectionnés sont disponibles après l’instantané quotidien suivant, lorsque l’actualisation des données est effectuée.

![Boîte de dialogue permettant de sélectionner les attributs de schéma avec les attributs et Enregistrer en surbrillance.](../images/customization/select-attribute.png)

## Étapes suivantes

Après lecture de ce guide, vous êtes en mesure d’accéder à la bibliothèque de widgets et de sélectionner les attributs du profil client en temps réel pour configurer votre schéma. Une fois les attributs de profil sélectionnés, vous pouvez démarrer la [création de widgets personnalisés pour vos tableaux de bord](custom-widgets.md).

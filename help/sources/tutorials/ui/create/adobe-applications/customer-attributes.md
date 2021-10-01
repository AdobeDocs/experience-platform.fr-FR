---
keywords: Experience Platform;accueil;rubriques populaires;attributs du client
solution: Experience Platform
title: Création d’une connexion source d’attributs du client dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source dans l’interface utilisateur pour collecter des données de profil d’attributs du client dans Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

---

# Création d’une connexion source Attributs du client dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source dans l’interface utilisateur afin de collecter les données de profil des attributs du client dans Adobe Experience Platform. Pour plus d’informations sur les attributs du client, consultez la [présentation des attributs du client](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=fr).

>[!IMPORTANT]
>
>Les fonctionnalités de désactivation, d’activation et de suppression des flux de données ne sont actuellement pas prises en charge pour la source Attributs du client.

## Création d’une connexion source

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer une connexion.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Adobe d’applications] , sélectionnez **[!UICONTROL Attributs du client]**, puis **[!UICONTROL Ajouter des données]**.

>[!NOTE]
>
>Si vous avez déjà établi une connexion source pour les données de profil Attributs du client, l’option de connexion à la source est désactivée.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

L’écran [!UICONTROL Ajouter des données] répertorie toutes les sources de données disponibles pour les attributs du client. Pour créer une nouvelle connexion, sélectionnez une source de données dans la liste, puis **[!UICONTROL Suivant]**.

>[!NOTE]
>
>Un seul jeu de données peut être sélectionné par connexion source Attributs du client.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

L’étape [!UICONTROL Détails du flux de données] s’affiche, vous permettant de nommer et de fournir une brève description de votre nouveau flux de données.

Au cours de ce processus, vous pouvez également activer [!UICONTROL l’ingestion partielle] et [!UICONTROL les diagnostics d’erreur]. [!UICONTROL L’] ingestion partielle permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil que vous pouvez définir, tandis que les  [!UICONTROL diagnostics d’] erreur fournissent des détails sur les données incorrectes qui sont traitées par lots séparément. Pour plus d’informations, consultez la [présentation de l’ingestion par lots partielle](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

L’étape [!UICONTROL Réviser] s’affiche, ce qui vous permet de passer en revue votre nouveau flux de données avant qu’il ne soit créé. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : Affiche le type de source, le chemin d’accès approprié du fichier source choisi et le nombre de colonnes dans ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Étapes suivantes

Une fois la connexion créée, un schéma et un jeu de données cibles sont automatiquement créés pour contenir les données entrantes. Une fois l’ingestion initiale terminée, les données de profil d’attributs du client peuvent être utilisées par les services Platform en aval tels que [!DNL Real-time Customer Profile] et [!DNL Segmentation Service]. Pour plus d’informations, consultez les documents suivants :

* [Présentation d’[!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Présentation d’[!DNL Segmentation Service]](../../../../../segmentation/home.md)

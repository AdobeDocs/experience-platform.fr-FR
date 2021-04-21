---
keywords: Experience Platform ; accueil ; rubriques populaires ; attributs du client
solution: Experience Platform
title: Création d’une connexion à la source des attributs du client dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source dans l’interface utilisateur pour collecter des données de profil d’attributs du client dans Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---

# Création d’une connexion source Attributs du client dans l’interface utilisateur

Ce didacticiel décrit les étapes à suivre pour créer une connexion source dans l’interface utilisateur afin de collecter les données du profil Attributs du client dans Adobe Experience Platform. Pour plus d&#39;informations sur les attributs du client, consultez la [présentation des attributs du client](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités de désactivation, d’activation et de suppression des flux de données ne sont pas prises en charge pour la source Attributs du client.

## Création d’une connexion source

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer une connexion.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l&#39;aide de la barre de recherche.

Sous la catégorie [!UICONTROL Adobe applications], sélectionnez **[!UICONTROL Attributs du client]**, puis **[!UICONTROL Ajouter les données]**.

>[!NOTE]
>
>Si vous avez déjà établi une connexion source pour les données du profil Attributs du client, l’option de connexion à la source est désactivée.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

L’écran [!UICONTROL Ajouter les données] liste toutes les sources de données disponibles pour les attributs du client. Pour créer une nouvelle connexion, sélectionnez une source de données dans la liste, puis sélectionnez **[!UICONTROL Suivant]**.

>[!NOTE]
>
>Un seul jeu de données peut être sélectionné par connexion source Attributs du client.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

L&#39;étape [!UICONTROL Détails du flux de données] s&#39;affiche, vous permettant de nommer et de fournir une brève description de votre nouveau flux de données.

Au cours de ce processus, vous pouvez également activer les [!UICONTROL diagnostics d&#39;erreur ] et [!UICONTROL diagnostic d&#39;erreur]. [!UICONTROL L’] assimilation partielle permet d’assimiler des données contenant des erreurs, jusqu’à un certain seuil que vous pouvez définir, tandis que les  [!UICONTROL diagnostics d’] erreur fournissent des détails sur les données incorrectes qui sont battues séparément. Pour plus d&#39;informations, consultez l&#39;[aperçu de l&#39;assimilation partielle des lots](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

L&#39;étape [!UICONTROL Réviser] s&#39;affiche, vous permettant de vérifier votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : Indique le type de source, le chemin d’accès approprié du fichier source choisi et le nombre de colonnes dans ce fichier source.
* **[!UICONTROL Attribuer des champs]** de jeu de données et de mappage : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Étapes suivantes

Une fois la connexion créée, un schéma et un jeu de données cibles sont automatiquement créés pour contenir les données entrantes. Une fois l&#39;assimilation initiale terminée, les données du profil des attributs du client peuvent être utilisées par les services de plateforme en aval tels que [!DNL Real-time Customer Profile] et [!DNL Segmentation Service]. Pour plus d’informations, voir les documents suivants :

* [[!DNL Real-time Customer Profile] aperçu](../../../../../profile/home.md)
* [[!DNL Segmentation Service] aperçu](../../../../../segmentation/home.md)

---
keywords: Experience Platform;accueil;rubriques populaires;connecteur source Audience Manager;Audience Manager;connecteur audience manager
solution: Experience Platform
title: Création d’une connexion source Adobe Audience Manager dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Ce tutoriel vous guide tout au long des étapes de création d’un connecteur source pour Adobe Audience Manager afin d’importer les données d’événement d’expérience client dans Platform à l’aide de l’interface utilisateur.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 11%

---

# Créer une connexion source Adobe Audience Manager dans l’interface utilisateur

Ce tutoriel vous guide tout au long des étapes de création d’un connecteur source pour Adobe Audience Manager afin d’importer les données d’événement d’expérience client dans Platform à l’aide de l’interface utilisateur.

## Création d’une connexion source avec Adobe Audience Manager

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au [!UICONTROL Sources] workspace. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Sous , [!UICONTROL Adobe des applications] catégorie, sélectionnez **[!UICONTROL Adobe Audience Manager]** puis sélectionnez **[!UICONTROL Configurer]**.

![catalogue](../../../../images/tutorials/create/aam/catalog.png)

Le [!UICONTROL Sélection de caractéristiques et de segments] s’affiche, vous fournissant une interface interactive permettant d’explorer et de sélectionner vos caractéristiques, segments et données.

* Le panneau de gauche de l’interface contient le [!UICONTROL Sélection de caractéristiques et de segments] , ainsi qu’un répertoire hiérarchique de tous les segments disponibles.
* La moitié droite de l’interface vous permet d’interagir avec les segments sélectionnés et de sélectionner les données spécifiques que vous souhaitez utiliser.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Pour parcourir les segments disponibles, sélectionnez le dossier auquel vous souhaitez accéder à partir du [!UICONTROL Tous les segments] du panneau. La sélection d’un dossier vous permet de parcourir la hiérarchie d’un dossier et vous fournit une liste de segments à filtrer.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Une fois que vous avez identifié et sélectionné les segments que vous souhaitez utiliser, un nouveau panneau s’affiche à droite, affichant votre liste d’éléments sélectionnés. Vous pouvez continuer à accéder à différents dossiers et sélectionner différents segments pour votre connexion. La sélection d’autres segments met à jour le panneau de droite.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Vous pouvez également sélectionner la variable **[!UICONTROL Sélectionner tous les segments]** et **[!UICONTROL Sélectionner toutes les caractéristiques]** des boîtes de dialogue. La sélection de tous les segments apporte les segments d’Audience Manager à Platform, tandis que la sélection de toutes les caractéristiques active toutes les caractéristiques propriétaires de l’Audience Manager.

Une fois que vous avez terminé, sélectionnez **[!UICONTROL Suivant]**

![tous les segments](../../../../images/tutorials/create/aam/all-segments.png)

Le [!UICONTROL Réviser] s’affiche, ce qui vous permet de passer en revue vos caractéristiques et segments sélectionnés avant qu’ils ne soient connectés à Platform. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]**: Affiche la plateforme source et l’état de la connexion.
* **[!UICONTROL Données sélectionnées]**: Affiche le nombre de segments sélectionnés et de caractéristiques activées.

![review](../../../../images/tutorials/create/aam/review.png)

Une fois que vous avez examiné votre flux de données, sélectionnez **[!UICONTROL Terminer]** et accorder un certain temps pour la création du flux de données.

## Étapes suivantes

Lorsqu’un flux de données d’Audience Manager est principal, les données entrantes sont automatiquement ingérées dans les profils clients en temps réel. Vous pouvez désormais utiliser ces données entrantes et créer des segments d’audience à l’aide de Platform Segmentation Service. Consultez les documents suivants pour plus d’informations :

* [Présentation du profil client en temps réel](../../../../../profile/home.md)
* [Présentation de Segmentation Service](../../../../../segmentation/home.md)

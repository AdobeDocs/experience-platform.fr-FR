---
keywords: Experience Platform ; accueil ; rubriques populaires ; connecteur source du gestionnaire d’Audiences ; Audience Manager ; connecteur du gestionnaire d’audiences
solution: Experience Platform
title: Création d’une connexion à la source Adobe Audience Manager dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Ce didacticiel vous guide tout au long des étapes nécessaires pour créer des connecteurs source pour Adobe Audience Manager afin d’importer les données du Événement d’expérience de consommation dans la plate-forme à l’aide de l’interface utilisateur.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---

# Création d’une connexion source Adobe Audience Manager dans l’interface utilisateur

Ce didacticiel vous guide tout au long des étapes de création d’un connecteur source pour Adobe Audience Manager afin d’importer les données du Événement d’expérience de consommation dans la plate-forme à l’aide de l’interface utilisateur.

## Création d’une connexion source avec Adobe Audience Manager

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Sous la catégorie [!UICONTROL Adobe applications], sélectionnez **[!UICONTROL Adobe Audience Manager]**, puis **[!UICONTROL Configurer]**.

![catalogue](../../../../images/tutorials/create/aam/catalog.png)

L&#39;étape [!UICONTROL Sélectionner les caractéristiques et les segments] s&#39;affiche, vous offrant une interface interactive pour explorer et sélectionner vos caractéristiques, segments et données.

* Le panneau de gauche de l&#39;interface contient les options [!UICONTROL Sélectionner les caractéristiques et les segments], ainsi qu&#39;un répertoire hiérarchique de tous les segments disponibles.
* La moitié droite de l’interface vous permet d’interagir avec les segments sélectionnés et de sélectionner les données spécifiques à utiliser.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Pour parcourir les segments disponibles, sélectionnez le dossier auquel vous souhaitez accéder à partir du panneau [!UICONTROL Tous les segments]. La sélection d’un dossier vous permet de traverser la hiérarchie d’un dossier et vous fournit une liste de segments à filtrer.

![segment-dossier](../../../../images/tutorials/create/aam/segment-folder.png)

Une fois que vous avez identifié et sélectionné les segments à utiliser, un nouveau panneau s’affiche à droite, affichant votre liste d’éléments sélectionnés. Vous pouvez continuer à accéder à différents dossiers et sélectionner différents segments pour votre connexion. La sélection de segments supplémentaires met à jour le panneau sur la droite.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Vous pouvez également sélectionner les zones **[!UICONTROL Sélectionner tous les segments]** et **[!UICONTROL Sélectionner toutes les caractéristiques]**. La sélection de tous les segments amènera les segments d’Audience Manager à la plate-forme, tandis que la sélection de toutes les caractéristiques active toutes les caractéristiques propriétaires de l’Audience Manager.

Une fois que vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![tous les segments](../../../../images/tutorials/create/aam/all-segments.png)

L&#39;étape [!UICONTROL Réviser] s&#39;affiche, vous permettant de passer en revue vos caractéristiques et segments sélectionnés avant qu&#39;ils ne soient connectés à la plate-forme. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : Affiche la plate-forme source et l&#39;état de la connexion.
* **[!UICONTROL Données]** sélectionnées : Affiche le nombre de segments sélectionnés et de caractéristiques activées.

![examiner](../../../../images/tutorials/create/aam/review.png)

Une fois que vous avez passé en revue votre flux de données, sélectionnez **[!UICONTROL Terminer]** et attendez un certain temps pour que le flux de données soit créé.

## Étapes suivantes

Lorsqu’un flux de données d’Audience Manager est principal, les données entrantes sont automatiquement assimilées aux Profils client en temps réel. Vous pouvez désormais utiliser ces données entrantes et créer des segments d’audience à l’aide du service de segmentation de plate-forme. Pour plus d’informations, voir les documents suivants :

* [Présentation du profil client en temps réel](../../../../../profile/home.md)
* [Présentation du service de segmentation](../../../../../segmentation/home.md)

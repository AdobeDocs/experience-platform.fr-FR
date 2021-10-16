---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zone d’entrée des données;zone d’entrée des données
solution: Experience Platform
title: Connexion de la zone d’entrée des données à Platform à l’aide de l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer un connecteur source de zone d’entrée de données à l’aide de l’interface utilisateur de Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 10%

---

# Connexion de [!DNL Data Landing Zone] à Platform à l’aide de l’interface utilisateur

[!DNL Data Landing Zone] est une fonctionnalité de stockage de données dans le cloud pour le stockage de fichiers temporaire configurée avec Adobe Experience Platform. Les données sont automatiquement supprimées de [!DNL Data Landing Zone] au bout de sept jours.

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Data Landing Zone] à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Exportez vos fichiers de [!DNL Data Landing Zone] vers Platform.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL espace de stockage dans le cloud], sélectionnez [!DNL Data Landing Zone], puis **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/dlz/catalog.png)

L’étape [!UICONTROL Ajouter des données] s’affiche, vous fournissant une interface pour sélectionner et prévisualiser les données à importer dans Platform.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

Pour obtenir un guide détaillé et détaillé sur la création d’un flux de données pour une source de stockage dans le cloud, consultez le tutoriel sur la [création d’un flux de données de stockage dans le cloud pour importer des données vers Platform](../../dataflow/batch/cloud-storage.md).

## Récupérez et actualisez vos informations d’identification [!DNL Data Landing Zone]

[!DNL Data Landing Zone] est une source prête à l’emploi fournie avec votre licence Sources Adobe Experience Platform. [!DNL Data Landing Zone] utilise une authentification SAS URI et SAS Token. Vous pouvez récupérer et actualiser vos informations d’authentification à partir de la page [!UICONTROL Catalogue de sources] .

Dans le [!UICONTROL catalogue des sources], sous la catégorie [!UICONTROL Stockage dans le cloud], sélectionnez les ellipses (**...**) à partir de la carte **[!UICONTROL Zone d’entrée des données]**. Dans le menu déroulant qui s’affiche, sélectionnez **[!UICONTROL Afficher les informations d’identification]**.

![Options](../../../../images/tutorials/create/dlz/options.png)

Une fenêtre contextuelle s’affiche, indiquant le nom du conteneur, le jeton SAS, le nom du compte de stockage et l’URI SAS.

Sélectionnez **[!UICONTROL Actualiser les informations d’identification]** et attendez quelques secondes pour que vos informations d’identification mises à jour soient traitées.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez accédé à votre conteneur [!DNL Data Landing Zone] et appris à récupérer et à actualiser vos informations d’identification. Vous pouvez maintenant passer au tutoriel suivant sur la [création d’un flux de données pour importer les données d’un espace de stockage dans le cloud vers Platform](../../dataflow/batch/cloud-storage.md).

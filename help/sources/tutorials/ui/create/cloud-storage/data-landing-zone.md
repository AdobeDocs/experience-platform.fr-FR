---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zone d’entrée des données;zone d’entrée des données
solution: Experience Platform
title: Connexion de la zone d’entrée des données à Platform à l’aide de l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer un connecteur source de zone d’entrée de données à l’aide de l’interface utilisateur de Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: b007cdf92811b453df5b5d005456a05cd845b769
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 9%

---

# Connexion [!DNL Data Landing Zone] vers Platform à l’aide de l’interface utilisateur

[!DNL Data Landing Zone] est une fonctionnalité de stockage de données dans le cloud pour le stockage de fichiers temporaire configurée avec Adobe Experience Platform. Les données sont automatiquement supprimées de la variable [!DNL Data Landing Zone] après sept jours.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Data Landing Zone] connexion source à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Exportez vos fichiers depuis [!DNL Data Landing Zone] vers Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de la barre de recherche.

Sous , [!UICONTROL espace de stockage] catégorie, sélectionnez [!DNL Data Landing Zone] puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/dlz/catalog.png)

Le [!UICONTROL Ajouter des données] s’affiche, vous fournissant une interface pour sélectionner et prévisualiser les données à importer dans Platform.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

Pour obtenir un guide détaillé et détaillé sur la création d’un flux de données pour une source de stockage dans le cloud, consultez le tutoriel sur [création d’un flux de données de stockage dans le cloud pour importer des données dans Platform](../../dataflow/batch/cloud-storage.md).

## Récupérez et actualisez votre [!DNL Data Landing Zone] informations

[!DNL Data Landing Zone] est une source prête à l’emploi fournie avec votre licence Sources Adobe Experience Platform. [!DNL Data Landing Zone] utilise une authentification SAS URI et SAS Token. Vous pouvez récupérer et actualiser vos informations d’authentification à partir du [!UICONTROL Catalogue de sources] page.

Dans le [!UICONTROL Catalogue de sources], sous [!UICONTROL Stockage dans le cloud] , sélectionnez les ellipses (**...**) de la variable **[!UICONTROL Zone d’entrée des données]** carte. Dans le menu déroulant qui s’affiche, sélectionnez **[!UICONTROL Affichage des informations d’identification]**.

![Options](../../../../images/tutorials/create/dlz/options.png)

Une fenêtre contextuelle s’affiche, indiquant le nom du conteneur, le jeton SAS, le nom du compte de stockage et l’URI SAS.

Sélectionner **[!UICONTROL Actualiser les informations d’identification]** et comptez quelques secondes pour que vos informations d’identification mises à jour soient traitées.

>[!TIP]
>
>Votre [!DNL Data Landing Zone] les informations d’identification sont définies pour expirer automatiquement après 90 jours et vous devez utiliser de nouvelles informations d’identification pour vous reconnecter à [!DNL Data Landing Zone] après expiration. Vos flux de données dans Platform ne sont pas affectés par l’expiration des informations d’identification et vous pouvez continuer à utiliser les nouveaux flux de données existants avec vos nouvelles informations d’identification.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez accédé à votre [!DNL Data Landing Zone] et appris à récupérer et à actualiser vos informations d’identification. Vous pouvez maintenant passer au tutoriel suivant sur [création d’un flux de données pour importer des données d’un espace de stockage dans le cloud vers Platform](../../dataflow/batch/cloud-storage.md).

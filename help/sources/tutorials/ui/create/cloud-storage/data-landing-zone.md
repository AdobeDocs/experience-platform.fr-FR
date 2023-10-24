---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zone d’entrée des données;zone d’entrée des données
title: Connexion de la zone d’entrée des données à Platform à l’aide de l’interface utilisateur
description: Découvrez comment créer un connecteur source de zone d’entrée de données à l’aide de l’interface utilisateur de Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 9cffd508c1bff7ce133f84ca686c414e997343b8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 20%

---

# Connecter [!DNL Data Landing Zone] à Platform à l’aide de l’interface utilisateur

>[!IMPORTANT]
>
>Cette page est spécifique aux [!DNL Data Landing Zone] *source* connecteur dans Experience Platform. Pour plus d’informations sur la connexion à la variable [!DNL Data Landing Zone] *destination* connecteur, voir [[!DNL Data Landing Zone] page de documentation de destination](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] est une fonctionnalité sécurisée de stockage de fichiers dans le cloud pour importer des fichiers dans Adobe Experience Platform. Les données sont automatiquement supprimées de la variable [!DNL Data Landing Zone] après sept jours.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Data Landing Zone] connexion source à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Exportez vos fichiers depuis [!DNL Data Landing Zone] vers Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Sous , [!UICONTROL espace de stockage] catégorie, sélectionnez [!DNL Data Landing Zone] puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue de sources avec zone d’entrée des données sélectionnée.](../../../../images/tutorials/create/dlz/catalog.png)

La variable [!UICONTROL Ajouter des données] s’affiche, vous fournissant une interface permettant de sélectionner et de prévisualiser les données à importer dans Platform.

* La partie gauche de l’interface est un explorateur de dossiers qui vous fournit une liste de fichiers de votre conteneur que vous pouvez ensuite apporter à Platform.
* La partie droite de l&#39;interface permet de prévisualiser jusqu&#39;à 100 lignes de données à partir d&#39;un fichier compatible.

Sélectionnez le fichier à importer dans Experience Platform et attendez quelques instants avant que l’interface de droite ne se mette à jour dans un écran de prévisualisation.

![Interface d’ajout de données de l’espace de travail des sources.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform détecte automatiquement les informations de propriété du fichier que vous avez sélectionné, y compris les informations sur le format de données du fichier, le délimiteur de colonne désigné et le type de compression.

L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Par défaut, l’interface d’aperçu affiche le premier fichier du dossier que vous avez sélectionné.

Pour prévisualiser un autre fichier, cliquez sur l’icône d’aperçu située en regard du nom du fichier à inspecter.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![La page d’aperçu des données de l’espace de travail des sources.](../../../../images/tutorials/create/dlz/file-detection.png)

Pour obtenir un guide détaillé et détaillé sur la création d’un flux de données pour une source de stockage dans le cloud, consultez le tutoriel sur [création d’un flux de données de stockage dans le cloud pour importer des données dans Platform](../../dataflow/batch/cloud-storage.md).

## Récupérer et actualiser votre [!DNL Data Landing Zone] informations

[!DNL Data Landing Zone] est une source prête à l’emploi fournie avec votre licence Sources Adobe Experience Platform. [!DNL Data Landing Zone] utilise une authentification SAS URI et SAS Token. Vous pouvez récupérer et actualiser vos informations d’authentification à partir du [!UICONTROL Catalogue de sources] page.

Dans le [!UICONTROL Catalogue de sources], sous [!UICONTROL Stockage dans le cloud] , sélectionnez les ellipses (**..**) de la variable **[!UICONTROL Zone d’entrée des données]** carte. Dans le menu déroulant qui s’affiche, sélectionnez **[!UICONTROL Affichage des informations d’identification]**.

![Liste des options d’affichage pour la zone d’entrée des données.](../../../../images/tutorials/create/dlz/options.png)

Une fenêtre contextuelle s’affiche, indiquant le nom du conteneur, le jeton SAS, le nom du compte de stockage, l’URI SAS et la date d’expiration.

Sélectionner **[!UICONTROL Actualiser les informations d’identification]** et comptez quelques secondes pour que vos informations d’identification mises à jour soient traitées.

>[!TIP]
>
>Votre [!DNL Data Landing Zone] les informations d’identification sont définies pour expirer automatiquement après 90 jours et vous devez utiliser de nouvelles informations d’identification pour vous reconnecter à [!DNL Data Landing Zone] après expiration. Vos flux de données dans Platform ne sont pas affectés par l’expiration des informations d’identification et vous pouvez continuer à utiliser les nouveaux flux de données existants avec vos nouvelles informations d’identification.

![Les informations d’identification associées à un compte Data Landing Zone donné.](../../../../images/tutorials/create/dlz/view-credentials.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez accédé à votre [!DNL Data Landing Zone] et appris à récupérer et à actualiser vos informations d’identification. Vous pouvez maintenant passer au tutoriel suivant sur [création d’un flux de données pour importer des données d’un espace de stockage dans le cloud vers Platform](../../dataflow/batch/cloud-storage.md).

---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zone d’entrée des données;zone d’entrée des données
title: Connexion de la zone d’entrée des données à Platform à l’aide de l’interface utilisateur
description: Découvrez comment créer un connecteur source de zone d’entrée de données à l’aide de l’interface utilisateur de Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: fb16ea940ef394a15dd24fe703239b4487fafb18
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 22%

---

# Connexion [!DNL Data Landing Zone] vers Platform à l’aide de l’interface utilisateur

[!DNL Data Landing Zone] est une fonctionnalité sécurisée de stockage de fichiers dans le cloud pour importer des fichiers dans Adobe Experience Platform. Les données sont automatiquement supprimées de la variable [!DNL Data Landing Zone] après sept jours.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Data Landing Zone] connexion source à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Exportez vos fichiers depuis [!DNL Data Landing Zone] vers Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Sous , [!UICONTROL espace de stockage] catégorie, sélectionnez [!DNL Data Landing Zone] puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/dlz/catalog.png)

Le [!UICONTROL Ajouter des données] s’affiche, vous fournissant une interface pour sélectionner et prévisualiser les données à importer dans Platform.

* La partie gauche de l’interface est un explorateur de dossiers qui vous fournit une liste de fichiers de votre conteneur que vous pouvez ensuite apporter à Platform.
* La partie droite de l&#39;interface permet de prévisualiser jusqu&#39;à 100 lignes de données à partir d&#39;un fichier compatible.

Sélectionnez le fichier que vous souhaitez importer dans Platform et attendez quelques instants pour que l’interface de droite se mette à jour dans un écran de prévisualisation.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform détecte automatiquement les informations de propriété du fichier que vous avez sélectionné, y compris les informations sur le format de données du fichier, le délimiteur de colonne désigné et le type de compression.

L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Par défaut, l’interface d’aperçu affiche le premier fichier du dossier que vous avez sélectionné.

Pour prévisualiser un autre fichier, cliquez sur l’icône d’aperçu située en regard du nom du fichier à inspecter.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![détection de fichier](../../../../images/tutorials/create/dlz/file-detection.png)

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

---
title: Connexion de la zone d’entrée des données à Platform à l’aide de l’interface utilisateur
description: Découvrez comment créer un connecteur source de zone d’entrée de données à l’aide de l’interface utilisateur de Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 19%

---

# Connecter [!DNL Data Landing Zone] à Platform à l’aide de l’interface utilisateur

>[!IMPORTANT]
>
>Cette page est spécifique au connecteur [!DNL Data Landing Zone] *source* dans Experience Platform. Pour plus d&#39;informations sur la connexion au connecteur [!DNL Data Landing Zone] *destination*, consultez la [[!DNL Data Landing Zone] page de documentation de destination](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] est une fonctionnalité sécurisée de stockage de fichiers dans le cloud pour importer des fichiers dans Adobe Experience Platform. Les données sont automatiquement supprimées de l’élément [!DNL Data Landing Zone] au bout de sept jours.

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Data Landing Zone] à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Amener vos fichiers de [!DNL Data Landing Zone] vers Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Sous la catégorie [!UICONTROL espace de stockage dans le cloud], sélectionnez [!DNL Data Landing Zone], puis **[!UICONTROL Ajouter des données]**.

![Catalogue de sources avec zone d’entrée de données sélectionnée.](../../../../images/tutorials/create/dlz/catalog.png)

L’étape [!UICONTROL Ajouter des données] s’affiche, vous fournissant une interface pour sélectionner et prévisualiser les données à importer dans Platform.

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

![La page d&#39;aperçu des données de l&#39;espace de travail des sources.](../../../../images/tutorials/create/dlz/file-detection.png)

Pour obtenir un guide détaillé et détaillé sur la création d’un flux de données pour une source de stockage dans le cloud, consultez le tutoriel sur la [création d’un flux de données de stockage dans le cloud pour importer des données vers Platform](../../dataflow/batch/cloud-storage.md).

## Récupération de vos informations d’identification [!DNL Data Landing Zone]

[!DNL Data Landing Zone] est une source fournie avec votre licence Sources de Adobe Experience Platform. [!DNL Data Landing Zone] utilise une authentification SAS URI et SAS Token. Vous pouvez récupérer vos informations d’authentification à partir de la page [!UICONTROL Catalogue de sources] .

Pour récupérer vos informations d’identification, sélectionnez la carte **[!UICONTROL Data Landing Zone]** , puis copiez vos informations d’identification depuis le rail de droite qui s’affiche.

![Liste des options d’affichage pour la zone d’entrée des données.](../../../../images/tutorials/create/dlz/view-credentials.png)

Une fenêtre contextuelle s’affiche, indiquant le nom du conteneur, le jeton SAS, le nom du compte de stockage, l’URI SAS et la date d’expiration.

## Actualiser vos informations d’identification [!DNL Data Landing Zone]

Vos informations d’identification [!DNL Data Landing Zone] sont définies pour expirer automatiquement après 90 jours et vous devez utiliser de nouvelles informations d’identification pour vous reconnecter à [!DNL Data Landing Zone] après expiration. Vos flux de données dans Experience Platform ne sont pas affectés par l’expiration des informations d’identification et vous pouvez continuer à travailler avec les nouveaux flux de données existants avec vos nouvelles informations d’identification.

Il existe deux manières d’actualiser vos informations d’identification [!DNL Data Landing Zone] :

>[!BEGINTABS]

>[!TAB Utiliser la carte source]

Pour actualiser vos informations d’identification à partir de la page du catalogue des sources, sélectionnez les points de suspension (**`...`**) dans la carte [!DNL Data Landing Zone], puis sélectionnez **[!UICONTROL Actualiser les informations d’identification]**.

![Actualisez les informations d’identification à l’aide de la carte source.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

Une fenêtre contextuelle s’affiche, vous invitant à confirmer votre choix avant de pouvoir continuer. Lorsque vous êtes prêt, sélectionnez **[!UICONTROL Actualiser les informations d’identification]**.

![Fenêtre de confirmation des informations d’identification d’actualisation.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB Utiliser le rail droit]

Pour actualiser vos informations d’identification à l’aide du rail de droite, sélectionnez la carte source **[!UICONTROL Data Landing Zone]** , puis sélectionnez **[!UICONTROL Autres actions]**. Sélectionnez ensuite **[!UICONTROL Actualiser les informations d’identification]**, puis confirmez à l’aide de la fenêtre contextuelle qui s’affiche.

![Actualisez les informations d’identification à l’aide du rail de droite.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez accédé à votre conteneur [!DNL Data Landing Zone] et appris à récupérer et à actualiser vos informations d’identification. Vous pouvez maintenant passer au tutoriel suivant sur la [création d’un flux de données pour importer des données d’un espace de stockage dans le cloud vers Platform](../../dataflow/batch/cloud-storage.md).

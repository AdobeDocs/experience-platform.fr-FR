---
keywords: Experience Platform;accueil;rubriques les plus consultées;système local;téléchargement de fichiers;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide ui;
solution: Experience Platform
title: Création d’un connecteur source de téléchargement de fichier local dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source pour votre système local pour importer des fichiers locaux dans Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: 08805ed0d89d3d6908ddccdafda55d2f862e727e
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 9%

---

# Création d’un connecteur source de transfert de fichiers local dans l’interface utilisateur

Ce tutoriel décrit les étapes de création d’un connecteur source de chargement de fichier local pour ingérer des fichiers locaux vers Platform à l’aide de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel de l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md): Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Chargement de fichiers locaux dans Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL Système local] catégorie, sélectionnez **[!UICONTROL Chargement de fichier local]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/local/catalog.png)

### Utilisation d’un jeu de données existant

Le [!UICONTROL Détails du flux de données] vous permet de choisir si vous souhaitez ingérer vos données CSV dans un jeu de données existant ou un nouveau jeu de données.

Pour ingérer vos données CSV dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Vous pouvez récupérer un jeu de données existant à l’aide de la variable [!UICONTROL Recherche avancée] ou en faisant défiler la liste des jeux de données existants dans le menu déroulant.

Une fois qu’un jeu de données est sélectionné, attribuez un nom à votre flux de données et une description facultative.

Au cours de ce processus, vous pouvez également activer [!UICONTROL Diagnostics d’erreur] et [!UICONTROL Ingestion partielle]. [!UICONTROL Diagnostics d’erreur] permet la génération de messages d’erreur détaillés pour tout enregistrement erroné qui se produit dans votre flux de données, tandis que [!UICONTROL Ingestion partielle] vous permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil que vous définissez manuellement. Voir [Présentation de l’ingestion par lots partielle](../../../../../ingestion/batch-ingestion/partial.md) pour plus d’informations.

![existing-dataset](../../../../images/tutorials/create/local/existing-dataset.png)

### Utilisation d’un nouveau jeu de données

Pour ingérer vos données CSV dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** puis fournissez un nom de jeu de données de sortie et une description facultative. Sélectionnez ensuite un schéma à mapper à l’aide de la propriété [!UICONTROL Recherche avancée] ou en faisant défiler la liste des schémas existants dans le menu déroulant.

Une fois le schéma sélectionné, attribuez un nom à votre flux de données et une description facultative, puis appliquez la variable [!UICONTROL Diagnostics d’erreur] et [!UICONTROL Ingestion partielle] paramètres de votre flux de données. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![new-dataset](../../../../images/tutorials/create/local/new-dataset.png)

### Sélectionner des données

Le [!UICONTROL Sélectionner des données] s’affiche, fournissant une interface pour télécharger vos fichiers locaux et prévisualiser leur structure et leur contenu. Sélectionner **[!UICONTROL Sélection de fichiers]** pour charger un fichier CSV à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier CSV que vous souhaitez transférer dans le [!UICONTROL Glisser-déposer des fichiers] du panneau.

>[!TIP]
>
>Seuls les fichiers CSV sont actuellement pris en charge par le téléchargement de fichiers local. La taille de fichier maximale pour chaque fichier est de 1 Go.

![choice-files](../../../../images/tutorials/create/local/choose-files.png)

Une fois le fichier téléchargé, l’interface de prévisualisation se met à jour pour afficher le contenu et la structure du fichier.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Selon votre fichier, vous pouvez sélectionner un délimiteur de colonne (tabulations, virgules, barres verticales, ou un délimiteur de colonne personnalisé) pour vos données source. Sélectionnez la **[!UICONTROL Délimiteur]** Flèche de liste déroulante, puis sélectionnez le délimiteur approprié dans le menu.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![délimiteur](../../../../images/tutorials/create/local/delimiter.png)

## Mappage

Le [!UICONTROL Mappage] s’affiche, vous fournissant une interface pour mapper les champs source de votre schéma source à leurs champs XDM cibles appropriés dans le schéma cible.

Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs calculées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface de mappage, reportez-vous à la section [Guide de l’interface utilisateur de la préparation de données](../../../../../data-prep/ui/mapping.md).

Une fois vos jeux de mappages prêts, sélectionnez **[!UICONTROL Terminer]** et prenez en compte quelques instants pour la création du nouveau flux de données.

![mapping](../../../../images/tutorials/create/local/mapping.png)

## Surveillance de l’ingestion des données

Une fois votre fichier CSV mappé et créé, vous pouvez surveiller les données ingérées à l’aide du tableau de bord de surveillance. Pour plus d’informations, consultez le tutoriel sur [surveillance des flux de données de sources dans l’interface utilisateur](../../../../../dataflows/ui/monitor-sources.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez mappé un fichier CSV plat à un schéma XDM et l’avez ingéré dans Platform. Ces données peuvent désormais être utilisées en aval. [!DNL Platform] des services tels que [!DNL Real-time Customer Profile]. Consultez la présentation pour [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) pour plus d’informations.

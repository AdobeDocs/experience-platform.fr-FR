---
keywords: Experience Platform;accueil;rubriques les plus consultées;système local;téléchargement de fichiers;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide ui;
solution: Experience Platform
title: Création d’un connecteur Source de téléchargement de fichier local dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source pour votre système local pour importer des fichiers locaux dans Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 72%

---

# Création d’un connecteur source de transfert de fichiers local dans l’interface utilisateur

Ce tutoriel décrit les étapes de création d’un connecteur source de chargement de fichier local pour ingérer des fichiers locaux vers Platform à l’aide de l’interface utilisateur.

## Commencer

Ce tutoriel nécessite une compréhension pratique des composants suivants de Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Le cadre normalisé par lequel Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Chargement de fichiers locaux dans Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie [!UICONTROL Système local], sélectionnez **[!UICONTROL Chargement de fichier local]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/local/catalog.png)

### Utiliser un jeu de données existant

La page [!UICONTROL Détails du flux de données] vous permet de choisir si vous souhaitez ingérer vos données CSV dans un jeu de données existant ou un nouveau jeu de données.

Pour ingérer vos données CSV dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Vous pouvez soit récupérer un jeu de données existant à l’aide de l’option de [!UICONTROL Recherche avancée], soit en faisant défiler la liste des jeux de données existants dans le menu déroulant.

Une fois un jeu de données sélectionné, donnez un nom à votre flux de données et une description facultative.

Au cours de ce processus, vous pouvez également activer les [!UICONTROL diagnostics d’erreur] et l’[!UICONTROL ingestion partielle]. Le [!UICONTROL diagnostic d’erreur] permet de générer un message d’erreur détaillé pour tout enregistrement erroné survenant dans votre flux de données, tandis que l’[!UICONTROL ingestion partielle] vous permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil que vous définissez manuellement. Pour plus d’informations, consultez la [présentation de l’ingestion par lots partiels](../../../../../ingestion/batch-ingestion/partial.md).

![existing-dataset](../../../../images/tutorials/create/local/existing-dataset.png)

### Utiliser un nouveau jeu de données

Pour ingérer vos données CSV dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** puis fournissez un nom de jeu de données de sortie et une description facultative. Sélectionnez ensuite un schéma à mapper à l’aide de l’option [!UICONTROL Recherche avancée] ou en faisant défiler la liste des schémas existants dans le menu déroulant.

Une fois le schéma sélectionné, donnez un nom à votre flux de données et une description facultative, puis appliquez les [!UICONTROL diagnostics d’erreur] et les paramètres d’[!UICONTROL ingestion partielle] que vous souhaitez pour votre flux de données. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![new-dataset](../../../../images/tutorials/create/local/new-dataset.png)

### Sélectionner les données

L’étape [!UICONTROL Sélectionner les données] apparaît, vous offrant une interface pour charger vos fichiers locaux et prévisualiser leur structure et leur contenu. Sélectionnez **[!UICONTROL Choisir les fichiers]** pour charger un fichier CSV à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier CSV que vous souhaitez charger dans le panneau [!UICONTROL Glisser-déposer des fichiers].

>[!TIP]
>
>Seuls les fichiers CSV sont actuellement pris en charge par le chargement de fichiers locaux. La taille maximale de chaque fichier est de 1 Go.

![choose-files](../../../../images/tutorials/create/local/choose-files.png)

Une fois votre fichier chargé, l’interface de prévisualisation se met à jour pour afficher le contenu et la structure du fichier.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

En fonction de votre fichier, vous pouvez sélectionner un délimiteur de colonne tel que des tabulations, des virgules, des barres verticales ou un délimiteur de colonne personnalisé pour vos données source. Sélectionnez la flèche déroulante **[!UICONTROL Délimiteur]**, puis sélectionnez le délimiteur approprié dans le menu.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![délimiteur](../../../../images/tutorials/create/local/delimiter.png)

## Mappage

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface de mappage, consultez le [Guide de l’interface utilisateur de la préparation de données](../../../../../data-prep/ui/mapping.md).

Une fois vos jeux de mappages prêts, sélectionnez **[!UICONTROL Terminer]** et attendez quelques instants pour créer le nouveau flux de données.

![mappage](../../../../images/tutorials/create/local/mapping.png)

## Surveiller l’ingestion des données

Une fois votre fichier CSV mappé et créé, vous pouvez surveiller les données ingérées à l’aide du tableau de bord de surveillance. Pour plus d’informations, consultez le tutoriel sur la [surveillance des flux de données de sources dans l’interface utilisateur](../../../../../dataflows/ui/monitor-sources.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez mappé un fichier CSV plat à un schéma XDM et l’avez ingéré dans Platform. Ces données peuvent désormais être utilisées par les services de [!DNL Platform] en aval, comme [!DNL Real-Time Customer Profile]. Pour de plus d’informations, rendez-vous sur la présentation de [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md).

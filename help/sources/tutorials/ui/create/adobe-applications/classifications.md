---
keywords: Experience Platform;home;popular topics; analytics;classifications
description: Ce didacticiel décrit la procédure à suivre pour créer un connecteur de données de classifications Adobe Analytics dans l’interface utilisateur afin d’importer des données de classification dans Adobe Experience Platform.
solution: Experience Platform
title: Création d’un connecteur de données de classifications Adobe Analytics dans l’interface utilisateur
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 4%

---


# Création d’un connecteur de données de classifications Adobe Analytics dans l’interface utilisateur

Ce didacticiel décrit la procédure à suivre pour créer un connecteur de données de classifications Adobe Analytics dans l’interface utilisateur afin d’importer des données de classification dans Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model] (XDM) Système](../../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
* [[ !Profil client en temps réel DNL]](../../../../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[ !Sandbox DNL]](../../../../../sandboxes/home.md): experience platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

## Sélectionner vos classifications

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail sources. L’écran **[!UICONTROL Catalogue]** affiche les sources disponibles pour créer des connexions entrantes avec. Chaque carte source affiche une option permettant de configurer un nouveau compte ou d’ajouter des données à un compte existant.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie des applications **[!UICONTROL d’]** Adobe, sélectionnez la carte **[!UICONTROL Adobe Analytics]** , puis sélectionnez **[!UICONTROL Ajouter les données]** au début en utilisant les données de classification Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

L’étape d’ajout de données **[!UICONTROL à la source]** Analytics s’affiche. Sélectionnez **[!UICONTROL Classifications]** dans l’en-tête supérieur pour afficher une liste de [!DNL Classifications] jeux de données, y compris des informations sur leur ID **[!UICONTROL de]** Dimension, le nom **[!UICONTROL de la suite de]** rapports et l’ID de la suite de rapports .****

Chaque page affiche jusqu’à dix [!DNL Classifications] jeux de données différents parmi lesquels vous pouvez choisir. Sélectionnez **[!UICONTROL Suivant]** en bas de la page pour rechercher d’autres options. Le panneau de droite affiche le nombre total de jeux de données que vous avez sélectionnés, ainsi que leurs noms. [!DNL Classifications] Ce panneau vous permet également de supprimer tous les [!DNL Classifications] jeux de données sélectionnés par erreur ou d&#39;effacer toutes les sélections par une seule action.

Vous pouvez sélectionner jusqu’à 30 [!DNL Classifications] jeux de données différents à importer [!DNL Platform].

Une fois que vous avez sélectionné vos [!DNL Classifications] jeux de données, sélectionnez **[!UICONTROL Suivant]** en haut à droite de la page.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Vérifier vos classifications

L&#39;étape **[!UICONTROL Révision]** s&#39;affiche, vous permettant de revoir vos [!DNL Classifications] jeux de données sélectionnés avant de les créer. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]**: Affiche la plate-forme source et l&#39;état de la connexion.
* **[!UICONTROL Type]** de données : Affiche le nombre de [!DNL Classifications]personnes sélectionnées.
* **[!UICONTROL Planification]**: Affiche la fréquence de synchronisation des [!DNL Classifications] données.

Une fois que vous avez passé en revue votre flux de données, cliquez sur **[!UICONTROL Terminer]** et accordez un certain temps à la création du flux de données.

![](../../../../images/tutorials/create/classifications/review.png)

## Surveiller le flux de données de vos classifications

Une fois que votre flux de données a été créé, vous pouvez surveiller les données qui y sont ingérées. Dans l’écran **[!UICONTROL Catalogue]** , sélectionnez **[!UICONTROL Flux de données]** pour vue d’une liste de flux établis associés à votre [!DNL Classifications] compte.

![](../../../../images/tutorials/create/classifications/dataflows.png)

L’écran **[!UICONTROL Flux de données]** s’affiche. Cette page contient une liste de flux de données, y compris des informations sur leur nom, leurs données source et leur état d&#39;exécution. Le panneau **[!UICONTROL Propriétés]** , situé à droite, contient des métadonnées relatives au flux de [!DNL Classifications] données.

Sélectionnez le jeu **[!UICONTROL de données de]** Cible auquel vous souhaitez accéder.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

La page activité **[!UICONTROL des]** jeux de données affiche des informations sur le jeu de données de cible que vous avez sélectionné, y compris des détails sur son statut de lot, son ID de jeu de données et son schéma.

>[!IMPORTANT]
>
>Bien que la suppression de jeux de données soit possible pour d’autres connecteurs source, elle n’est actuellement pas prise en charge pour le connecteur de données des classifications Analytics. Si vous supprimez un jeu de données par erreur, contactez le service à la clientèle Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur de données de classifications Analytics qui permet d’importer [!DNL Classifications] des données [!DNL Platform]. See the following documents for more information on [!DNL Analytics] and [!DNL Classifications] data:

* [Présentation du connecteur de données Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Création d’un connecteur de données Analytics dans l’interface utilisateur](./analytics.md)
* [À propos des classifications](https://docs.adobe.com/content/help/fr-FR/analytics/components/classifications/c-classifications.html#)
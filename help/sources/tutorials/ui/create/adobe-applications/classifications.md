---
keywords: Experience Platform;accueil;rubriques les plus consultées ; analytics;classifications
description: Découvrez comment créer un connecteur source Adobe Analytics dans l’interface utilisateur pour importer des données de classification dans Adobe Experience Platform.
solution: Experience Platform
title: Création d’une connexion source Adobe Analytics pour les données de classification dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 11%

---

# Création d’une connexion source Adobe Analytics pour les données de classification dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion à la source de données Adobe Analytics Classifications dans l’interface utilisateur afin d’importer des données de classification dans Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform fournit des environnements de test virtuels qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Le connecteur de données des classifications Analytics nécessite que vos données aient été migrées vers la nouvelle infrastructure [!DNL Classifications] d’Adobe Analytics avant d’être utilisées. Pour confirmer l’état de migration de vos données, contactez votre Adobe Customer Success Manager.

## Sélectionner vos classifications

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail des sources. L’écran **[!UICONTROL Catalogue]** affiche les sources disponibles pour créer des connexions entrantes avec . Chaque carte source affiche une option permettant de configurer un nouveau compte ou d’ajouter des données à un compte existant.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Adobe d’applications]** , sélectionnez la carte **[!UICONTROL Adobe Analytics]** , puis sélectionnez **[!UICONTROL Ajouter des données]** pour commencer à utiliser les données des classifications Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

L’étape **[!UICONTROL Ajout de données à la source Analytics]** s’affiche. Sélectionnez **[!UICONTROL Classifications]** dans l’en-tête supérieur pour afficher la liste des jeux de données [!DNL Classifications], y compris des informations sur leur ID de dimension, le nom de la suite de rapports et l’ID de la suite de rapports.

Chaque page affiche jusqu’à dix jeux de données [!DNL Classifications] différents parmi lesquels vous pouvez choisir. Sélectionnez **[!UICONTROL Suivant]** au bas de la page pour rechercher d’autres options. Le panneau de droite affiche le nombre total de jeux de données [!DNL Classifications] que vous avez sélectionnés, ainsi que leurs noms. Ce panneau vous permet également de supprimer tous les jeux de données [!DNL Classifications] que vous avez peut-être sélectionnés par erreur ou d’effacer toutes les sélections avec une seule action.

Vous pouvez sélectionner jusqu’à 30 jeux de données [!DNL Classifications] différents à importer dans [!DNL Platform].

Une fois que vous avez sélectionné vos jeux de données [!DNL Classifications], sélectionnez **[!UICONTROL Suivant]** en haut à droite de la page.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Vérification des classifications

L’étape **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de revoir vos [!DNL Classifications] jeux de données sélectionnés avant qu’ils ne soient créés. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : Affiche la plateforme source et l’état de la connexion.
* **[!UICONTROL Type]** de données : Affiche le nombre de  [!DNL Classifications]sélectionnés.
* **[!UICONTROL Planification]** : Affiche la fréquence de synchronisation des  [!DNL Classifications] données.

Une fois que vous avez examiné votre flux de données, cliquez sur **[!UICONTROL Terminer]** et laissez un certain temps pour que le flux de données soit créé.

![](../../../../images/tutorials/create/classifications/review.png)

## Surveillance du flux de données des classifications

Une fois votre flux de données créé, vous pouvez surveiller les données qui sont ingérées par celui-ci. Dans l’écran **[!UICONTROL Catalogue]**, sélectionnez **[!UICONTROL Flux de données]** pour afficher la liste des flux établis associés à votre compte [!DNL Classifications].

![](../../../../images/tutorials/create/classifications/dataflows.png)

L’écran **[!UICONTROL Flux de données]** s’affiche. Cette page contient une liste de flux de données, y compris des informations sur leur nom, les données source et l’état d’exécution de flux de données. À droite, se trouve le panneau **[!UICONTROL Propriétés]** qui contient des métadonnées concernant votre flux de données [!DNL Classifications].

Sélectionnez le **[!UICONTROL jeu de données cible]** auquel vous souhaitez accéder.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

La page **[!UICONTROL Activité du jeu de données]** affiche des informations sur le jeu de données cible que vous avez sélectionné, y compris des détails sur son état de lot, son identifiant de jeu de données et son schéma.

>[!IMPORTANT]
>
>Bien que la suppression de jeux de données soit possible pour dʼautres connecteurs source, elle nʼest actuellement pas prise en charge pour le Connecteur de classifications Analytics. Si vous supprimez un jeu de données par erreur, contactez lʼassistance clientèle Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Étapes suivantes

En suivant ce tutoriel, vous avez créé un connecteur de données Analytics Classifications qui récupère les données [!DNL Classifications] dans [!DNL Platform]. Consultez les documents suivants pour plus d’informations sur les données [!DNL Analytics] et [!DNL Classifications] :

* [Présentation du connecteur de données Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Création d’une connexion aux données Analytics dans l’interface utilisateur](./analytics.md)
* [À propos des classifications](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=fr)

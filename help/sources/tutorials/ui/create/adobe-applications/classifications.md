---
keywords: Experience Platform ; accueil ; sujets populaires ; analytics;classifications
description: Découvrez comment créer un connecteur source Adobe Analytics dans l’interface utilisateur pour importer des données de classification dans Adobe Experience Platform.
solution: Experience Platform
title: Création d’une connexion source Adobe Analytics pour les données des classifications dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 5%

---

# Création d’une connexion source Adobe Analytics pour les données de classification dans l’interface utilisateur

Ce didacticiel décrit les étapes à suivre pour créer une connexion de source de données de classifications Adobe Analytics dans l’interface utilisateur afin d’importer des données de classification dans Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Le connecteur de données des classifications Analytics nécessite que vos données aient été migrées vers la nouvelle infrastructure [!DNL Classifications] d’Adobe Analytics avant d’être utilisées. Pour confirmer l’état de migration de vos données, contactez votre responsable de succès client Adobe.

## Sélectionner vos classifications

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail sources. L’écran **[!UICONTROL Catalogue]** affiche les sources disponibles pour créer des connexions entrantes avec. Chaque carte source affiche une option permettant de configurer un nouveau compte ou d’ajouter des données à un compte existant.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Adobe applications]**, sélectionnez la carte **[!UICONTROL Adobe Analytics]**, puis **[!UICONTROL Ajouter les données]** au début d’utilisation des données de classification Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

L’étape **[!UICONTROL Ajout de données à la source Analytics]** s’affiche. Sélectionnez **[!UICONTROL Classifications]** dans l&#39;en-tête supérieur pour afficher une liste de [!DNL Classifications] jeux de données, y compris des informations sur leur ID de dimension, le nom de la suite de rapports et l&#39;identifiant de la suite de rapports.

Chaque page affiche jusqu&#39;à dix jeux de données [!DNL Classifications] différents parmi lesquels vous pouvez choisir. Sélectionnez **[!UICONTROL Suivant]** en bas de la page pour rechercher d’autres options. Le panneau de droite affiche le nombre total de jeux de données [!DNL Classifications] que vous avez sélectionnés, ainsi que leurs noms. Ce panneau vous permet également de supprimer tous les jeux de données [!DNL Classifications] sélectionnés par erreur ou d&#39;effacer toutes les sélections à l&#39;aide d&#39;une seule action.

Vous pouvez sélectionner jusqu’à 30 jeux de données [!DNL Classifications] différents à importer dans [!DNL Platform].

Une fois que vous avez sélectionné vos [!DNL Classifications] jeux de données, sélectionnez **[!UICONTROL Suivant]** en haut à droite de la page.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Vérifier vos classifications

L&#39;étape **[!UICONTROL Réviser]** s&#39;affiche, ce qui vous permet de revoir vos [!DNL Classifications] jeux de données sélectionnés avant de les créer. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : Affiche la plate-forme source et l&#39;état de la connexion.
* **[!UICONTROL Type]** de données : Affiche le nombre de  [!DNL Classifications]personnes sélectionnées.
* **[!UICONTROL Planification]** : Affiche la fréquence de synchronisation des  [!DNL Classifications] données.

Une fois que vous avez passé en revue votre flux de données, cliquez sur **[!UICONTROL Terminer]** et attendez un certain temps pour que le flux de données soit créé.

![](../../../../images/tutorials/create/classifications/review.png)

## Surveiller le flux de données de vos classifications

Une fois que votre flux de données a été créé, vous pouvez surveiller les données qui y sont ingérées. Dans l&#39;écran **[!UICONTROL Catalogue]**, sélectionnez **[!UICONTROL Flux de données]** pour vue une liste de flux établis associés à votre compte [!DNL Classifications].

![](../../../../images/tutorials/create/classifications/dataflows.png)

L&#39;écran **[!UICONTROL Flux de données]** s&#39;affiche. Cette page contient une liste de flux de données, y compris des informations sur leur nom, leurs données source et leur état d&#39;exécution. Sur la droite se trouve le panneau **[!UICONTROL Propriétés]** qui contient des métadonnées concernant votre flux de données [!DNL Classifications].

Sélectionnez le **[!UICONTROL jeu de données de Cible]** auquel vous souhaitez accéder.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

La page **[!UICONTROL activité des ensembles de données]** affiche des informations sur le jeu de données de cible que vous avez sélectionné, y compris des détails sur son état de lot, son ID de jeu de données et son schéma.

>[!IMPORTANT]
>
>Bien que la suppression de jeux de données soit possible pour d’autres connecteurs source, elle n’est actuellement pas prise en charge pour le connecteur de données des classifications Analytics. Si vous supprimez un jeu de données par erreur, contactez le service à la clientèle Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur de données de classifications Analytics qui permet d’importer [!DNL Classifications] des données dans [!DNL Platform]. Pour plus d&#39;informations sur les données [!DNL Analytics] et [!DNL Classifications], consultez les documents suivants :

* [Présentation du connecteur de données Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Création d’une connexion aux données Analytics dans l’interface utilisateur](./analytics.md)
* [À propos des classifications](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)

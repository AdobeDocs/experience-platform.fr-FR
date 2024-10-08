---
description: Découvrez comment créer un connecteur source Adobe Analytics dans l’interface utilisateur pour importer des données de classification dans Adobe Experience Platform.
title: Création d’une connexion Adobe Analytics Source pour les données de classification dans l’interface utilisateur
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: 02b5c5f963c21247adbb1d13114f92b22f8758de
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 15%

---

# Créer une connexion source Adobe Analytics pour les données de classification dans l’interface utilisateur

>[!TIP]
>
>Par défaut, les données de classification d’Adobe Analytics sont mises à jour toutes les semaines. L’ingestion de données pour vos données de classification sera traitée sept jours après la configuration initiale de votre flux de données. Le premier chargement ingère l’ensemble des données et l’ingestion hebdomadaire qui en résulte exécute des données incrémentielles.

Lisez ce tutoriel pour savoir comment ingérer vos données de classification Adobe Analytics dans Adobe Experience Platform par le biais de l’interface utilisateur.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Le connecteur source des classifications Analytics nécessite que vos données aient été migrées vers la nouvelle infrastructure de classifications d’Adobe Analytics avant d’être utilisées. Pour confirmer l’état de migration de vos données, contactez votre équipe de compte d’Adobe.

## Sélectionner vos classifications

Dans l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie *Adobe applications*, sélectionnez **[!UICONTROL Adobe Analytics]**, puis **[!UICONTROL Configurer]**.

>[!TIP]
>
>Les sources dans le catalogue des sources affichent l’option **[!UICONTROL Configurer]** s’il n’existe aucun compte authentifié. Une fois qu’un compte est authentifié, l’option devient **[!UICONTROL Ajouter des données]**.

![Catalogue des sources dans l’interface utilisateur de l’Experience Platform avec la source Adobe Analytics sélectionnée.](../../../../images/tutorials/create/classifications/catalog.png)

Sélectionnez ensuite [!UICONTROL Classifications] et sélectionnez les jeux de données de classification à ingérer à l’Experience Platform.

Vous pouvez sélectionner jusqu’à 30 jeux de données de classifications différents à importer dans Experience Platform. Tous les jeux de données que vous sélectionnez s’affichent dans le rail de droite. Lorsque vous avez terminé, sélectionnez [!UICONTROL Suivant] pour continuer.

![Page de classifications avec plusieurs jeux de données de classifications sélectionnés.](../../../../images/tutorials/create/classifications/select.png)

## Vérification des classifications

L’étape **[!UICONTROL Réviser]** s’affiche, vous permettant de passer en revue les jeux de données de classification sélectionnés avant qu’ils ne soient créés. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche la plateforme source et l’état de la connexion.
* **[!UICONTROL Type de données]** : affiche le nombre de classifications sélectionnées.
* **[!UICONTROL Planification]** : affiche la fréquence de synchronisation des données de classification. **Remarque** : les données des classifications sont mises à jour chaque semaine.

Une fois que vous avez examiné votre flux de données, cliquez sur **[!UICONTROL Terminer]** et laissez un certain temps pour créer le flux de données.

![Page de révision des données de classification Adobe Analytics.](../../../../images/tutorials/create/classifications/review.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un connecteur de données de classification Analytics qui apporte des données de classification dans Experience Platform. Consultez les documents suivants pour plus d’informations sur [!DNL Analytics] et les données de classification :

* [Présentation du connecteur source Adobe Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Création d’une connexion source Analytics pour les données de suite de rapports dans l’interface utilisateur](./analytics.md)
* [À propos des classifications](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)

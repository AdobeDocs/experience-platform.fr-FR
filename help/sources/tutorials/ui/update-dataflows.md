---
keywords: Experience Platform;accueil;rubriques les plus consultées;mettre à jour les flux de données;modifier la planification
description: Ce tutoriel décrit les étapes de mise à jour d’un planning de flux de données, y compris sa fréquence d’ingestion et son taux d’intervalle, à l’aide de l’espace de travail Sources .
solution: Experience Platform
title: Mise à jour d’un flux de données de connexion source dans l’interface utilisateur
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: cef5c203acf3318445399669336166e6627ebe66
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 13%

---

# Mise à jour des flux de données dans l’interface utilisateur

Ce tutoriel vous explique comment mettre à jour un flux de données existant, y compris sa planification et son mappage, à l’aide de l’espace de travail des sources.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Mettre à jour des flux de données {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Expiration du jeu de données"
>abstract="Cette colonne indique le nombre de jours restants au jeu de données cible avant son expiration automatique.<br>Un flux de données échoue si le jeu de données cible expire. Pour éviter l’échec d’un flux de données, assurez-vous qu’un jeu de données cible est défini pour expirer à la date correcte. Consultez la documentation pour savoir comment mettre à jour les dates d’expiration."

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Sélectionner **[!UICONTROL Flux de données]** dans l’en-tête supérieur pour afficher une liste des flux de données existants.

![catalogue](../../images/tutorials/update-dataflows/catalog.png)

Le [!UICONTROL Flux de données] contient une liste de tous les flux de données existants, y compris des informations sur leur jeu de données cible, leur source et leur nom de compte correspondant.

Pour trier la liste, sélectionnez l’icône de filtre ![filter](../../images/tutorials/update/filter.png) en haut à gauche pour utiliser le panneau de tri.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Le panneau de tri fournit une liste de toutes les sources disponibles. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de flux de données appartenant à différentes sources.

Sélectionnez la source que vous souhaitez utiliser pour afficher la liste de ses flux de données existants. Une fois que vous avez identifié le flux de données à mettre à jour, sélectionnez les ellipses (`...`) en regard du nom du flux de données.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Un menu déroulant s’affiche, vous fournissant des options permettant de mettre à jour le flux de données que vous avez sélectionné. À partir de là, vous pouvez choisir de mettre à jour les jeux de mappages et le planning d’ingestion d’un flux de données. Vous pouvez également sélectionner des options pour inspecter le flux de données dans le tableau de bord de surveillance, vous abonner à des alertes et désactiver ou supprimer le flux de données.

Pour mettre à jour les informations de votre flux de données, sélectionnez **[!UICONTROL Mise à jour du flux de données]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### Ajouter des données

L’étape [!UICONTROL Ajouter les données] apparaît. Sélectionnez le format de données approprié pour examiner le contenu des données sélectionnées, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Détails du flux de données

Dans le [!UICONTROL Détails du flux de données] , vous pouvez fournir un nom et une description mis à jour pour votre flux de données et reconfigurer le seuil d’erreur de votre flux de données. Au cours de cette étape, vous pouvez également configurer ou modifier les paramètres de votre abonnement aux alertes.

Une fois les valeurs mises à jour fournies, sélectionnez **[!UICONTROL Suivant]**.

![dataflow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Mappage

>[!NOTE]
>
>La fonction de modification du mappage n’est actuellement pas prise en charge pour les sources suivantes : Adobe Analytics, Adobe Audience Manager, API HTTP et [!DNL Marketo Engage].

Le [!UICONTROL Mappage] vous fournit une interface dans laquelle vous pouvez ajouter et supprimer des jeux de mappages associés à votre flux de données.

L’interface de mappage affiche le jeu de mappage existant de votre flux de données et non un nouveau jeu de mappage recommandé. Les mises à jour du mappage ne sont appliquées qu’aux exécutions de flux de données planifiées à l’avenir. Les jeux de mappages d’un flux de données planifié pour une ingestion unique ne peuvent pas être mis à jour.

À partir de là, vous pouvez utiliser l’interface de mappage pour modifier les jeux de mappages appliqués à votre flux de données. Pour obtenir des instructions complètes sur l’utilisation de l’interface de mappage, reportez-vous à la section [guide de l’interface utilisateur de la préparation de données](../../../data-prep/ui/mapping.md) pour plus d’informations.

![mappage](../../images/tutorials/update-dataflows/mapping.png)

### Planification

Le [!UICONTROL Planification] s’affiche, ce qui vous permet de mettre à jour le planning d’ingestion de votre flux de données et d’ingérer automatiquement les données source sélectionnées avec les mappages mis à jour.

>[!NOTE]
>
>Vous ne pouvez pas replanifier un flux de données planifié pour une ingestion unique.

![new-schedule](../../images/tutorials/update-dataflows/new-schedule.png)

Vous pouvez également mettre à jour le planning d’ingestion de votre flux de données à l’aide de l’option de mise à jour en ligne fournie dans la page des flux de données.

Dans la page des flux de données, sélectionnez les ellipses (`...`) en regard du nom du flux de données, puis sélectionnez **[!UICONTROL Modifier le planning]** dans le menu déroulant qui s’affiche.

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

Le **[!UICONTROL Modifier le planning]** La boîte de dialogue vous fournit des options permettant de mettre à jour la fréquence d’ingestion et le taux d’intervalle de votre flux de données. Une fois que vous avez défini les valeurs de fréquence et d’intervalle mises à jour, sélectionnez **[!UICONTROL Enregistrer]**.

![planning-pop-up](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Réviser

Le **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de consulter votre flux de données avant qu’il ne soit mis à jour.

Une fois que vous avez examiné votre flux de données, sélectionnez **[!UICONTROL Terminer]** et laisser un certain temps au flux de données avec les nouveaux jeux de mappage à créer.

![review](../../images/tutorials/update-dataflows/review.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé avec succès la méthode [!UICONTROL Sources] espace de travail pour mettre à jour le planning d’ingestion et les jeux de mappage de votre flux de données.

Pour savoir comment effectuer ces opérations par programmation à l’aide de la méthode [!DNL Flow Service] API, reportez-vous au tutoriel sur [mise à jour des flux de données à l’aide de l’API Flow Service](../../tutorials/api/update-dataflows.md).

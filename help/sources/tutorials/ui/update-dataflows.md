---
keywords: Experience Platform;accueil;rubriques les plus consultées;mettre à jour les flux de données;modifier la planification
description: Ce tutoriel décrit les étapes de mise à jour d’un planning de flux de données, y compris sa fréquence d’ingestion et son taux d’intervalle, à l’aide de l’espace de travail Sources .
solution: Experience Platform
title: Mise à jour d’un flux de données de connexion source dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 7%

---

# Mise à jour des flux de données dans l’interface utilisateur

Ce tutoriel vous explique comment mettre à jour un flux de données de sources existantes, y compris des informations sur la modification d’un planning de flux de données et le mappage, à l’aide de l’espace de travail [!UICONTROL Sources] .

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources](../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
- [Environnements de test](../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Modification du mapping

>[!NOTE]
>
>La fonction de modification du mappage n’est actuellement pas prise en charge pour les sources suivantes : Adobe Analytics, Adobe Audience Manager, API HTTP et [!DNL Marketo Engage].

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Sélectionnez **[!UICONTROL Flux de données]** dans l’en-tête supérieur pour afficher une liste des flux de données existants.

![catalogue](../../images/tutorials/update-dataflows/catalog.png)

La page [!UICONTROL Flux de données] contient une liste de tous les flux de données existants, y compris des informations sur leur état d’exécution, leur date de dernière exécution et leur nom de compte.

Sélectionnez l’icône de filtre ![filter](../../images/tutorials/update/filter.png) en haut à gauche pour lancer le panneau de tri.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Le panneau de tri fournit une liste de toutes les sources disponibles. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de flux de données appartenant à différentes sources.

Sélectionnez la source que vous souhaitez utiliser pour afficher la liste de ses flux de données existants. Une fois que vous avez identifié le flux de données à mettre à jour, sélectionnez les points de suspension (`...`) en regard du nom du compte.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Un menu déroulant s’affiche, vous fournissant des options permettant de mettre à jour le flux de données que vous avez sélectionné. À partir de là, vous pouvez choisir de mettre à jour les jeux de mappages et le planning d’ingestion d’un flux de données. Vous pouvez également sélectionner des options pour inspecter le flux de données dans le tableau de bord de surveillance, ainsi que désactiver ou supprimer le flux de données.

Sélectionnez **[!UICONTROL Modifier la source]** pour mettre à jour son mapping.

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

L’étape [!UICONTROL Ajouter les données] apparaît. Sélectionnez le format de données approprié pour examiner le contenu des données sélectionnées, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

La page [!UICONTROL Mapping] vous fournit une interface dans laquelle vous pouvez ajouter et supprimer des jeux de mappages associés à votre jeu de données.

>[!TIP]
>
>Les mises à jour du mappage ne sont appliquées qu’aux exécutions de flux de données planifiées à l’avenir.

Sélectionnez **[!UICONTROL Ajouter un nouveau mappage]** pour ajouter un nouveau jeu de mappages.

![add-new-mapping](../../images/tutorials/update-dataflows/add-new-mapping.png)

Ensuite, saisissez l’attribut de champ source approprié et les valeurs de champ XDM cible pour terminer votre jeu de mappage supplémentaire. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![new-mapping-added](../../images/tutorials/update-dataflows/new-mapping-added.png)

L’étape [!UICONTROL Planification] s’affiche, ce qui vous permet de mettre à jour le planning d’ingestion de votre flux de données et d’ingérer automatiquement les données source sélectionnées avec les mappages mis à jour.

>[!NOTE]
>
>Vous ne pouvez pas mettre à jour les jeux de mappages pour les flux de données qui ont été planifiés pour une ingestion unique et l’heure de début se trouvent dans le passé.

![scheduling](../../images/tutorials/update-dataflows/scheduling.png)

Sur la page [!UICONTROL Détails du flux de données] , vous pouvez fournir un nom et une description mis à jour pour votre flux de données et reconfigurer le seuil d’erreur de votre flux de données.

Une fois les valeurs mises à jour fournies, sélectionnez **[!UICONTROL Suivant]**.

![dataflow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

L’étape **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de revoir votre flux de données avant qu’il ne soit mis à jour.

Une fois que vous avez examiné votre flux de données, sélectionnez **[!UICONTROL Terminer]** et laissez un certain temps au flux de données avec les nouveaux jeux de mappage à créer.

![review](../../images/tutorials/update-dataflows/review.png)

## Modifier le planning

Pour modifier le planning d’ingestion d’un flux de données existant, sélectionnez les ellipses (`...`) en regard d’un nom de flux de données, puis sélectionnez **[!UICONTROL Modifier le planning]** dans le menu déroulant.

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

La boîte de dialogue **[!UICONTROL Modifier le planning]** vous fournit des options pour mettre à jour la fréquence d’ingestion et le taux d’intervalle de votre flux de données. Une fois que vous avez défini les valeurs de fréquence et d’intervalle mises à jour, sélectionnez **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Vous ne pouvez pas replanifier un flux de données planifié pour une ingestion unique.

![schedule-dialog-box](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| Planification | Description |
| ---------- | ----------- |
| Fréquence | Fréquence à laquelle le flux de données collectera les données. Les valeurs acceptables pour la modification du planning de fréquence pour un flux de données existant sont les suivantes : `minute`, `hour`, `day` ou `week`. |
| Intervalle | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un entier non nul et doit être supérieure ou égale à `15`. |

Au bout de quelques instants, une boîte de confirmation s’affiche en bas de l’écran pour confirmer une mise à jour réussie.

![schedule-confirm](../../images/tutorials/update-dataflows/schedule-confirm.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé l’espace de travail [!UICONTROL Sources] pour mettre à jour le planning d’ingestion et les jeux de mappages de votre flux de données.

Pour savoir comment effectuer ces opérations par programmation à l’aide de l’API [!DNL Flow Service], reportez-vous au tutoriel sur la [mise à jour des flux de données à l’aide de l’API Flow Service](../../tutorials/api/update-dataflows.md).

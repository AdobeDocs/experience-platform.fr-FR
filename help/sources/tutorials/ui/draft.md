---
title: Créer des brouillons de flux de données dans l’interface utilisateur
description: Découvrez comment enregistrer vos flux de données en tant que brouillon et les publier ultérieurement, lorsque vous utilisez l’espace de travail des sources.
exl-id: ee00798e-152a-4618-acb3-db40f2f55fae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 3%

---

# Créer des brouillons de flux de données dans l’interface utilisateur

Enregistrez la progression de votre workflow d’ingestion de données non terminé en définissant votre flux de données sur le statut de brouillon. Vous pouvez reprendre et terminer votre brouillon de flux de données ultérieurement.

Ce document décrit la procédure à suivre pour enregistrer vos flux de données lors de l’utilisation de l’espace de travail des sources dans l’interface utilisateur de Adobe Experience Platform.

## Commencer

Ce document nécessite une compréhension du fonctionnement des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.

## Enregistrer un flux de données en tant que brouillon

Vous pouvez suspendre à tout moment la progression de la création de votre flux de données après avoir sélectionné les données que vous allez importer dans Experience Platform.

Par exemple, si vous souhaitez enregistrer votre progression au cours de l’étape Détails du flux de données, sélectionnez **[!UICONTROL Enregistrer en tant que brouillon]**.

![L’étape Détails du flux de données du workflow des sources avec l’option Enregistrer en tant que brouillon sélectionnée.](../../images/tutorials/draft/save-as-draft.png)

Une fois que vous avez enregistré votre brouillon, vous accédez à la page de votre compte, où vous pouvez voir la liste de vos flux de données existants, y compris vos brouillons.

![Liste des flux de données pour un compte donné.](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>Les brouillons de flux de données ne seront pas activés et leur statut sera défini sur `draft`.

Pour continuer avec votre brouillon, sélectionnez les points de suspension (`...`) à côté du nom de votre flux de données, puis sélectionnez **[!UICONTROL Mettre à jour le flux de données]**.

>[!NOTE]
>
>Si votre brouillon contient des informations de planification, la fenêtre déroulante vous offre également la possibilité de **[!UICONTROL Modifier le planning]**.

![Une fenêtre déroulante avec le flux de données de mise à jour sélectionné.](../../images/tutorials/draft/update-dataflow.png)

### Accéder à vos brouillons à partir du catalogue source

Vous pouvez également accéder à vos brouillons de flux de données par le biais du catalogue de flux de données. Sélectionnez **[!UICONTROL Flux de données]** dans l’en-tête supérieur pour accéder au catalogue des flux de données. À partir de là, recherchez votre brouillon dans la liste des flux de données existants de votre organisation, sélectionnez les points de suspension (`...`) à côté de son nom, puis sélectionnez **[!UICONTROL Mettre à jour le flux de données]**.

![Liste des flux de données pour une organisation donnée.](../../images/tutorials/draft/catalog-access.png)

## Publier votre brouillon de flux de données

Vous revenez à l’étape [!UICONTROL Ajouter des données] du workflow des sources, où vous pouvez confirmer à nouveau le format de vos données et continuer à progresser sur votre flux de données.

Une fois que vous avez confirmé le type de mise en forme, de délimiteur et de compression de vos données, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Étape d’ajout de données du workflow des sources.](../../images/tutorials/draft/select-data.png)

Ensuite, confirmez les détails de votre flux de données. Utilisez l’interface Détails du flux de données pour mettre à jour les configurations entourant le nom, la description, l’ingestion partielle, les paramètres de diagnostic d’erreur et les préférences d’alerte de votre flux de données.

Une fois les configurations terminées, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Étape des détails du flux de données du workflow des sources.](../../images/tutorials/draft/dataflow-detail.png)

L’étape [!UICONTROL Mappage] apparaît. Au cours de cette étape, vous pouvez reconfigurer les configurations de mappage de votre flux de données. Pour obtenir un guide complet sur les fonctions de préparation des données utilisées pour le mappage, consultez le [guide de l’interface utilisateur de la préparation des données](../../../data-prep/ui/mapping.md).

Une fois la reconfiguration du mappage terminée, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Étape de mappage du workflow des sources.](../../images/tutorials/draft/mapping.png)

Utilisez l’étape [!UICONTROL Planification] pour établir une planification d’ingestion pour votre flux de données. Vous pouvez définir la fréquence d’ingestion sur `once`, `minute`, `hour`, `day` ou `week`. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Étape de planification du workflow des sources.](../../images/tutorials/draft/scheduling.png)

Enfin, passez en revue les détails de votre flux de données, puis sélectionnez **[!UICONTROL Terminer]** pour publier le brouillon.

![Étape de révision du workflow des sources.](../../images/tutorials/draft/review.png)

Une fois que vous avez enregistré et publié un brouillon, le flux de données est activé et vous ne pouvez plus le réinitialiser en tant que brouillon.

## Étapes suivantes

En suivant attentivement ce tutoriel, vous avez appris à enregistrer votre progression et à définir un flux de données en tant que brouillon. Pour plus d’informations sur les sources, consultez la [présentation des sources](../../home.md).

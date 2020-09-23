---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;API;api;
title: Guide du développeur du service de segmentation Adobe Experience Platform
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 6%

---


# Guide du développeur d’ [!DNL Segmentation Service] API Adobe Experience Platform

[!DNL Adobe Experience Platform Segmentation Service] vous permet de créer des segments et de générer des audiences dans [!DNL Adobe Experience Platform] à partir de vos [!DNL Real-time Customer Profile] données.

L’ [!DNL Segmentation Service] API fournit plusieurs points de terminaison qui vous permettent de gérer par programmation vos opérations de segmentation dans [!DNL Experience Platform]. Ce document d’aperçu fournit des introductions de haut niveau à chacun de ces points de terminaison et des liens vers les guides de points de terminaison qui leur sont associés pour plus de détails. Avant de lire les guides des points de terminaison individuels, consultez le guide [de](./getting-started.md) prise en main pour obtenir des informations importantes sur les en-têtes requis, la lecture d’exemples d’appels d’API, etc.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, reportez-vous à la référence [de l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)Segmentation Service.

## Tâches d’exportation

Tâches d’exportation sont des processus asynchrones utilisés pour conserver les membres de segments d’audience dans les jeux de données. Vous pouvez utiliser le `/export/jobs` point de terminaison pour récupérer toutes les tâches d’exportation, créer une tâche d’exportation, récupérer les détails d’une tâche d’exportation spécifique ou annuler une tâche d’exportation spécifique.

For more information on using this endpoint, please read the [export jobs endpoint guide](./export-jobs.md).

## Prévisualisations et estimations

Les prévisualisations fournissent une liste paginée de profils qualifiants pour une définition de segment, ce qui vous permet de comparer les résultats à ce que vous attendez. Vous pouvez utiliser le `/preview` point de terminaison pour créer une tâche de prévisualisation ou rechercher les résultats d’une tâche de prévisualisation spécifique.

Les estimations fournissent des informations statistiques pour les définitions de segment, telles que la taille d’audience estimée, l’intervalle de confiance et l’écart-type d’erreur. Vous pouvez utiliser le `/estimate` point de terminaison pour vue une estimation d&#39;une définition de segment.

Pour plus d&#39;informations sur l&#39;utilisation de ces points de terminaison, veuillez lire le guide [des](./previews-and-estimates.md)prévisualisations et des estimations des points de terminaison.

## Plannings

Les calendriers sont un outil qui permet d&#39;exécuter automatiquement des tâches de segmentation par lots une fois par jour. Vous pouvez utiliser le `/config/schedules` point de terminaison pour récupérer une liste de planifications, créer une nouvelle planification, récupérer les détails d&#39;une planification spécifique, mettre à jour une planification spécifique ou supprimer une planification spécifique.

For more information on using this endpoint, please read the [schedules endpoint guide](./schedules.md).

## Définitions de segment

Les définitions de segment définissent les profils qui feront partie des segments d’audience. Vous pouvez utiliser le `/segment/definitions` point de terminaison pour gérer les définitions de segment.

For more information on using this endpoint, please read the [segment definitions endpoint guide](./segment-definitions.md).

## Tâches de segmentation

Les tâches de segmentation traitent les définitions de segmentation préalablement établies pour générer un segment d’audience. Vous pouvez utiliser le `/segment/jobs` point de terminaison pour gérer les tâches de segmentation.

For more information on using this endpoint, please read the [segment jobs endpoint guide](./segment-jobs.md).

## Recherche de segments

La recherche de segments permet de rechercher des champs contenus dans diverses sources de données et de les renvoyer en temps quasi réel. Pour commencer à utiliser la recherche de segments, reportez-vous au guide des points de terminaison de [recherche](segment-search.md)

## Étapes suivantes

Pour commencer à utiliser l’ [!DNL Segmentation Service] API, consultez les différents guides de points de terminaison pour obtenir des instructions détaillées sur la façon d’appeler les différents points de terminaison du service. To learn more about working with segments using the [!DNL Platform] UI, see the [Segmentation user guide](../ui/overview.md).
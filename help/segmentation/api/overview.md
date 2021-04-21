---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; API ; api ;
title: Guide de l’API du service de segmentation
topic-legacy: guide
description: L’API Segmentation Service permet aux développeurs de gérer par programmation les opérations de segmentation dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 6%

---

# Guide de l’API du service de segmentation

[!DNL Adobe Experience Platform Segmentation Service] vous permet de créer des segments et de générer des audiences à  [!DNL Adobe Experience Platform] partir de vos  [!DNL Real-time Customer Profile] données.

L&#39;API [!DNL Segmentation Service] fournit plusieurs points de terminaison qui vous permettent de gérer par programmation vos opérations de segmentation dans [!DNL Experience Platform]. Ce document d’aperçu fournit des introductions de haut niveau à chacun de ces points de terminaison et des liens vers les guides de points de terminaison qui leur sont associés pour plus de détails. Avant de lire les guides des points de terminaison individuels, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, consultez la [référence API du service de segmentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Tâches d’exportation

Tâches d’exportation sont des processus asynchrones utilisés pour conserver les membres de segments d’audience dans les jeux de données. Vous pouvez utiliser le point de terminaison `/export/jobs` pour récupérer toutes les tâches d’exportation, créer une tâche d’exportation, récupérer les détails d’une tâche d’exportation spécifique ou annuler une tâche d’exportation spécifique.

Pour plus d&#39;informations sur l&#39;utilisation de ce point de terminaison, consultez le [guide du point de terminaison des tâches d&#39;exportation](./export-jobs.md).

## Prévisualisations et estimations

Les prévisualisations fournissent une liste paginée de profils qualifiants pour une définition de segment, ce qui vous permet de comparer les résultats à ce que vous attendez. Vous pouvez utiliser le point de terminaison `/preview` pour créer une tâche de prévisualisation ou rechercher les résultats d&#39;une tâche de prévisualisation spécifique.

Les estimations fournissent des informations statistiques pour les définitions de segment, telles que la taille d’audience estimée, l’intervalle de confiance et l’écart-type d’erreur. Vous pouvez utiliser le point de terminaison `/estimate` pour vue une estimation d&#39;une définition de segment.

Pour plus d&#39;informations sur l&#39;utilisation de ces points de terminaison, consultez le [guide des prévisualisations et des estimations des points de terminaison](./previews-and-estimates.md).

## Plannings

Les calendriers sont un outil qui permet d&#39;exécuter automatiquement des tâches de segmentation par lots une fois par jour. Vous pouvez utiliser le point de terminaison `/config/schedules` pour récupérer une liste de planifications, créer une nouvelle planification, récupérer les détails d&#39;une planification spécifique, mettre à jour une planification spécifique ou supprimer une planification spécifique.

Pour plus d&#39;informations sur l&#39;utilisation de ce point de terminaison, consultez le [guide des points de terminaison planifiés](./schedules.md).

## Définitions de segment

Les définitions de segment définissent les profils qui feront partie des segments d’audience. Vous pouvez utiliser le point de terminaison `/segment/definitions` pour gérer les définitions de segment.

Pour plus d&#39;informations sur l&#39;utilisation de ce point de terminaison, consultez le [guide des points de terminaison des définitions de segment](./segment-definitions.md).

## Tâches de segmentation

Les tâches de segmentation traitent les définitions de segmentation préalablement établies pour générer un segment d’audience. Vous pouvez utiliser le point de terminaison `/segment/jobs` pour gérer les tâches de segment.

Pour plus d&#39;informations sur l&#39;utilisation de ce point de terminaison, consultez le [guide des points de terminaison des tâches de segment](./segment-jobs.md).

## Recherche de segments

La recherche de segments permet de rechercher des champs contenus dans diverses sources de données et de les renvoyer en temps quasi réel. Pour commencer à utiliser la recherche de segments, consultez le [guide des points de terminaison de la recherche](segment-search.md)

## Étapes suivantes

Pour commencer à utiliser l&#39;API [!DNL Segmentation Service], consultez les différents guides de points de terminaison pour obtenir des instructions détaillées sur la façon d&#39;appeler les différents points de terminaison du service. Pour en savoir plus sur l’utilisation des segments à l’aide de l’[!DNL Platform] interface utilisateur, consultez le [Guide de l’utilisateur de la segmentation](../ui/overview.md).

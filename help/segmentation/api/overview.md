---
title: Guide de l’API Segmentation Service
description: L’API Segmentation Service permet aux développeurs de gérer par programmation les opérations de segmentation dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: af79493c831c401c0bf14e391eb36a8175b4a2dd
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 4%

---

# Guide de l’API Segmentation Service

Adobe Experience Platform [!DNL Segmentation Service] vous permet de créer des audiences par le biais de définitions de segment ou d’autres sources dans Adobe Experience Platform à partir de vos données [!DNL Real-Time Customer Profile].

L’API [!DNL Segmentation Service] fournit plusieurs points d’entrée qui vous permettent de gérer par programmation vos opérations de segmentation dans [!DNL Experience Platform]. Ce document de présentation fournit des présentations générales de chacun de ces points d’entrée et des liens vers les guides des points d’entrée associés pour plus d’informations. Avant de lire les guides des points d’entrée individuels, reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture des exemples d’appels API, etc.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, reportez-vous à la [référence de l’API Segmentation Service](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Audiences

Les audiences sont un ensemble de personnes qui partagent des comportements et/ou des caractéristiques similaires. Ils peuvent être générés à l’aide d’Experience Platform ou à partir de sources externes. Vous pouvez utiliser le point d’entrée `/audiences` pour récupérer toutes les audiences, créer une nouvelle audience, récupérer les détails d’une audience spécifique, mettre à jour une audience spécifique ou supprimer une audience spécifique.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le [guide des points d’entrée des audiences](./audiences.md).

## Tâches d’exportation

Les tâches d’exportation sont des processus asynchrones utilisés pour conserver les membres des segments d’audience dans les jeux de données. Vous pouvez utiliser le point d’entrée `/export/jobs` pour récupérer toutes les tâches d’exportation, créer une tâche d’exportation, récupérer les détails d’une tâche d’exportation spécifique ou annuler une tâche d’exportation spécifique.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le [ guide des points d’entrée des tâches d’exportation](./export-jobs.md).

## Audiences externes

Vous pouvez importer des audiences externes dans Experience Platform, récupérer le statut de création d’une audience, mettre à jour une audience externe, démarrer une exécution d’ingestion d’audience, récupérer un statut d’ingestion d’audience externe, répertorier les exécutions d’ingestion d’audience et supprimer une audience externe à l’aide du point d’entrée `/core/ais/external-audiences`.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le [guide des points d’entrée des audiences externes](./external-audiences.md).

## Aperçus et estimations

Les aperçus fournissent une liste paginée de profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats par rapport à vos attentes. Vous pouvez utiliser le point d’entrée `/preview` pour créer une tâche de prévisualisation ou rechercher les résultats d’une tâche de prévisualisation spécifique.

Les estimations fournissent des informations statistiques pour les définitions de segment, telles que la taille d’audience prévisionnelle, l’intervalle de confiance et l’écart type d’erreur. Vous pouvez utiliser le point d’entrée `/estimate` pour afficher une estimation d’une définition de segment.

Pour plus d’informations sur l’utilisation de ces points d’entrée, consultez le guide des points d’entrée [aperçus et estimations](./previews-and-estimates.md).

## Plannings

Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des traitements de segmentation par lots une fois par jour. Vous pouvez utiliser le point d’entrée `/config/schedules` pour récupérer une liste de planifications, créer une nouvelle planification, récupérer les détails d’une planification spécifique, mettre à jour une planification spécifique ou supprimer une planification spécifique.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le [guide des points d’entrée planifiés](./schedules.md).

## Définitions de segment

Les définitions de segment définissent les profils qui feront partie de chaque audience. Vous pouvez utiliser le point d’entrée `/segment/definitions` pour gérer les définitions de segment.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le [ guide des points d’entrée des définitions de segment](./segment-definitions.md).

## Tâches de segmentation

Les tâches de segmentation traitent les définitions de segment précédemment établies pour générer une audience. Vous pouvez utiliser le point d’entrée `/segment/jobs` pour gérer les tâches de segmentation.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le guide [guide des points d’entrée des tâches de segment](./segment-jobs.md).

## Recherche de segments

La recherche de segments permet de rechercher des champs contenus dans différentes sources de données et de les renvoyer en temps quasi réel. Pour commencer à utiliser la recherche de segments, consultez le guide [point d’entrée de recherche](segment-search.md)

## Étapes suivantes

Pour commencer à utiliser l’API [!DNL Segmentation Service], consultez les guides des différents points d’entrée pour obtenir des instructions détaillées sur la manière d’effectuer des appels vers les différents points d’entrée du service. Pour en savoir plus sur l’utilisation des segments à l’aide de l’interface utilisateur de [!DNL Experience Platform], consultez le guide d’utilisation [Segmentation](../ui/overview.md).

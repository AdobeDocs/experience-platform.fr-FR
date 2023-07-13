---
title: Guide de l’API Segmentation Service
description: L’API Segmentation Service permet aux développeurs de gérer par programmation les opérations de segmentation dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 5%

---

# Guide de l’API Segmentation Service

Adobe Experience Platform [!DNL Segmentation Service] vous permet de créer des audiences par le biais de définitions de segment ou d’autres sources dans Adobe Experience Platform à partir de vos [!DNL Real-Time Customer Profile] data.

Le [!DNL Segmentation Service] L’API fournit plusieurs points de terminaison qui vous permettent de gérer par programmation vos opérations de segmentation dans [!DNL Experience Platform]. Ce document de présentation présente de manière détaillée chacun de ces points de terminaison et fournit des liens vers les guides des points de terminaison associés pour plus de détails. Avant de lire les guides des différents points de terminaison, reportez-vous à la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, lire des exemples d’appels API, etc.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, reportez-vous à la section [Référence de l’API Segmentation Service](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Audiences

Les audiences sont un ensemble de personnes qui partagent des comportements et/ou des caractéristiques similaires. Ils peuvent être générés à l’aide de Platform ou à partir de sources externes. Vous pouvez utiliser la variable `/audiences` point d’entrée pour récupérer toutes les audiences, créer une audience, récupérer les détails d’une audience spécifique, mettre à jour une audience spécifique ou supprimer une audience spécifique.

Pour plus d’informations sur l’utilisation de ce point de terminaison, veuillez lire la section [guide de point de terminaison d’audiences](./audiences.md).

## Tâches d’exportation

Les tâches d’exportation sont des processus asynchrones utilisés pour conserver les membres du segment d’audience dans des jeux de données. Vous pouvez utiliser la variable `/export/jobs` point de fin pour récupérer toutes les tâches d’exportation, créer une tâche d’exportation, récupérer les détails d’une tâche d’exportation spécifique ou annuler une tâche d’exportation spécifique.

Pour plus d’informations sur l’utilisation de ce point de terminaison, veuillez lire la section [guide de point de fin des traitements d’export](./export-jobs.md).

## Aperçus et estimations

Les aperçus fournissent une liste paginée de profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats à ce que vous attendez. Vous pouvez utiliser la variable `/preview` point de terminaison pour créer une tâche de prévisualisation ou rechercher les résultats d’une tâche de prévisualisation spécifique.

Les estimations fournissent des informations statistiques sur les définitions de segment, telles que la taille prévue de l’audience, l’intervalle de confiance et l’écart type d’erreur. Vous pouvez utiliser la variable `/estimate` point d’entrée pour afficher une estimation d’une définition de segment.

Pour plus d’informations sur l’utilisation de ces points de terminaison, veuillez lire la section [guide d’aperçu et de point de fin d’estimation](./previews-and-estimates.md).

## Plannings

Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des tâches de segmentation par lots une fois par jour. Vous pouvez utiliser la variable `/config/schedules` point de fin pour récupérer une liste de plannings, créer un nouveau planning, récupérer les détails d’un planning spécifique, mettre à jour un planning spécifique ou supprimer un planning spécifique.

Pour plus d’informations sur l’utilisation de ce point de terminaison, veuillez lire la section [guide de point de fin planifications](./schedules.md).

## Définitions de segment

Les définitions de segment définissent les profils qui feront partie de l’audience. Vous pouvez utiliser la variable `/segment/definitions` point d’entrée pour gérer les définitions de segment.

Pour plus d’informations sur l’utilisation de ce point de terminaison, veuillez lire la section [guide d’entrée des définitions de segment](./segment-definitions.md).

## Tâches de segmentation

Les tâches de segmentation traitent les définitions de segment précédemment établies pour générer une audience. Vous pouvez utiliser la variable `/segment/jobs` point de terminaison pour gérer les tâches de segmentation.

Pour plus d’informations sur l’utilisation de ce point de terminaison, veuillez lire la section [guide de point de fin des tâches de segmentation](./segment-jobs.md).

## Recherche de segments

La recherche de segments permet de rechercher des champs contenus dans diverses sources de données et de les renvoyer en temps quasi réel. Pour commencer à utiliser la recherche de segments, reportez-vous à la section [guide de point de terminaison de recherche](segment-search.md)

## Étapes suivantes

Pour commencer à utiliser la méthode [!DNL Segmentation Service] API, passez en revue les différents guides des points de terminaison pour obtenir des instructions détaillées sur la manière d’effectuer des appels vers les différents points de terminaison du service. Pour en savoir plus sur l’utilisation des segments à l’aide de la variable [!DNL Platform] Dans l’interface utilisateur, reportez-vous à la section [Guide d’utilisation de la segmentation](../ui/overview.md).

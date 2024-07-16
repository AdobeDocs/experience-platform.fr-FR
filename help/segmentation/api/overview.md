---
title: Guide de l’API Segmentation Service
description: L’API Segmentation Service permet aux développeurs de gérer par programmation les opérations de segmentation dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 5%

---

# Guide de l’API Segmentation Service

Adobe Experience Platform [!DNL Segmentation Service] vous permet de créer des audiences par le biais de définitions de segment ou d’autres sources dans Adobe Experience Platform à partir de vos données [!DNL Real-Time Customer Profile].

L’API [!DNL Segmentation Service] fournit plusieurs points de terminaison qui vous permettent de gérer par programmation vos opérations de segmentation dans [!DNL Experience Platform]. Ce document de présentation présente de manière détaillée chacun de ces points de terminaison et fournit des liens vers les guides des points de terminaison associés pour plus de détails. Avant de lire les guides des différents points de terminaison, reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d’exemples d’appels API, etc.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, reportez-vous à la [référence de l’API Segmentation Service](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Audiences

Les audiences sont un ensemble de personnes qui partagent des comportements et/ou des caractéristiques similaires. Ils peuvent être générés à l’aide de Platform ou à partir de sources externes. Vous pouvez utiliser le point d’entrée `/audiences` pour récupérer toutes les audiences, créer une nouvelle audience, récupérer les détails d’une audience spécifique, mettre à jour une audience spécifique ou supprimer une audience spécifique.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [guide du point de terminaison d’audience](./audiences.md).

## Tâches d’exportation

Les tâches d’exportation sont des processus asynchrones utilisés pour conserver les membres du segment d’audience dans des jeux de données. Vous pouvez utiliser le point de terminaison `/export/jobs` pour récupérer toutes les tâches d’exportation, créer une tâche d’exportation, récupérer les détails d’une tâche d’exportation spécifique ou annuler une tâche d’exportation spécifique.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [guide de point de terminaison des tâches d’exportation](./export-jobs.md).

## Aperçus et estimations

Les aperçus fournissent une liste paginée de profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats à ce que vous attendez. Vous pouvez utiliser le point d’entrée `/preview` pour créer une tâche de prévisualisation ou rechercher les résultats d’une tâche de prévisualisation spécifique.

Les estimations fournissent des informations statistiques sur les définitions de segment, telles que la taille prévue de l’audience, l’intervalle de confiance et l’écart type d’erreur. Vous pouvez utiliser le point d’entrée `/estimate` pour afficher une estimation d’une définition de segment.

Pour plus d’informations sur l’utilisation de ces points de terminaison, consultez le [guide d’aperçu et d’estimation des points de terminaison](./previews-and-estimates.md).

## Plannings

Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des tâches de segmentation par lots une fois par jour. Vous pouvez utiliser le point de terminaison `/config/schedules` pour récupérer une liste de planifications, créer une planification, récupérer les détails d’une planification spécifique, mettre à jour une planification spécifique ou supprimer une planification spécifique.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [guide de point de terminaison de plannings](./schedules.md).

## Définitions de segment

Les définitions de segment définissent les profils qui feront partie de l’audience. Vous pouvez utiliser le point d’entrée `/segment/definitions` pour gérer les définitions de segment.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [ guide du point de terminaison des définitions de segment](./segment-definitions.md).

## Tâches de segmentation

Les tâches de segmentation traitent les définitions de segment précédemment établies pour générer une audience. Vous pouvez utiliser le point d’entrée `/segment/jobs` pour gérer les tâches de segmentation.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [guide de point de terminaison des tâches de segmentation](./segment-jobs.md).

## Recherche de segments

La recherche de segments permet de rechercher des champs contenus dans diverses sources de données et de les renvoyer en temps quasi réel. Pour commencer à utiliser la recherche de segments, consultez le [guide de point de terminaison de recherche](segment-search.md)

## Étapes suivantes

Pour commencer à utiliser l’API [!DNL Segmentation Service], consultez les différents guides des points de terminaison pour obtenir des instructions détaillées sur la manière d’effectuer des appels aux différents points de terminaison du service. Pour en savoir plus sur l’utilisation des segments à l’aide de l’interface utilisateur [!DNL Platform], consultez le [guide d’utilisation de la segmentation](../ui/overview.md).

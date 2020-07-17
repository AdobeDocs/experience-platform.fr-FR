---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un segment
topic: tutorial
translation-type: tm+mt
source-git-commit: c0eacfba2feea66803e63ed55ad9d0a97e9ae47c
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 67%

---


# Création d’un segment

This document provides a tutorial for developing, testing, previewing, and saving a segment definition using the [DNL Adobe Experience Platform Segmentation Service API](../api/getting-started.md).

Pour plus d’informations sur la création de segments à l’aide de l’interface utilisateur, consultez le [guide du créateur de segments](../ui/overview.md).

## Prise en main

This tutorial requires a working understanding of the various [!DNL Adobe Experience Platform] services involved in creating audience segments. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [!DNL Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [!DNL Adobe Experience Platform Segmentation Service](../home.md) : permet de créer des segments d’audience à partir de données Real-time Customer Profile.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Platform] APIs.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Développement d’une définition de segment

La première étape de la segmentation consiste à définir un segment, représenté dans un concept appelé **définition de segment**. A segment definition is an object that encapsulates a query written in [!DNL Profile Query Language] (PQL). Cet objet est également appelé **prédicat PQL**. Les prédicats PQL définissent les règles du segment en fonction des conditions liées aux données d’enregistrement ou de série temporelle que vous fournissez à [!DNL Real-time Customer Profile]. Pour plus d’informations sur l’écriture de requêtes PQL, reportez-vous au [guide de PQL](../pql/overview.md).

Vous pouvez créer une nouvelle définition de segment en envoyant une requête POST au point de terminaison `/segment/definitions` de l’API [!DNL Segmentation] L’exemple suivant illustre la manière de formater une requête de définition, et inclut les informations requises pour qu’un segment soit défini avec succès.

Pour une explication détaillée sur la définition d&#39;un segment, consultez le guide [du développeur de définitions de](../api/segment-definitions.md#create)segment.

## Estimation et prévisualisation d’une audience {#estimate-and-preview-an-audience}

As you develop your segment definition, you can use the estimate and preview tools within [!DNL Real-time Customer Profile] to view summary-level information to help ensure you are isolating the expected audience. Les estimations fournissent des informations statistiques sur une définition de segment telles que la taille prévue de l’audience et l’intervalle de confiance. Les prévisualisations fournissent des listes paginées des profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats avec vos attentes.

En estimant et en prévisualisant votre audience, vous pouvez tester et optimiser vos prédicats PQL jusqu’à ce qu’ils produisent un résultat souhaitable. Ils peuvent alors être utilisés dans une définition de segment mise à jour.

Deux étapes sont nécessaires pour prévisualiser ou obtenir une estimation de votre segment :

1. [Création d’une tâche de prévisualisation](#create-a-preview-job)
2. [Afficher l’estimation ou la prévisualisation](#view-an-estimate-or-preview) à l’aide de l’identifiant de la tâche de prévisualisation

### Comment sont générées les estimations

Des exemples de données sont utilisés pour évaluer les segments et estimer le nombre de profils admissibles. De nouvelles données sont chargées dans la mémoire chaque matin (entre 0 h et 2 h PT, soit entre 7 h et 9 h UTC) et toutes les requêtes de segmentation sont estimées à l’aide des exemples de données de cette journée. Par conséquent, tous les nouveaux champs ajoutés ou toutes les données supplémentaires recueillies seront pris en compte dans les estimations du lendemain.

La taille de l’échantillon dépend du nombre total d’entités dans votre banque de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Les estimations durent généralement entre 10 et 15 secondes. L’estimation est d’abord approximative, et se précise au fur et à mesure de la lecture d’un plus grand nombre d’enregistrements.

### Création d’une tâche de prévisualisation

Vous pouvez créer une nouvelle tâche de prévisualisation en exécutant une requête POST sur le point de terminaison `/preview`.

Vous trouverez des instructions détaillées sur la création d&#39;une tâche de prévisualisation dans le guide [des](../api/previews-and-estimates.md#create-preview)prévisualisations et des estimations des points de terminaison.

### Affichage d’une estimation ou d’une prévisualisation

Les processus d’estimation et de prévisualisation sont exécutés de manière asynchrone, car le temps de traitement peut différer d’une requête à une autre. Une fois qu’une requête a été lancée, vous pouvez utiliser des appels API pour récupérer (GET) l’état actuel de l’estimation ou de la prévisualisation au fur et à mesure de sa progression.

Using the [!DNL Segmentation Service] API, you can look up a preview job&#39;s current state by its ID. Si l’état affiche « RESULT_READY », vous pouvez consulter les résultats. Pour connaître l&#39;état actuel d&#39;une tâche de prévisualisation, lisez la section sur la [](../api/previews-and-estimates.md#get-preview) récupération d&#39;une tâche de prévisualisation dans le guide des points de terminaison des prévisualisations et des estimations. Pour connaître l&#39;état actuel d&#39;un travail d&#39;estimation, veuillez lire la section sur la [récupération d&#39;un travail](../api/previews-and-estimates.md#get-estimate) d&#39;estimation dans le guide des prévisualisations et des points de terminaison d&#39;estimation.


## Étapes suivantes

Once you have developed, tested, and saved your segment definition, you can create a segment job to build an audience using the [!DNL Segmentation Service] API. Consultez le tutoriel portant sur l’[évaluation et l’accès aux résultats des segments](./evaluate-a-segment.md) pour obtenir des instructions détaillées sur la manière d’y parvenir.
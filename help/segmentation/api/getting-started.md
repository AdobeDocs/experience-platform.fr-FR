---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de Segmentation Service
topic: developer guide
translation-type: tm+mt
source-git-commit: c0eacfba2feea66803e63ed55ad9d0a97e9ae47c
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 46%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Le service de segmentation des Adobes Experience Platform vous permet de créer des segments et de générer des audiences dans l’Adobe Experience Platform à partir de vos [!DNL Real-time Customer Profile] données.

The developer guide requires a working understanding of the various Experience Platform services involved with using [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md) : permet de créer des segments d’audience à partir de données Real-time Customer Profile.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
- [!DNL Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Environnements de test](../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

The following sections provide additional information that you will need to know in order to successfully work with the [!DNL Segmentation] API.

## Lecture d’exemples d’appels API

The [!DNL Segmentation Service] API documentation provides example API calls to demonstrate how to format your requests. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](../../tutorials/authentication.md) pour lancer des appels vers des points de terminaison Platform. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox in which the operation will take place:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on working with sandboxes in [!DNL Experience Platform], see the [sandboxes overview documentation](../../sandboxes/home.md).

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md). -->

## Définitions de segment

Les définitions de segment définissent les profils qui feront partie des segments d’audience. Vous pouvez utiliser le `/segment/definitions` point de terminaison pour récupérer une liste de définitions de segment, créer une définition de segment, récupérer les détails d’une définition de segment spécifique, supprimer une définition de segment spécifique ou remplacer les détails d’une définition de segment spécifique.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md).

## Tâches de segmentation

Les tâches de segmentation traitent les définitions de segmentation préalablement établies pour générer un segment d’audience. Vous pouvez utiliser le point de terminaison `/segment/jobs` pour obtenir une liste des tâches de segmentation, créer une tâche de segments, récupérer les détails d’une tâche de segmentation spécifique ou la supprimer.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [guide de développement de tâches de segmentation](./segment-jobs.md).

## Recherche de segments

La recherche de segments permet de rechercher et d’indexer des champs configurables contenus dans diverses sources de données et de les renvoyer en temps quasi réel. Pour commencer à utiliser la recherche de segments, consultez le guide du développeur de [recherche](segment-search.md)

## Étapes suivantes

Pour passer des appels à l’aide de l’ [!DNL Segmentation Service] API, sélectionnez l’un des guides de point de terminaison disponibles à l’aide du volet de navigation de gauche ou dans l’aperçu du guide du [développeur.](./overview.md)
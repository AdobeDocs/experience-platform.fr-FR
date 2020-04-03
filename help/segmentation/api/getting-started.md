---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur du service de segmentation
topic: developer guide
translation-type: tm+mt
source-git-commit: 38762fa57188ed018c4347c07765f3d09daef2e6

---


# Guide du développeur du service de segmentation

La segmentation vous permet de créer des segments et de générer   dans Adobe Experience Platform à partir de vos données de client en temps réel.

## Prise en main

Ce guide nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l’utilisation de la segmentation.

- [Segmentation](../home.md): Permet de créer  segments  à partir de données de client en temps réel.
- [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
- [](../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
- [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour utiliser correctement la segmentation à l’aide de l’API.

### Lecture des exemples d’appels d’API

La documentation de l’API du service de segmentation fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### En-têtes obligatoires

La documentation de l’API exige également que vous ayez suivi le didacticiel [d’](../../tutorials/authentication.md) authentification afin d’effectuer des appels vers les points de fin de plateforme. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : `Bearer {ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>**Remarque :** Pour plus d’informations sur l’utilisation de sandbox dans Experience Platform, voir la documentation [d’aperçu des](../../sandboxes/home.md)sandbox.

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

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md).

## Segment definitions

Segment definitions define which profiles will be part of which audience segments. You can use the `/segment/definitions` endpoint to retrieve a list of segment definitions, create a new segment definition, retrieve details of a specific segment definition, delete a specific segment definition, or overwrite details of a specific segment definition.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md). -->

## Tâches de segment

Les tâches de segmentation traitent les définitions de segment précédemment établies pour générer un segment  de . Vous pouvez utiliser le `/segment/jobs` point de fin pour récupérer un de tâches de segment, créer une tâche de segment, récupérer les détails d’une tâche de segment spécifique ou supprimer une tâche de segment spécifique.

Pour plus d’informations sur l’utilisation de ce point de fin, consultez le guide [du développeur de tâches de](./segment-jobs.md)segment.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API de segmentation, sélectionnez l’un des sous-guides pour savoir comment utiliser des points de fin de segmentation spécifiques. Pour en savoir plus sur l’utilisation des segments à l’aide de l’interface utilisateur de la plateforme, consultez le guide [de l’utilisateur](../ui/overview.md)Segmentation.
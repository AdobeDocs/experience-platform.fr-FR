---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;Catalog
solution: Experience Platform
title: Guide de développement du service de catalogue
topic: developer guide
description: Ce guide de développement fournit des étapes pour vous aider à commencer à utiliser l’API Catalog. Ce guide fournit aussi des exemples d’appels API pour réaliser des opérations clés à l’aide du catalogue.
translation-type: tm+mt
source-git-commit: c8e53a25c5b22e8d840658fe26ff47875947a6d0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 55%

---


# [!DNL Catalog Service] guide du développeur

[!DNL Catalog Service] est le système d’enregistrement de l’emplacement et de la lignée des données dans Adobe Experience Platform. [!DNL Catalog] agit comme un magasin de métadonnées ou un &quot;catalogue&quot; dans lequel vous pouvez trouver des informations sur vos données [!DNL Experience Platform], sans avoir à accéder aux données proprement dites. Pour plus d’informations, consultez la [[!DNL Catalog] présentation des ](../home.md).

Ce guide du développeur décrit les étapes à suivre pour vous aider à démarrer l’API [!DNL Catalog]. The guide then provides sample API calls for performing key operations using [!DNL Catalog].

## Conditions préalables 

[!DNL Catalog] effectue le suivi des métadonnées pour plusieurs types de ressources et d’opérations au sein de [!DNL Experience Platform]. This developer guide requires a working understanding of the various [!DNL Experience Platform] services involved with creating and managing these resources:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
* [Ingestion par lots](../../ingestion/batch-ingestion/overview.md)[!DNL Experience Platform] : méthode d’ingestion et de stockage de données de fichiers, par exemple de type CSV et Parquet, dans 
* [Ingestion par flux](../../ingestion/streaming-ingestion/overview.md)[!DNL Experience Platform] : méthode d’ingestion et de stockage de données en temps réel dans à partir de périphériques côté client et côté serveur.

The following sections provide additional information that you will need to know or have on-hand in order to successfully make calls to the [!DNL Catalog Service] API.

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](../../tutorials/authentication.md). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Best practices for [!DNL Catalog] API calls

When performing GET requests to the [!DNL Catalog] API, best practice is to include query parameters in your requests in order to return only the objects and properties that you need. Les requêtes non filtrées peuvent entraîner des payloads de réponse supérieurs à 3 Go, ce qui peut ralentir les performances globales.

Vous pouvez afficher des objets spécifiques en incluant leurs identifiants dans le chemin d’accès à la requête ou utiliser des paramètres de requête tels que `properties` et `limit` pour filtrer les réponses. Les filtres peuvent être transmis sous forme d’en-têtes et de paramètres de requête, les filtres transmis sous forme de paramètres de requête prévalant sur les autres. Pour plus d’informations, consultez le document sur le [filtrage des données du catalogue](filter-data.md).

Since some queries can put a heavy load on the API, global limits have been implemented on [!DNL Catalog] queries to further support best practices.

## Étapes suivantes

This document covered the prerequisite knowledge required to make calls to the [!DNL Catalog] API. Vous pouvez désormais procéder aux appels d’échantillon fournis dans ce guide de développement à suivre avec leurs instructions.

Most of the examples in this guide use the `/dataSets` endpoint, but the principles can be applied to other endpoints within [!DNL Catalog] (such as `/batches` and `/accounts`). Consultez la [référence de l’API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) pour obtenir une liste complète de tous les appels et opérations disponibles pour chaque point de terminaison.

For a step-by-step workflow that demonstrates how the [!DNL Catalog] API is involved with data ingestion, see the tutorial on [creating a dataset](../datasets/create.md).

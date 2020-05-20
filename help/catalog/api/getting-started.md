---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur de Catalog Service
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Guide du développeur de Catalog Service

Catalog Service est le système d’enregistrement de l’emplacement et du lignage des données dans Adobe Experience Platform. Le catalogue agit en tant que magasin de métadonnées ou &quot;catalogue&quot; où vous pouvez trouver des informations sur vos données dans la plate-forme d’expérience, sans avoir à accéder aux données proprement dites. See the [Catalog overview](../home.md) for more information.

Ce guide du développeur décrit les étapes à suivre pour vous aider à début à l’aide de l’API Catalogue. Le guide fournit ensuite des exemples d’appels d’API pour effectuer des opérations clés à l’aide du catalogue.

## Conditions préalables

Le catalogue effectue le suivi des métadonnées pour plusieurs types de ressources et d’opérations dans la plate-forme d’expérience. Ce guide du développeur nécessite une bonne compréhension des différents services de la plateforme d’expérience impliqués dans la création et la gestion de ces ressources :

* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
* [Importation](../../ingestion/batch-ingestion/overview.md)par lot : Expérience Platform ingère et stocke des données à partir de fichiers de données, tels que CSV et Parquet.
* [Prise en charge](../../ingestion/streaming-ingestion/overview.md)en flux continu : Expérience Platform ingère et stocke en temps réel les données des périphériques client et serveur.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître ou connaître pour pouvoir invoquer l’API du service de catalogue.

## Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

## Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Recommandations relatives aux appels d’API de catalogue

Lors de l’exécution de requêtes GET sur l’API Catalog, il est recommandé d’inclure des paramètres de requête dans vos requêtes afin de renvoyer uniquement les objets et les propriétés dont vous avez besoin. Les requêtes non filtrées peuvent entraîner une charge utile de réponse dépassant 3 Go, ce qui peut ralentir les performances globales.

Vous pouvez vue d’objets spécifiques en incluant leur identifiant dans le chemin d’accès à la requête ou utiliser des paramètres de requête tels que `properties` et `limit` pour filtrer les réponses. Les Filtres peuvent être transmis en tant qu’en-têtes et en tant que paramètres de requête, les paramètres transmis en tant que paramètres de requête étant prioritaires. Pour plus d’informations, voir le document sur le [filtrage des données](filter-data.md) du catalogue.

Comme certaines requêtes peuvent imposer une charge importante à l’API, des limites globales ont été mises en oeuvre sur les requêtes de catalogue afin de mieux prendre en charge les meilleures pratiques.

## Étapes suivantes

Ce document couvrait les connaissances préalables requises pour effectuer des appels à l’API du catalogue. Vous pouvez maintenant passer aux exemples d’appels fournis dans ce guide du développeur et suivre leurs instructions.

La plupart des exemples de ce guide utilisent le `/dataSets` point de terminaison, mais les principes peuvent être appliqués à d’autres points de terminaison dans le catalogue (tels que `/batches` et `/accounts`). Consultez la référence [de l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalog Service pour obtenir une liste complète de tous les appels et opérations disponibles pour chaque point de terminaison.

Pour un flux de travail détaillé qui montre comment l’API Catalog est impliquée dans l’assimilation de données, consultez le didacticiel sur la [création d’un jeu de données](../datasets/create.md).

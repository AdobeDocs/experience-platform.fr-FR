---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur du service de catalogue
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Guide du développeur du service de catalogue

Le service de catalogue est le système d’enregistrement de l’emplacement et de la lignée des données dans Adobe Experience Platform. Le catalogue agit comme un magasin de métadonnées ou un &quot;catalogue&quot; dans lequel vous pouvez trouver des informations sur vos données dans la plate-forme d’expérience, sans avoir à accéder aux données elles-mêmes. See the [Catalog overview](../home.md) for more information.

Ce guide du développeur décrit les étapes à suivre pour vous aider à  à l’aide de l’API de catalogue. Le guide fournit ensuite des exemples d’appels d’API pour effectuer des opérations clés à l’aide du catalogue.

## Conditions préalables

Le catalogue effectue le suivi des métadonnées pour plusieurs types de ressources et d’opérations dans la plateforme d’expérience. Ce guide du développeur nécessite une compréhension pratique des différents services de la plateforme d’expérience impliqués dans la création et la gestion de ces ressources :

* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.
* [Importation](../../ingestion/batch-ingestion/overview.md)par lot : Méthode d’assimilation et de stockage des données des fichiers de données, tels que CSV et Parquet.
* [Prise en charge](../../ingestion/streaming-ingestion/overview.md)en flux continu : Expérience Platform assimile et stocke en temps réel les données des périphériques client et serveur.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître ou connaître pour pouvoir effectuer des appels vers l’API du service de catalogue.

## Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

## Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Recommandations relatives aux appels d’API de catalogue

Lors de l’exécution de requêtes GET dans l’API de catalogue, il est recommandé d’inclure des paramètres  dans vos requêtes afin de renvoyer uniquement les objets et les propriétés dont vous avez besoin. Les requêtes non filtrées peuvent entraîner une charge utile de réponse dépassant 3 Go, ce qui peut ralentir les performances globales.

Vous pouvez des objets spécifiques en incluant leur ID dans le chemin d’accès à la requête ou utiliser des paramètres de tels que `properties` et `limit` pour filtrer les réponses. Les  de peuvent être transmises sous forme d’en-têtes et de paramètres , les paramètres transmis sous forme de paramètres  de l’. Pour plus d’informations, reportez-vous au  sur le [filtrage des données](filter-data.md) du catalogue.

Comme certains peuvent imposer une charge importante à l’API, des limites globales ont été mises en oeuvre sur le de catalogue pour  prendre en charge davantage les meilleures pratiques.

## Étapes suivantes

Ce  couvrait les connaissances préalables requises pour effectuer des appels à l’API de catalogue. Vous pouvez maintenant accéder aux exemples d’appels fournis dans ce guide du développeur et suivre leurs instructions.

La plupart des exemples de ce guide utilisent le `/dataSets` point de fin, mais les principes peuvent être appliqués à d’autres points de fin du catalogue (tels `/batches` et `/accounts`). Voir la référence [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalog Service pour obtenir un complet de tous les appels et opérations disponibles pour chaque point de fin.

Pour un flux de travail détaillé qui montre comment l’API de catalogue est impliquée dans l’assimilation de données, consultez le didacticiel sur la [création d’un jeu](../datasets/create.md)de données.

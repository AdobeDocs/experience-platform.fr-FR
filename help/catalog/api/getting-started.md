---
keywords: Experience Platform ; accueil ; rubriques populaires ; service catalogue ; catalogue ; service catalogue ; Catalogue
solution: Experience Platform
title: Guide de l’API du service de catalogue
topic-legacy: developer guide
description: L’API Catalog Service permet aux développeurs de gérer les métadonnées de jeux de données dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 47%

---

# [!DNL Catalog Service] Guide des API

[!DNL Catalog Service] est le système d’enregistrement de l’emplacement et de la lignée des données dans Adobe Experience Platform. [!DNL Catalog] agit comme un magasin de métadonnées ou un &quot;catalogue&quot; dans lequel vous pouvez trouver des informations sur vos données  [!DNL Experience Platform], sans avoir à accéder aux données proprement dites. Pour plus d’informations, consultez [[!DNL Catalog] aperçu des ](../home.md).

Ce guide du développeur décrit les étapes à suivre pour vous aider à démarrer l’API [!DNL Catalog]. Le guide fournit ensuite des exemples d&#39;appels d&#39;API pour effectuer des opérations clés à l&#39;aide de [!DNL Catalog].

## Conditions préalables

[!DNL Catalog] effectue le suivi des métadonnées pour plusieurs types de ressources et d’opérations au sein de  [!DNL Experience Platform]. Ce guide du développeur nécessite une compréhension pratique des différents services [!DNL Experience Platform] impliqués dans la création et la gestion de ces ressources :

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
* [Ingestion par lots](../../ingestion/batch-ingestion/overview.md)[!DNL Experience Platform] : méthode d’ingestion et de stockage de données de fichiers, par exemple de type CSV et Parquet, dans 
* [Prise en charge](../../ingestion/streaming-ingestion/overview.md) en flux continu : Comment  [!DNL Experience Platform] ingère et stocke les données des périphériques client et serveur en temps réel.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître ou connaître pour pouvoir invoquer l&#39;API [!DNL Catalog Service].

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Recommandations relatives aux appels d&#39;API [!DNL Catalog]

Lors de l&#39;exécution de requêtes de GET à l&#39;API [!DNL Catalog], il est recommandé d&#39;inclure des paramètres de requête dans vos requêtes afin de renvoyer uniquement les objets et les propriétés dont vous avez besoin. Les requêtes non filtrées peuvent entraîner des payloads de réponse supérieurs à 3 Go, ce qui peut ralentir les performances globales.

Vous pouvez afficher des objets spécifiques en incluant leurs identifiants dans le chemin d’accès à la requête ou utiliser des paramètres de requête tels que `properties` et `limit` pour filtrer les réponses. Les filtres peuvent être transmis sous forme d’en-têtes et de paramètres de requête, les filtres transmis sous forme de paramètres de requête prévalant sur les autres. Pour plus d’informations, consultez le document sur le [filtrage des données du catalogue](filter-data.md).

Comme certaines requêtes peuvent imposer une charge importante à l&#39;API, des limites globales ont été mises en oeuvre sur les requêtes [!DNL Catalog] afin de mieux prendre en charge les meilleures pratiques.

## Étapes suivantes

Ce document couvrait les connaissances préalables requises pour effectuer des appels à l&#39;API [!DNL Catalog]. Vous pouvez désormais procéder aux exemples d’appel fournis dans ce guide de développement et suivre leurs instructions.

La plupart des exemples de ce guide utilisent le point de terminaison `/dataSets`, mais les principes peuvent être appliqués à d&#39;autres points de terminaison dans [!DNL Catalog] (tels que `/batches` et `/accounts`). Consultez la [référence de l’API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) pour obtenir une liste complète de tous les appels et opérations disponibles pour chaque point de terminaison.

Pour un flux de travail détaillé qui montre comment l&#39;API [!DNL Catalog] est impliquée dans l&#39;assimilation de données, consultez le didacticiel sur la création d&#39;un jeu de données ](../datasets/create.md).[

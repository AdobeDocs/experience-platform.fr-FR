---
keywords: Experience Platform;accueil;rubriques populaires;service de catalogue;catalogue;service de catalogue;catalogue
solution: Experience Platform
title: Guide de l’API Catalog Service
topic-legacy: developer guide
description: L’API Catalog Service permet aux développeurs de gérer les métadonnées des jeux de données dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 58%

---

# Guide de l’API [!DNL Catalog Service]

Le [!DNL Catalog Service]est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. [!DNL Catalog] agit comme un magasin de métadonnées ou un &quot;catalogue&quot; dans lequel vous pouvez trouver des informations sur vos données  [!DNL Experience Platform], sans avoir à accéder aux données elles-mêmes. Pour plus d’informations, consultez la [[!DNL Catalog] présentation ](../home.md).

Ce guide du développeur décrit les étapes à suivre pour commencer à utiliser l&#39;API [!DNL Catalog]. Le guide fournit ensuite des exemples d’appels API pour effectuer des opérations clés à l’aide de [!DNL Catalog].

## Conditions préalables

[!DNL Catalog] effectue le suivi des métadonnées pour plusieurs types de ressources et d’opérations dans  [!DNL Experience Platform]. Ce guide de développement nécessite une compréhension pratique des différents services [!DNL Experience Platform] impliqués dans la création et la gestion de ces ressources :

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
* [Ingestion par lots](../../ingestion/batch-ingestion/overview.md)[!DNL Experience Platform] : méthode d’ingestion et de stockage de données de fichiers, par exemple de type CSV et Parquet, dans 
* [Ingestion par flux](../../ingestion/streaming-ingestion/overview.md) : Comment  [!DNL Experience Platform] ingère et stocke des données à partir de périphériques côté client et côté serveur en temps réel.

Les sections suivantes apportent des informations supplémentaires que vous devrez connaître ou dont vous devrez disposer pour passer avec succès des appels à l’API [!DNL Catalog Service].

## Lecture d&#39;exemples d&#39;appels API

Ce guide fournit des exemples d&#39;appels API pour démontrer comment formater vos requêtes. Il s&#39;agit notamment de chemins d&#39;accès, d&#39;en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Bonnes pratiques relatives aux appels d’API [!DNL Catalog]

Lors de l’exécution de requêtes de GET à l’API [!DNL Catalog], la bonne pratique consiste à inclure des paramètres de requête dans vos requêtes afin de renvoyer uniquement les objets et les propriétés dont vous avez besoin. Les requêtes non filtrées peuvent entraîner des payloads de réponse supérieurs à 3 Go, ce qui peut ralentir les performances globales.

Vous pouvez afficher des objets spécifiques en incluant leurs identifiants dans le chemin d’accès à la requête ou utiliser des paramètres de requête tels que `properties` et `limit` pour filtrer les réponses. Les filtres peuvent être transmis sous forme d’en-têtes et de paramètres de requête, les filtres transmis sous forme de paramètres de requête prévalant sur les autres. Pour plus d’informations, consultez le document sur le [filtrage des données du catalogue](filter-data.md).

Comme certaines requêtes peuvent imposer une charge importante à l’API, des limites globales ont été mises en oeuvre sur les requêtes [!DNL Catalog] afin de prendre davantage en charge les bonnes pratiques.

## Étapes suivantes

Ce document couvrait les connaissances préalables requises pour effectuer des appels à l’API [!DNL Catalog]. Vous pouvez désormais procéder aux exemples d&#39;appel fournis dans ce guide de développement et suivre leurs instructions.

La plupart des exemples de ce guide utilisent le point de terminaison `/dataSets`, mais les principes peuvent être appliqués à d’autres points de terminaison dans [!DNL Catalog] (comme `/batches` et `/accounts`). Consultez la [référence de l’API Catalog Service](https://www.adobe.io/experience-platform-apis/references/catalog/) pour obtenir une liste complète de tous les appels et opérations disponibles pour chaque point de terminaison.

Pour un processus détaillé qui montre comment l’API [!DNL Catalog] est impliquée dans l’ingestion de données, consultez le tutoriel sur la [création d’un jeu de données](../datasets/create.md).

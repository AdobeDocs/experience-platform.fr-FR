---
keywords: Experience Platform ; accueil ; rubriques populaires ; Adobe Experience Platform ; guide d’api ; guide d’api de la plate-forme ; présentation de la plate-forme ; guide du développeur
solution: Experience Platform
title: Prise en main des API Adobe Experience Platform
topic: api guide
description: Adobe Experience Platform fournit des services d’API étroitement liés les uns aux autres. Ce guide contient des informations sur les services disponibles, les en-têtes requis pour les opérations CRUD, les messages d’erreur, les collections Postman et les exemples d’appels d’API.
translation-type: tm+mt
source-git-commit: 85d2ae5ccf1b27baaafe839f1d3f00d588abe4fc
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 24%

---


# Prise en main des API Adobe Experience Platform

Adobe Experience Platform est développé selon la philosophie &quot;API first&quot;. Grâce aux API de plateformes, vous pouvez exécuter par programmation des opérations CRUD (Créer, Lire, Mettre à jour, Supprimer) de base sur des données, telles que la configuration d’attributs calculés, l’accès aux données/entités, l’exportation de données, la suppression de données ou de lots inutiles, etc.

Les API de chaque service d’Experience Platform partagent tous le même jeu d’en-têtes d’authentification et utilisent des syntaxes similaires pour leurs opérations CRUD. Le guide suivant décrit les étapes nécessaires pour commencer à utiliser les API de plateformes.

## Authentification et en-têtes

Pour réussir les appels aux points de terminaison de la plateforme, vous devez suivre le [didacticiel d&#39;authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### En-tête Sandbox

Dans Experience Platform, toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

- `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d’informations sur les environnements de test dans Platform, consultez la [documentation de présentation des environnements de test](../sandboxes/home.md).

### En-tête de type de contenu

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées sont spécifiques à chaque point de terminaison de l’API. Si une valeur `Content-Type` spécifique est nécessaire pour un point de terminaison, sa valeur est affichée dans l&#39;exemple de demandes d&#39;API fourni par les guides d&#39;API [pour les services de plateforme individuels](#api-guides).

## Principes de base de l’API Experience Platform

Les API Adobe Experience Platform utilisent plusieurs technologies et syntaxes sous-jacentes qui sont importantes à comprendre pour gérer efficacement les ressources de la plate-forme.

Pour en savoir plus sur les technologies d&#39;API sous-jacentes utilisées par la plateforme, y compris les exemples d&#39;objets de schéma JSON, consultez le [guide Experience Platform API fundamentals](api-fundamentals.md).

## Collections Postman pour les API Experience Platform

Postman est une plateforme de collaboration pour le développement d&#39;API qui vous permet de configurer des environnements avec des variables prédéfinies, de partager des collections d&#39;API, de rationaliser les demandes CRUD, etc. La plupart des services d’API de plate-forme disposent de collections Postman qui peuvent être utilisées pour faciliter les appels d’API.

Pour en savoir plus sur Postman, y compris sur la façon de configurer un environnement, une liste de collections disponibles et comment importer des collections, consultez la [documentation de Platform Postman](postman.md).

## Lecture d’exemples d’appels API {#sample-api}

Les formats de requête varient selon l’API de Platform utilisée. Le meilleur moyen d’apprendre à structurer vos appels API est de suivre les exemples fournis dans la documentation du service Platform que vous utilisez.

La documentation de [!DNL Experience Platform] présente des exemples d&#39;appels d&#39;API de deux manières différentes. Tout d’abord, l’appel est présenté dans son **format d’API**, qui consiste en une représentation de modèle affichant uniquement l’opération (GET, POST, PUT, PATCH, DELETE) et le point de terminaison utilisé (par exemple `/global/classes`). Certains modèles indiquent également l’emplacement des variables pour mieux illustrer la manière dont un appel doit être formulé, comme par exemple `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Les appels sont ensuite affichés sous forme de commandes cURL dans une **Requête**, qui comprend les en-têtes nécessaires et le « chemin racine » complet indispensable pour que l’interaction avec l’API soit réussie. Le chemin racine doit être ajouté à tous les points de terminaison. Par exemple, le point de terminaison `/global/classes` cité plus haut devient `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Vous verrez le format d&#39;API / modèle de requête dans toute la documentation et vous devez utiliser le chemin d&#39;accès complet illustré dans l&#39;exemple de requête lors de vos propres appels aux API de plateforme.

### Exemple de requête API

Voici un exemple de requête API illustrant le format que vous rencontrerez dans la documentation.

**Format d’API**

Le format d’API affiche l’opération (GET) et le point de terminaison utilisé. Les variables sont indiquées par des accolades (ici `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Requête**

Dans cet exemple de requête, les variables du format API reçoivent des valeurs réelles dans le chemin de la requête. En outre, tous les en-têtes requis sont présentés sous forme d’exemples de valeurs d’en-tête ou de variables dans lesquels des informations sensibles (telles que des jetons de sécurité et des ID d’accès) doivent être incluses.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse illustre ce que vous vous attendez à recevoir après un appel réussi vers l’API en fonction de la requête envoyée. Parfois, la réponse est tronquée en raison d’un espace insuffisant, il est donc possible que vous voyiez plus d’informations ou des informations supplémentaires par rapport à ce qui est affiché dans l’échantillon.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## Messages d’erreur

Le [Guide de dépannage de la plate-forme](troubleshooting.md#errors-and-troubleshooting) fournit une liste d&#39;erreurs que vous pouvez rencontrer lors de l&#39;utilisation d&#39;un service Experience Platform.

Pour obtenir des guides de dépannage sur les services de plateforme individuels, consultez le [répertoire de dépannage du service](troubleshooting.md#service-troubleshooting-directory).

Pour plus d&#39;informations sur des points de terminaison spécifiques dans les API de plateformes, y compris les en-têtes et les corps de requêtes requis, consultez les [guides de l&#39;API de plateforme](#api-guides).

## Guides de l&#39;API de plateforme {#api-guides}

| Guide de l’API | Description |
| --- | --- |
| [[!DNL Access Control] Guide de l’API](.././access-control/api/getting-started.md) | Le point de terminaison de l&#39;API [!DNL Access Control] peut récupérer les stratégies actuelles en vigueur pour un utilisateur sur des ressources données dans un sandbox spécifié. Toutes les autres capacités de contrôle d&#39;accès sont fournies par le [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guide de l&#39;API d&#39;assimilation de lot](.././ingestion/batch-ingestion/api-overview.md) | L&#39;API Adobe Experience Platform [!DNL Data Ingestion] vous permet d&#39;assimiler des données dans la plate-forme sous forme de fichiers de commandes. Les données ingérées peuvent être les données de profil provenant d&#39;un fichier plat dans un système de gestion de la relation client (par exemple un fichier Parquet), ou les données conformes à un schéma connu dans le registre des Schémas (XDM). |
| [[!DNL Catalog Service] Guide de l’API](.././catalog/api/getting-started.md) | L&#39;API [!DNL Catalog Service] permet aux développeurs de gérer les métadonnées de jeux de données dans Adobe Experience Platform. Cela inclut les emplacements de données, les étapes de traitement, les erreurs survenues pendant le traitement et les rapports de données. |
| [[!DNL Data Access] Guide de l’API](.././data-access/api.md) | L&#39;API [!DNL Data Access] permet aux développeurs de récupérer des informations sur les jeux de données assimilés dans l&#39;Experience Platform. Cela inclut l’accès et le téléchargement de fichiers de jeux de données, la récupération des informations d’en-tête, la liste des lots ayant échoué et réussi et le téléchargement de fichiers CSV/Parquet de prévisualisation. |
| [[!DNL Dataset Service] Guide de l’API](.././data-governance/labels/dataset-api.md) | L’API Service de dataset vous permet d’appliquer et de modifier des étiquettes d’utilisation pour les jeux de données. Il fait partie des fonctionnalités de catalogue de données Adobe Experience Platform, mais est distinct de l’API Catalog Service qui gère les métadonnées des jeux de données. |
| [[!DNL Flow Service] Guide](.././sources/tutorials/api/create-dataset-base-connection.md) <br>  API (Sources et destinations) | L&#39;API [!DNL Flow Service] est utilisée pour collecter et centraliser vos données à partir de diverses sources disparates et est utilisée pour créer et activer des données vers différentes destinations dans Adobe Experience Platform. Le service fournit une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables. |
| [[!DNL Identity Service] Guide de l’API](.././identity-service/api/getting-started.md) | L&#39;API [!DNL Identity Service] permet aux développeurs de gérer l&#39;identification inter-périphériques, entre canaux et en temps quasi réel de vos clients à l&#39;aide de graphiques d&#39;identité dans Adobe Experience Platform. |
| [[!DNL Observability Insights] Guide de l’API](.././observability/api/overview.md) | [!DNL Observability Insights] est une API RESTful qui permet aux développeurs d’exposer les mesures d’observabilité clés de Adobe Experience Platform. Ces mesures fournissent des insights sur les statistiques d’utilisation de Platform, les contrôles d’intégrité des services Platform, les tendances historiques et les indicateurs de performance pour diverses fonctionnalités de Platform. |
| [[!DNL Policy Service] Guide](.././data-governance/api/overview.md) <br>  API (gouvernance des données) | L&#39;API [!DNL Policy Service] vous permet de créer et de gérer des étiquettes et des stratégies d&#39;utilisation des données afin de déterminer quelles actions marketing peuvent être entreprises par rapport aux données contenant certaines étiquettes d&#39;utilisation des données. Pour appliquer des libellés aux jeux de données et aux champs, reportez-vous au guide [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) |
| [[!DNL Privacy Service] Guide de l’API](.././privacy-service/api/getting-started.md) | L&#39;API [!DNL Privacy Service] permet aux développeurs de créer et de gérer des demandes de clients pour accéder à leurs données personnelles ou les supprimer dans des applications Experience Cloud, en conformité avec les règles de confidentialité légales. |
| [[!DNL Query Service] Guide de l’API](.././query-service/api/getting-started.md) | L&#39;API [!DNL Query Service] permet aux développeurs de requête de leurs données Adobe Experience Platform à l&#39;aide de SQL standard. |
| [[!DNL Real-time Customer Profile] Guide de l’API](.././profile/api/overview.md) | L’API Profil client en temps réel permet aux développeurs d’explorer et d’utiliser des données de Profil, notamment l’affichage de profils, la création et la mise à jour de stratégies de fusion, l’exportation ou l’échantillonnage de données de Profil et la suppression de données de Profil qui ne sont plus requises ou qui ont été ajoutées par erreur. |
| [Guide de l’API Sandbox](.././sandboxes/api/getting-started.md) | L’API Sandbox permet aux développeurs de gérer par programmation des environnements de sandbox virtuels isolés à Adobe Experience Platform. |
| [[!DNL Schema Registry] Guide](.././xdm/api/overview.md) <br>  API (XDM) | L&#39;API [!DNL Schema Registry] permet aux développeurs de gérer par programmation tous les schémas et les ressources XDM (Experience Data Model) associées dans Adobe Experience Platform. |
| [[!DNL Segmentation Service] Guide de l’API](.././segmentation/api/overview.md) | L&#39;API [!DNL Segmentation Service] permet aux développeurs de gérer par programmation les opérations de segmentation dans Adobe Experience Platform. Cela inclut la création de segments et la génération d’audiences à partir de vos données de Profil client en temps réel. |
| [[!DNL Sensei Machine Learning] Guide](.././data-science-workspace/api/getting-started.md) <br>  API (Data Science Workspace) | L’API [!DNL Sensei Machine Learning] fournit un mécanisme permettant aux scientifiques de données d’organiser et de gérer les services d’apprentissage automatique (ML), depuis l’intégration d’algorithmes, l’expérimentation et le déploiement de services. |

Pour plus d&#39;informations sur les points de terminaison et les opérations spécifiques disponibles pour chaque service, consultez la [documentation de référence de l&#39;API](http://www.adobe.com/go/platform-api-reference-en) sur l&#39;Adobe I/O.

## Étapes suivantes

Ce document présente les en-têtes requis, les guides disponibles et fournit un exemple d’appel d’API. Maintenant que vous disposez des valeurs d’en-tête requises pour effectuer des appels d’API sur Adobe Experience Platform, sélectionnez un point de terminaison d’API que vous souhaitez explorer à partir du [tableau des guides d’API de plate-forme](#api-guides).

Pour obtenir des réponses aux questions fréquentes, consultez le [Guide de dépannage de la plate-forme](troubleshooting.md).

Pour configurer un environnement Postman et explorer les collections Postman disponibles, consultez le [guide Platform Postman](postman.md).


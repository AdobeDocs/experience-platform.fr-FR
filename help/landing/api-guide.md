---
keywords: Experience Platform;accueil;rubriques les plus consultées;Adobe Experience Platform;guide de l’api;guide de l’api de la plateforme;présentation de Platform;guide de développement
solution: Experience Platform
title: Prise en main des API Adobe Experience Platform
description: Adobe Experience Platform fournit des services d’API étroitement liés les uns aux autres. Ce guide contient des informations sur les services disponibles, les en-têtes requis pour les opérations CRUD, les messages d’erreur, les collections Postman et des exemples d’appels API.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: c728d63c22593ca56999dd0bb6679dea7de0e00a
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 28%

---

# Prise en main des API Adobe Experience Platform

Adobe Experience Platform est développé selon une philosophie &quot;API d’abord&quot;. À l’aide des API Platform, vous pouvez réaliser par programmation des opérations CRUD (Créer, Lire, Mettre à jour, Supprimer) de base sur des données, telles que la configuration d’attributs calculés, l’accès à des données/entités, l’exportation de données, la suppression de données ou de lots inutiles, etc.

Les API de chaque service Experience Platform partagent tous le même ensemble d’en-têtes d’authentification et utilisent des syntaxes similaires pour leurs opérations CRUD. Le guide suivant décrit les étapes nécessaires pour commencer à utiliser les API Platform.

## Authentification et en-têtes

Pour réussir les appels aux points de terminaison Platform, vous devez suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### En-tête Sandbox

Dans Experience Platform, toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans Platform, consultez la [documentation de présentation des sandbox](../sandboxes/home.md).

### En-tête de type contenu

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées sont spécifiques à chaque point de terminaison de l’API. Si une valeur `Content-Type` spécifique est nécessaire pour un point de terminaison, sa valeur s’affichera dans les exemples de requêtes d’API fournis par les [ guides d’API pour les services Platform individuels](#api-guides).

## Principes fondamentaux des API Experience Platform

Les API Adobe Experience Platform utilisent plusieurs technologies et syntaxes sous-jacentes importantes à comprendre pour gérer efficacement les ressources de Platform.

Pour en savoir plus sur les technologies d’API sous-jacentes utilisées par Platform, y compris les exemples d’objets de schéma JSON, consultez le guide [Principes de base de l’API Experience Platform](api-fundamentals.md).

## Collections Postman pour les API Experience Platform

Postman est une plateforme de collaboration pour le développement d’API qui vous permet de configurer des environnements avec des variables prédéfinies, de partager des collections d’API, de rationaliser les requêtes CRUD, etc. La plupart des services d’API Platform disposent de collections Postman qui peuvent être utilisées pour faciliter les appels d’API.

Pour en savoir plus sur Postman, y compris sur la configuration d’un environnement, une liste des collections disponibles et sur l’importation de collections, consultez la [documentation de Platform Postman](postman.md).

## Lecture d’exemples d’appels API {#sample-api}

Les formats de requête varient selon l’API de Platform utilisée. Le meilleur moyen d’apprendre à structurer vos appels API est de suivre les exemples fournis dans la documentation du service Platform que vous utilisez.

La documentation de [!DNL Experience Platform] présente des exemples d’appels API de deux manières différentes. Tout d’abord, l’appel est présenté dans son **format d’API**, qui consiste en une représentation de modèle affichant uniquement l’opération (GET, POST, PUT, PATCH, DELETE) et le point d’entrée utilisé (par exemple `/global/classes`). Certains modèles indiquent également l’emplacement des variables pour mieux illustrer la manière dont un appel doit être formulé, comme par exemple `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Les appels sont ensuite affichés sous forme de commandes cURL dans une **Requête**, qui comprend les en-têtes nécessaires et le « chemin racine » complet indispensable pour que l’interaction avec l’API soit réussie. Le chemin racine doit être ajouté à tous les points d’entrée. Par exemple, le point d’entrée `/global/classes` cité plus haut devient `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Le format/modèle de requête de l’API s’affiche dans toute la documentation et vous devez utiliser le chemin d’accès complet illustré dans l’exemple de requête lors de vos propres appels aux API Platform.

### Exemple de requête API

Voici un exemple de requête API illustrant le format que vous rencontrerez dans la documentation.

**Format d’API**

Le format d’API affiche l’opération (GET) et le point d’entrée utilisé. Les variables sont indiquées par des accolades (ici `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Requête**

Dans cet exemple de requête, les variables du format API reçoivent des valeurs réelles dans le chemin de la requête. En outre, tous les en-têtes requis sont affichés sous la forme d’exemples de valeurs d’en-tête ou de variables dans lesquelles des informations sensibles (telles que des jetons de sécurité et des ID d’accès) doivent être incluses.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Le [guide de dépannage de Platform](troubleshooting.md#errors-and-troubleshooting) fournit une liste des erreurs que vous pouvez rencontrer lors de l’utilisation d’un service Experience Platform.

Pour obtenir des guides de dépannage sur des services Platform individuels, consultez le [répertoire de dépannage des services](troubleshooting.md#service-troubleshooting-directory).

Pour plus d’informations sur des points de terminaison spécifiques dans les API Platform, y compris les en-têtes requis et les corps de requêtes, consultez les [guides de l’API Platform](#api-guides).

## Guides de l’API Platform {#api-guides}

| Guide des API | Description |
| --- | --- |
| [[!DNL Access Control] Guide de l’API](.././access-control/api/getting-started.md) | Le point d’entrée de l’API [!DNL Access Control] peut récupérer les stratégies actuelles en vigueur pour un utilisateur sur des ressources données dans un environnement de test spécifié. Toutes les autres fonctionnalités de contrôle d’accès sont fournies via [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guide de l’API d’ingestion par lots](.././ingestion/batch-ingestion/api-overview.md) | L’API Adobe Experience Platform [!DNL Data Ingestion] vous permet d’ingérer des données dans Platform sous forme de fichiers de lot. Les données en cours d’ingestion peuvent être les données de profil d’un fichier plat dans un système CRM (par exemple un fichier Parquet) ou les données conformes à un schéma connu dans le registre des schémas (XDM). |
| [[!DNL Catalog Service] Guide de l’API](.././catalog/api/getting-started.md) | L’API [!DNL Catalog Service] permet aux développeurs de gérer les métadonnées des jeux de données dans Adobe Experience Platform. Cela inclut l’emplacement des données, les étapes de traitement, les erreurs qui se sont produites pendant le traitement et les rapports de données. |
| [[!DNL Data Access] Guide de l’API](.././data-access/api.md) | L’API [!DNL Data Access] permet aux développeurs de récupérer des informations sur les jeux de données ingérés dans Experience Platform. Cela inclut l’accès et le téléchargement de fichiers de jeu de données, la récupération des informations d’en-tête, la liste des lots ayant échoué et réussi et le téléchargement de fichiers CSV/Parquet d’aperçu. |
| [[!DNL Dataset Service] Guide de l’API](.././data-governance/labels/dataset-api.md) | LʼAPI Dataset Service vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI Catalog Service qui gère les métadonnées du jeu de données. |
| [[!DNL Edge Network Server] Guide de l’API](../server-api/overview.md) | L’ [!DNL Edge Network Server API] peut être utilisé pour divers cas d’utilisation de la collecte de données, de la personnalisation, de la publicité et du marketing. Le [!DNL Server API] peut être utilisé sur les serveurs, les appareils [!DNL IoT], les décodeurs et sur divers autres appareils. |
| [[!DNL Identity Service] Guide de l’API](.././identity-service/api/getting-started.md) | L’API [!DNL Identity Service] permet aux développeurs de gérer l’identification inter-appareils, cross-canal et en temps quasi réel de vos clients à l’aide de graphiques d’identités dans Adobe Experience Platform. |
| [[!DNL Observability Insights] Guide de l’API](.././observability/api/overview.md) | [!DNL Observability Insights] est une API RESTful qui permet aux développeurs d’exposer les mesures d’observabilité clés dans Adobe Experience Platform. Ces mesures fournissent des informations sur les statistiques d’utilisation de Platform, les contrôles d’intégrité des services Platform, les tendances historiques et les indicateurs de performance pour diverses fonctionnalités de Platform. |
| [[!DNL Policy Service] Guide de l’API](.././data-governance/api/overview.md) <br> (Gouvernance des données) | L’API [!DNL Policy Service] vous permet de créer et de gérer des libellés et des stratégies d’utilisation des données afin de déterminer quelles actions marketing peuvent être entreprises concernant les données contenant certains libellés d’utilisation des données. Pour appliquer des libellés aux jeux de données et aux champs, reportez-vous au guide [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) |
| [[!DNL Privacy Service] Guide de l’API](.././privacy-service/api/getting-started.md) | L’API [!DNL Privacy Service] permet aux développeurs de créer et de gérer des demandes de clients pour accéder ou supprimer leurs données personnelles dans des applications Experience Cloud, conformément aux réglementations de confidentialité légales. |
| [[!DNL Query Service] Guide de l’API](.././query-service/api/getting-started.md) | L’API [!DNL Query Service] permet aux développeurs d’interroger leurs données Adobe Experience Platform à l’aide de SQL standard. |
| [[!DNL Real-Time Customer Profile] Guide de l’API](.././profile/api/overview.md) | L’API Real-time Customer Profile permet aux développeurs d’explorer et d’utiliser les données de profil, notamment d’afficher des profils, de créer et de mettre à jour des stratégies de fusion, d’exporter ou d’échantillonner des données de profil et de supprimer des données de profil qui ne sont plus requises ou qui ont été ajoutées par erreur. |
| [Guide de l’API Sandbox](.././sandboxes/api/getting-started.md) | L’API Sandbox permet aux développeurs de gérer par programmation les environnements de test virtuels isolés dans Adobe Experience Platform. |
| [[!DNL Schema Registry] Guide de l’API](.././xdm/api/overview.md) <br> (XDM) | L’API [!DNL Schema Registry] permet aux développeurs de gérer par programmation tous les schémas et les ressources XDM (Experience Data Model) associées dans Adobe Experience Platform. |
| [[!DNL Segmentation Service] Guide de l’API](.././segmentation/api/overview.md) | L’API [!DNL Segmentation Service] permet aux développeurs de gérer par programmation les opérations de segmentation dans Adobe Experience Platform. Cela inclut la création de segments et la génération d’audiences à partir de vos données Real-time Customer Profile. |
| [[!DNL Sensei Machine Learning] Guide de l’API](.././data-science-workspace/api/getting-started.md) <br> (Data Science Workspace) | L’API [!DNL Sensei Machine Learning] fournit un mécanisme permettant aux spécialistes des données d’organiser et de gérer les services d’apprentissage automatique (ML) depuis l’intégration d’algorithmes, l’expérimentation et jusqu’au déploiement de services. |

Pour plus d’informations sur les points de terminaison spécifiques et les opérations disponibles pour chaque service, consultez la [documentation de référence sur les API](https://www.adobe.com/go/platform-api-reference-en) sur Adobe I/O.

## Étapes suivantes

Ce document présente les en-têtes requis, les guides disponibles et fournit un exemple d’appel API. Maintenant que vous disposez des valeurs d’en-tête requises pour effectuer des appels API sur Adobe Experience Platform, sélectionnez un point de terminaison API que vous souhaitez explorer dans la [table des guides de l’API Platform](#api-guides).

Pour obtenir des réponses aux questions fréquentes, reportez-vous au [guide de dépannage de Platform](troubleshooting.md).

Pour configurer un environnement Postman et explorer les collections Postman disponibles, reportez-vous au [guide Platform Postman](postman.md).

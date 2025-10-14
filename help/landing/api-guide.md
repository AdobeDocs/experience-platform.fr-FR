---
keywords: Experience Platform;accueil;rubriques populaires;Adobe Experience Platform;guide de l’api;guide de l’api platform;présentation de platform;guide du développeur
solution: Experience Platform
title: Prise en main des API Adobe Experience Platform
description: Adobe Experience Platform fournit des services d’API étroitement liés les uns aux autres. Ce guide contient des informations sur les services disponibles, les en-têtes requis pour les opérations CRUD, les messages d’erreur, les collections Postman et les exemples d’appels API.
role: Developer
feature: API
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 21%

---

# Prise en main des API Adobe Experience Platform

Adobe Experience Platform est développé selon la philosophie « API first ». Grâce aux API d’Experience Platform, vous pouvez effectuer par programmation des opérations CRUD (Create, Read, Update, Delete) de base sur les données, comme configurer des attributs calculés, accéder à des données/entités, exporter des données, supprimer des données ou des lots inutiles, etc.

Les API de chaque service Experience Platform partagent toutes le même ensemble d’en-têtes d’authentification et utilisent des syntaxes similaires pour leurs opérations CRUD. Le guide suivant décrit les étapes nécessaires à la prise en main des API d’Experience Platform.

## Authentification et en-têtes

Pour passer avec succès des appels à des points d’entrée Experience Platform, vous devez suivre le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### En-tête Sandbox

Dans Experience Platform, toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Les requêtes envoyées aux API Experience Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans Experience Platform, consultez la [documentation de présentation des sandbox](../sandboxes/home.md).

### En-tête de type de contenu

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées sont spécifiques à chaque point d’entrée de l’API. Si une valeur d’`Content-Type` spécifique est nécessaire pour un point d’entrée, sa valeur s’affiche dans les exemples de requêtes d’API fournis par les guides d’API [&#x200B; pour les services Experience Platform individuels](#api-guides).

## Principes fondamentaux des API d’Experience Platform

Les API Adobe Experience Platform utilisent plusieurs technologies et syntaxes sous-jacentes importantes à comprendre pour gérer efficacement les ressources Experience Platform.

Pour en savoir plus sur les technologies d’API sous-jacentes utilisées par Experience Platform, y compris des exemples d’objets de schéma JSON, consultez le guide [Principes de base de l’API Experience Platform](api-fundamentals.md).

## Collections Postman pour les API Experience Platform

Postman est une plateforme de collaboration pour le développement d’API qui vous permet de configurer des environnements avec des variables prédéfinies, de partager des collections d’API, de rationaliser les requêtes CRUD, etc. La plupart des services d’API Experience Platform possèdent des collections Postman qui peuvent être utilisées pour faciliter l’émission d’appels d’API.

Pour en savoir plus sur Postman, notamment sur la configuration d’un environnement, sur une liste des collections disponibles et sur l’importation de collections, consultez la [documentation Experience Platform Postman](postman.md).

## Lecture d’exemples d’appels API {#sample-api}

Les formats de requête varient selon l’API Experience Platform utilisée. Le meilleur moyen d’apprendre à structurer vos appels API est de suivre les exemples fournis dans la documentation du service Experience Platform que vous utilisez.

La documentation de [!DNL Experience Platform] présente les exemples d’appels API de deux manières différentes. Tout d’abord, l’appel est présenté dans son **format d’API**, qui consiste en une représentation de modèle affichant uniquement l’opération (GET, POST, PUT, PATCH, DELETE) et le point d’entrée utilisé (par exemple `/global/classes`). Certains modèles indiquent également l’emplacement des variables pour mieux illustrer la manière dont un appel doit être formulé, comme par exemple `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Les appels sont ensuite affichés sous forme de commandes cURL dans une **Requête**, qui comprend les en-têtes nécessaires et le « chemin racine » complet indispensable pour que l’interaction avec l’API soit réussie. Le chemin racine doit être ajouté à tous les points d’entrée. Par exemple, le point d’entrée `/global/classes` cité plus haut devient `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Le format/modèle de requête de l’API est visible dans toute la documentation et vous devez utiliser le chemin d’accès complet illustré dans l’exemple de requête lorsque vous effectuez vos propres appels vers les API Experience Platform.

### Exemple de requête API

Voici un exemple de requête API illustrant le format que vous rencontrerez dans la documentation.

**Format d’API**

Le format d’API affiche l’opération (GET) et le point d’entrée utilisé. Les variables sont indiquées par des accolades (ici `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Requête**

Dans cet exemple de requête, les variables du format API reçoivent des valeurs réelles dans le chemin de la requête. En outre, tous les en-têtes requis s’affichent sous la forme d’exemples de valeurs d’en-tête ou de variables où des informations sensibles (telles que des jetons de sécurité et des identifiants d’accès) doivent être incluses.

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

Le guide de dépannage d’[Experience Platform](troubleshooting.md#errors-and-troubleshooting) fournit une liste des erreurs que vous pouvez rencontrer lors de l’utilisation d’un service Experience Platform.

Pour obtenir un guide de dépannage concernant un service Experience Platform spécifique, consultez le [répertoire de dépannage des services](troubleshooting.md#service-troubleshooting-directory).

Pour plus d’informations sur les points d’entrée spécifiques dans les API Experience Platform, y compris les en-têtes requis et les corps de requête, consultez les [guides de l’API Experience Platform](#api-guides).

## Guides de l’API Experience Platform {#api-guides}

| Guide des API | Description |
| --- | --- |
| [[!DNL Access Control]  Guide de l’API &#x200B;](.././access-control/api/getting-started.md) | Le point d’entrée de l’API [!DNL Access Control] peut récupérer les politiques actuelles en vigueur pour un utilisateur sur des ressources données dans un sandbox spécifié. Toutes les autres fonctionnalités de contrôle d’accès sont fournies via [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [&#x200B; Guide de l’API d’ingestion par lots &#x200B;](.././ingestion/batch-ingestion/api-overview.md) | L’API Adobe Experience Platform [!DNL Data Ingestion] vous permet d’ingérer des données dans Experience Platform sous forme de fichiers de lots. Les données ingérées peuvent être les données de profil d’un fichier plat dans un système CRM (comme un fichier Parquet) ou des données conformes à un schéma connu dans Schema Registry (XDM). |
| [[!DNL Catalog Service]  Guide de l’API &#x200B;](.././catalog/api/getting-started.md) | L’API [!DNL Catalog Service] permet aux développeurs de gérer les métadonnées des jeux de données dans Adobe Experience Platform. Cela inclut les emplacements des données, les étapes de traitement, les erreurs survenues pendant le traitement et les rapports de données. |
| [[!DNL Data Access]  Guide de l’API &#x200B;](.././data-access/api.md) | L’API [!DNL Data Access] permet aux développeurs de récupérer des informations sur les jeux de données ingérés dans Experience Platform. Cela inclut l’accès et le téléchargement des fichiers de jeu de données, la récupération des informations d’en-tête, la liste des lots ayant échoué et réussi et le téléchargement des fichiers CSV/Parquet d’aperçu. |
| [[!DNL Dataset Service]  Guide de l’API &#x200B;](.././data-governance/labels/dataset-api.md) | LʼAPI Dataset Service vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI Catalog Service qui gère les métadonnées du jeu de données. |
| [[!DNL Data Hygiene API guide]](../hygiene/api/overview.md) | L’API [!DNL Data Hygiene] vous permet de corriger ou de supprimer par programmation les données personnelles de vos clients stockées dans Adobe Experience Platform, ainsi que de planifier des dates d’expiration pour les jeux de données. |
| [[!DNL Edge Network]  Guide de l’API &#x200B;](https://developer.adobe.com/data-collection-apis/docs/getting-started/) | Le [!DNL Edge Network API] peut être utilisé pour divers cas d’utilisation de la collecte de données, de la personnalisation, de la publicité et du marketing. Le [!DNL Edge Network API] peut être utilisé sur des serveurs, des appareils [!DNL IoT], des décodeurs et de nombreux autres appareils. |
| [[!DNL Identity Service]  Guide de l’API &#x200B;](.././identity-service/api/getting-started.md) | L’API [!DNL Identity Service] permet aux développeurs de gérer l’identification inter-appareils, inter-canaux et en temps quasi réel de vos clients à l’aide de graphiques d’identités dans Adobe Experience Platform. |
| [[!DNL MTLS Service API guide]](../data-governance/mtls-api/overview.md) | L’API [!DNL MTLS Service] vous permet de récupérer en toute sécurité les certificats publics émis par Adobe pour votre organisation. |
| [[!DNL Observability Insights]  Guide de l’API &#x200B;](.././observability/api/overview.md) | [!DNL Observability Insights] est une API RESTful qui permet aux développeurs d’afficher des mesures d’observabilité clés dans Adobe Experience Platform. Ces mesures fournissent des informations sur les statistiques d’utilisation d’Experience Platform, les contrôles d’intégrité des services Experience Platform, les tendances historiques et les indicateurs de performances de diverses fonctionnalités d’Experience Platform. |
| [[!DNL Policy Service] Guide de l’API](.././data-governance/api/overview.md) <br> (gouvernance des données) | L’API [!DNL Policy Service] vous permet de créer et de gérer des libellés et des politiques d’utilisation des données afin de déterminer quelles actions marketing peuvent être entreprises concernant les données qui contiennent certains libellés d’utilisation. Pour appliquer des libellés aux jeux de données et aux champs, consultez le guide [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) |
| [[!DNL Privacy Service]  Guide de l’API &#x200B;](.././privacy-service/api/getting-started.md) | L’API [!DNL Privacy Service] permet aux développeurs et développeuses de créer et de gérer les demandes de clients souhaitant accéder à leurs données personnelles ou les supprimer dans les applications Experience Cloud, conformément aux réglementations légales en matière de confidentialité. |
| [[!DNL Query Service]  Guide de l’API &#x200B;](.././query-service/api/getting-started.md) | L’API [!DNL Query Service] permet aux développeurs d’interroger leurs données Adobe Experience Platform à l’aide de SQL standard. |
| [[!DNL Real-Time Customer Profile]  Guide de l’API &#x200B;](.././profile/api/overview.md) | L’API Real-Time Customer Profile permet aux développeurs d’explorer et d’utiliser les données de profil, notamment d’afficher les profils, de créer et de mettre à jour des politiques de fusion, d’exporter ou d’échantillonner des données de profil et de supprimer les données de profil qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. |
| [&#x200B; Guide de l’API Sandbox &#x200B;](.././sandboxes/api/getting-started.md) | L’API Sandbox permet aux développeurs de gérer par programmation les environnements de sandbox virtuels isolés dans Adobe Experience Platform. |
| [[!DNL Schema Registry] Guide de l’API](.././xdm/api/overview.md) <br> (XDM) | L’API [!DNL Schema Registry] permet aux développeurs de gérer par programmation tous les schémas et les ressources de modèle de données d’expérience (XDM) associées dans Adobe Experience Platform. |
| [[!DNL Segmentation Service]  Guide de l’API &#x200B;](.././segmentation/api/overview.md) | L’API [!DNL Segmentation Service] permet aux développeurs et développeuses de gérer par programmation les opérations de segmentation dans Adobe Experience Platform. Cela inclut la création de segments et la génération d’audiences à partir de vos données de profil client en temps réel. |
| [[!DNL Sensei Machine Learning] Guide de l’API](.././data-science-workspace/api/getting-started.md) <br> (Workspace de science des données) | L’API [!DNL Sensei Machine Learning] fournit un mécanisme permettant aux spécialistes des données d’organiser et de gérer les services de machine learning (ML) depuis l’intégration des algorithmes, l’expérimentation et le déploiement des services. |

Pour plus d’informations sur les points d’entrée et opérations spécifiques disponibles pour chaque service, consultez la [documentation de référence sur les API](https://www.adobe.com/go/platform-api-reference-en) sur Adobe I/O.

## Étapes suivantes

Ce document présente les en-têtes requis, les guides disponibles et fournit un exemple d’appel API. Maintenant que vous disposez des valeurs d’en-tête requises pour effectuer des appels API sur Adobe Experience Platform, sélectionnez un point d’entrée d’API que vous souhaitez explorer dans le tableau [Guides de l’API Experience Platform](#api-guides).

Pour obtenir des réponses aux questions fréquentes, reportez-vous au guide de dépannage d’[Experience Platform](troubleshooting.md).

Pour configurer un environnement Postman et explorer les collections Postman disponibles, reportez-vous au [guide Experience Platform Postman](postman.md).

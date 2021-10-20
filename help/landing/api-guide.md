---
keywords: Experience Platform ; accueil ; sujets populaires ; Adobe Experience Platform ; guide d’API ; guide d’API de plate-forme ; introduction à la plate-forme ; guide du développeur
solution: Experience Platform
title: Prise en main des API Adobe Experience Platform
topic-legacy: api guide
description: Adobe Experience Platform fournit des services d’API étroitement liés les uns aux autres. Ce guide contient des informations sur les services disponibles, les en-têtes requis pour les opérations CRUD, les messages d’erreur, les collections Postman et les exemples d’appels d’API.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: e62e4e3a12ad2a85de5b10c60fde3618cde84c4b
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 30%

---

# Prise en main des API Adobe Experience Platform

Adobe Experience Platform est développé selon une philosophie &quot;API first&quot;. À l’aide des API de plate-forme, vous pouvez effectuer par programmation des opérations CRUD de base (Créer, Lire, Mettre à jour, Supprimer) en fonction des données, telles que la configuration des attributs calculés, l’accès aux données/entités, l’exportation de données, la suppression de lots ou de données superflus, etc.

Les API de chaque service d’Experience Platform partagent tous le même ensemble d’en-têtes d’authentification et utilisent des syntaxes similaires pour leurs opérations CRUD. Le guide suivant décrit les étapes nécessaires pour commencer à utiliser les API de plate-forme.

## Authentification et en-têtes

Pour réussir les appels vers les points de terminaison de la plate-forme, vous devez terminer la [tutoriel sur l&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### En-tête Sandbox

Dans Experience Platform, toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

- `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d’informations sur les environnements de test dans Platform, consultez la [documentation de présentation des environnements de test](../sandboxes/home.md).

### En-tête de type de contenu

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées sont spécifiques à chaque point de terminaison API. Si `Content-Type` est nécessaire pour un point de terminaison, sa valeur sera affichée dans l’exemple de demandes d’API fourni par le [Guides d’API pour les services de plates-formes individuels](#api-guides).

## Principes de base de l’API Experience Platform

Les API Adobe Experience Platform utilisent plusieurs technologies et syntaxes sous-jacentes qui sont importantes à comprendre pour gérer efficacement les ressources de la plate-forme.

Pour en savoir plus sur les technologies d’API sous-jacentes utilisées par la plate-forme, y compris les exemples d’objets de schéma JSON, consultez la page [Principes de base de l’API Experience Platform](api-fundamentals.md) guide.

## Collections Postman pour les API Experience Platform

Postman est une plate-forme de collaboration pour le développement d’API qui vous permet de configurer des environnements avec des variables prédéfinies, de partager des collections d’API, de rationaliser les demandes CRUD, etc. La plupart des services d’API de plate-forme possèdent des collections Postman qui peuvent être utilisées pour faciliter l’exécution d’appels d’API.

Pour en savoir plus sur Postman, notamment sur la configuration d&#39;un environnement, la liste des collections disponibles et l&#39;importation de collections, consultez la page [Documentation de Platform Postman](postman.md).

## Lecture d&#39;exemples d&#39;appels API {#sample-api}

Les formats de requête varient selon l’API de Platform utilisée. Le meilleur moyen d’apprendre à structurer vos appels API est de suivre les exemples fournis dans la documentation du service Platform que vous utilisez.

La documentation pour [!DNL Experience Platform] présente des exemples d’appels d’API de deux manières différentes. Tout d’abord, l’appel est présenté dans son **format d’API**, qui consiste en une représentation de modèle affichant uniquement l’opération (GET, POST, PUT, PATCH, DELETE) et le point de terminaison utilisé (par exemple `/global/classes`). Certains modèles indiquent également l’emplacement des variables pour mieux illustrer la manière dont un appel doit être formulé, comme par exemple `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Les appels sont ensuite affichés sous forme de commandes cURL dans une **Requête**, qui comprend les en-têtes nécessaires et le « chemin racine » complet indispensable pour que l’interaction avec l’API soit réussie. Le chemin racine doit être ajouté à tous les points de terminaison. Par exemple, le point de terminaison `/global/classes` cité plus haut devient `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Vous verrez le format d’API/modèle de demande dans l’ensemble de la documentation. Vous devez utiliser le chemin d’accès complet indiqué dans l’exemple de demande lors de vos propres appels aux API de plate-forme.

### Exemple de requête API

Voici un exemple de requête API illustrant le format que vous rencontrerez dans la documentation.

**Format d’API**

Le format d’API affiche l’opération (GET) et le point de terminaison utilisé. Les variables sont indiquées par des accolades (ici `{CONTAINER_ID}`).

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

Le [Guide de dépannage des plates-formes](troubleshooting.md#errors-and-troubleshooting) fournit une liste des erreurs que vous pouvez rencontrer lors de l’utilisation d’un service d’Experience Platform.

Pour consulter les guides de dépannage sur les services de plate-forme individuels, voir [répertoire de dépannage des services](troubleshooting.md#service-troubleshooting-directory).

Pour plus d’informations sur des points de terminaison spécifiques dans les API de plate-forme, y compris les en-têtes et les organismes de demande requis, consultez la section [Guides de l’API de plate-forme](#api-guides).

## Guides de l’API de plate-forme {#api-guides}

| Guide des API | Description |
| --- | --- |
| [[!DNL Access Control] Guide des API](.././access-control/api/getting-started.md) | Le [!DNL Access Control] Le point de terminaison API peut récupérer les stratégies actuelles en vigueur pour un utilisateur sur des ressources données dans un sandbox spécifié. Toutes les autres fonctionnalités de contrôle d’accès sont fournies par le biais de la [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guide de l’API d’assimilation par lots](.././ingestion/batch-ingestion/api-overview.md) | Le Adobe Experience Platform [!DNL Data Ingestion] L’API vous permet d’assimiler des données dans la plate-forme sous la forme de fichiers par lots. Les données en cours d&#39;assimilation peuvent être les données de profil d&#39;un fichier plat dans un système CRM (tel qu&#39;un fichier Parquet), ou les données conformes à un schéma connu dans le Registre de schémas (XDM). |
| [[!DNL Catalog Service] Guide des API](.././catalog/api/getting-started.md) | Le [!DNL Catalog Service] L’API permet aux développeurs de gérer les métadonnées des ensembles de données dans Adobe Experience Platform. Cela comprend les emplacements des données, les étapes de traitement, les erreurs survenues pendant le traitement et les rapports de données. |
| [[!DNL Data Access] Guide des API](.././data-access/api.md) | Le [!DNL Data Access] L’API permet aux développeurs de récupérer des informations sur les ensembles de données assimilés dans l’Experience Platform. Cela comprend l’accès et le téléchargement des fichiers de jeu de données, la récupération des informations d’en-tête, la mise en vente des lots ayant échoué et réussi et le téléchargement des fichiers CSV/Parquet d’aperçu. |
| [[!DNL Dataset Service] Guide des API](.././data-governance/labels/dataset-api.md) | LʼAPI Dataset Service vous permet dʼappliquer et de modifier des étiquettes dʼutilisation pour les jeux de données. LʼAPI fait partie des fonctionnalités de catalogue de données dʼAdobe Experience Platform, mais est distinct de lʼAPI Catalog Service qui gère les métadonnées du jeu de données. |
| [[!DNL Identity Service] Guide des API](.././identity-service/api/getting-started.md) | Le [!DNL Identity Service] L’API permet aux développeurs de gérer l’identification inter-périphériques, inter-canaux et quasi en temps réel de vos clients à l’aide de graphiques d’identité dans Adobe Experience Platform. |
| [[!DNL Observability Insights] Guide des API](.././observability/api/overview.md) | [!DNL Observability Insights] est une API RESTful qui permet aux développeurs d&#39;exposer les mesures d&#39;observabilité clés dans Adobe Experience Platform. Ces mesures fournissent des insights sur les statistiques d’utilisation de Platform, les contrôles d’intégrité des services Platform, les tendances historiques et les indicateurs de performance pour diverses fonctionnalités de Platform. |
| [[!DNL Policy Service] Guide d’API](.././data-governance/api/overview.md) <br> (Gouvernance des données) | Le [!DNL Policy Service] L’API vous permet de créer et de gérer des libellés et des stratégies d’utilisation des données afin de déterminer quelles actions marketing peuvent être entreprises par rapport aux données qui contiennent certains libellés d’utilisation des données. Pour appliquer des libellés aux ensembles de données et aux champs, reportez-vous à la section [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) guide |
| [[!DNL Privacy Service] Guide des API](.././privacy-service/api/getting-started.md) | Le [!DNL Privacy Service] L’API permet aux développeurs de créer et de gérer des demandes client d’accès ou de suppression de leurs données personnelles dans des applications Experience Cloud, conformément aux règles de confidentialité légales. |
| [[!DNL Query Service] Guide des API](.././query-service/api/getting-started.md) | Le [!DNL Query Service] L’API permet aux développeurs d’interroger leurs données Adobe Experience Platform à l’aide de SQL standard. |
| [[!DNL Real-time Customer Profile] Guide des API](.././profile/api/overview.md) | L’API de profil de client en temps réel permet aux développeurs d’explorer et d’utiliser les données de profil, y compris l’affichage des profils, la création et la mise à jour des stratégies de fusion, l’exportation ou l’échantillonnage des données de profil et la suppression des données de profil qui ne sont plus requises ou qui ont été ajoutées par erreur. |
| [Guide de l’API Sandbox](.././sandboxes/api/getting-started.md) | L’API Sandbox permet aux développeurs de gérer par programme des environnements sandbox virtuels isolés dans Adobe Experience Platform. |
| [[!DNL Schema Registry] Guide d’API](.././xdm/api/overview.md) <br> (XDM) | Le [!DNL Schema Registry] L’API permet aux développeurs de gérer par programme tous les schémas et les ressources XDM (Experience Data Model) associées au sein de Adobe Experience Platform. |
| [[!DNL Segmentation Service] Guide des API](.././segmentation/api/overview.md) | Le [!DNL Segmentation Service] L’API permet aux développeurs de gérer par programme les opérations de segmentation dans Adobe Experience Platform. Cela inclut la création de segments et la génération de publics à partir de vos données de profil client en temps réel. |
| [[!DNL Sensei Machine Learning] Guide d’API](.././data-science-workspace/api/getting-started.md) <br> (Espace de travail Data Science) | Le [!DNL Sensei Machine Learning] L’API fournit un mécanisme permettant aux scientifiques de données d’organiser et de gérer les services d’apprentissage automatique (ML) à partir de l’intégration d’algorithmes, de l’expérimentation et du déploiement de services. |

Pour plus d’informations sur les points de terminaison spécifiques et les opérations disponibles pour chaque service, consultez la section [Documentation de référence API](https://www.adobe.com/go/platform-api-reference-en) sur Adobe I/O.

## Étapes suivantes

Ce document présente les en-têtes requis, les guides disponibles et fournit un exemple d’appel d’API. Maintenant que vous disposez des valeurs d’en-tête requises pour effectuer des appels d’API sur Adobe Experience Platform, sélectionnez un point de terminaison d’API que vous souhaitez explorer à partir de l’onglet [Tableau des repères d’API de plate-forme](#api-guides).

Pour obtenir des réponses aux questions fréquemment posées, consultez la section [Guide de dépannage des plates-formes](troubleshooting.md).

Pour configurer un environnement Postman et explorer les collections Postman disponibles, reportez-vous à la section [Guide de Platform Postman](postman.md).

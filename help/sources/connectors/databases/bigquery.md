---
keywords: Experience Platform;accueil;rubriques populaires;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Présentation du connecteur source Google BigQuery
topic-legacy: overview
description: Découvrez comment connecter Google BigQuery à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 7a62dcf1e9712d3c0c0d148b953e50dc11c91f1b
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 34%

---

# [!DNL Google BigQuery]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’une base de données tierce. Platform peut se connecter à différents types de bases de données comme les entrepôts relationnels, NoSQL ou de données. La prise en charge des fournisseurs de base de données inclut [!DNL Google BigQuery].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables

La section suivante fournit des informations supplémentaires sur la configuration de prérequis requise avant de pouvoir créer une [!DNL Google BigQuery] connexion source.

### Générez vos [!DNL Google BigQuery] informations

Pour se connecter [!DNL Google BigQuery] Pour Platform, vous devez générer des valeurs pour les informations d’identification suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `project` | Le projet est l’entité organisatrice de base pour votre [!DNL Google Cloud] ressources, y compris [!DNL Google BigQuery]. |
| `clientID` | L’ID client représente la moitié de votre [!DNL Google BigQuery] Informations d’identification OAuth 2.0. |
| `clientSecret` | Le secret client est l’autre moitié de votre [!DNL Google BigQuery] Informations d’identification OAuth 2.0. |
| `refreshToken` | Le jeton d’actualisation vous permet d’obtenir de nouveaux jetons d’accès pour votre API. Les jetons d’accès ont des durées de vie limitées et peuvent expirer au cours du projet. Vous pouvez utiliser le jeton d’actualisation pour vous authentifier et demander des jetons d’accès ultérieurs pour votre projet, si nécessaire. |
| `largeResultsDataSetId` | La variable  [!DNL Google BigQuery] identifiant du jeu de données requis pour activer la prise en charge des jeux de résultats volumineux. |

Pour obtenir des instructions détaillées sur la génération des informations d’identification OAuth 2.0 pour [!DNL Google] API, voir [[!DNL Google] Guide d’authentification OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Connecter [!DNL Google BigQuery] à Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Google BigQuery] à Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

- [Création d’une connexion de base Google BigQuery à l’aide de l’API Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Exploration des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Création d’un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

### Utiliser l’interface utilisateur

- [Création d’une connexion source Google BigQuery dans l’interface utilisateur](../../tutorials/ui/create/databases/bigquery.md)
- [Création d’un flux de données pour une connexion à la source de la base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)

---
keywords: Experience Platform;accueil;rubriques populaires;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Présentation du connecteur source Google BigQuery
topic-legacy: overview
description: Découvrez comment connecter Google BigQuery à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 15%

---

# (Version bêta) Connecteur [!DNL Google BigQuery]

>[!NOTE]
>
>[!DNL Google BigQuery] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../home.md#terms-and-conditions) .

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’une base de données tierce. Platform peut se connecter à différents types de bases de données comme les entrepôts relationnels, NoSQL ou de données. [!DNL Google BigQuery] est compatible avec les fournisseurs de base de données.

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Pour plus d’informations, consultez la page [liste autorisée d’adresses IP](../../ip-address-allow-list.md) .

## Conditions préalables

La section suivante fournit des informations supplémentaires sur la configuration de prérequis requise pour pouvoir créer une connexion source [!DNL Google BigQuery].

### Générer vos [!DNL Google BigQuery] informations d’identification

Pour connecter [!DNL Google BigQuery] à Platform, vous devez générer des valeurs pour les informations d’identification suivantes :

| Credential | Description |
| ---------- | ----------- |
| `project` | Le projet est l’entité organisatrice de base pour vos ressources [!DNL Google Cloud], y compris [!DNL Google BigQuery]. |
| `clientID` | L’ID client correspond à la moitié de vos [!DNL Google BigQuery] informations d’identification OAuth 2.0. |
| `clientSecret` | Le secret client est l’autre moitié de vos informations d’identification OAuth 2.0 [!DNL Google BigQuery]. |
| `refreshToken` | Le jeton d’actualisation vous permet d’obtenir de nouveaux jetons d’accès pour votre API. Les jetons d’accès ont des durées de vie limitées et peuvent expirer au cours du projet. Vous pouvez utiliser le jeton d’actualisation pour vous authentifier et demander des jetons d’accès ultérieurs pour votre projet, si nécessaire. |

Pour obtenir des instructions détaillées sur la génération des informations d’identification OAuth 2.0 pour les API [!DNL Google], consultez le [[!DNL Google] guide d’authentification OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) suivant.

## Connecter [!DNL Google BigQuery] à Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Google BigQuery] à Platform à l’aide d’API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’une connexion de base Google BigQuery à l’aide de l’API Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Explorer la structure et le contenu des données d’une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Création d’un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion source Google BigQuery dans l’interface utilisateur](../../tutorials/ui/create/databases/bigquery.md)
- [Création d’un flux de données pour une connexion à la source de la base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)

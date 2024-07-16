---
title: Présentation du connecteur Source BigQuery Google
description: Découvrez comment connecter Google BigQuery à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 34%

---

# Source [!DNL Google BigQuery]

>[!IMPORTANT]
>
>La source [!DNL Google BigQuery] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données à partir d’une base de données tierce. Platform peut se connecter à différents types de bases de données comme les entrepôts relationnels, NoSQL ou de données. [!DNL Google BigQuery] est compatible avec les fournisseurs de base de données.

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables

La section suivante fournit des informations supplémentaires sur la configuration de prérequis requise pour pouvoir créer une connexion source [!DNL Google BigQuery].

### Génération de vos informations d’identification [!DNL Google BigQuery]

Pour connecter [!DNL Google BigQuery] à Platform, vous devez générer des valeurs pour les informations d’identification suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `project` | Le projet est l’entité d’organisation de niveau de base pour vos ressources [!DNL Google Cloud], y compris [!DNL Google BigQuery]. |
| `clientID` | L’ID client correspond à la moitié de vos informations d’identification OAuth 2.0 [!DNL Google BigQuery]. |
| `clientSecret` | Le secret client est l’autre moitié de vos informations d’identification OAuth 2.0 [!DNL Google BigQuery]. |
| `refreshToken` | Le jeton d’actualisation vous permet d’obtenir de nouveaux jetons d’accès pour votre API. Les jetons d’accès ont des durées de vie limitées et peuvent expirer au cours du projet. Vous pouvez utiliser le jeton d’actualisation pour vous authentifier et demander des jetons d’accès ultérieurs pour votre projet, si nécessaire. |
| `largeResultsDataSetId` | L’identifiant du jeu de données [!DNL Google BigQuery] précréé qui est requis pour permettre la prise en charge des jeux de résultats volumineux. |

Pour obtenir des instructions détaillées sur la génération des informations d’identification OAuth 2.0 pour les API [!DNL Google], consultez le [[!DNL Google] guide d’authentification OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) suivant.

## Connecter [!DNL Google BigQuery] à Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Google BigQuery] à Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

- [Création d’une connexion de base Google BigQuery à l’aide de l’API Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Création d’un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

### Utilisation de l’interface utilisateur

- [Créer une connexion source Google BigQuery dans l’interface utilisateur](../../tutorials/ui/create/databases/bigquery.md)
- [Création d’un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)

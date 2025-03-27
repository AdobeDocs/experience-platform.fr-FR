---
title: Présentation du connecteur Source BigQuery Google
description: Découvrez comment connecter Google BigQuery à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 4%

---

# Source [!DNL Google BigQuery]

>[!IMPORTANT]
>
>La source [!DNL Google BigQuery] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce document pour connaître les étapes préalables à suivre pour connecter votre compte [!DNL Google BigQuery] à Adobe Experience Platform sur Azure ou Amazon Web Services (AWS).

## Conditions préalables {#prerequisites}

Lisez les sections suivantes pour connaître les conditions préalables à la configuration que vous devez remplir avant de pouvoir connecter votre compte [!DNL Google BigQuery] à Experience Platform.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform sur Azure ou Amazon Web Services (AWS). Pour plus d’informations, consultez le guide sur la [liste autorisée des adresses IP pour se connecter à Experience Platform sur Azure et AWS](../../ip-address-allow-list.md).

### S’authentifier auprès d’Experience Platform sur Azure {#azure}

Vous devez fournir les informations d’identification suivantes pour connecter votre compte [!DNL Google BigQuery] à Experience Platform sur Azure.

>[!BEGINTABS]

>[!TAB  Authentification de base ]

Pour vous authentifier à l’aide d’une combinaison d’OAuth 2.0 et de l’authentification de base, fournissez les valeurs appropriées pour les informations d’identification suivantes.

| Informations d’identification | Description |
| --- | --- |
| `project` | Le projet est l’entité d’organisation de base pour vos ressources [!DNL Google Cloud], y compris les [!DNL Google BigQuery]. |
| `clientID` | L’ID client correspond à la moitié de vos informations d’identification OAuth 2.0 [!DNL Google BigQuery]. |
| `clientSecret` | Le secret client correspond à l’autre moitié de vos informations d’identification OAuth 2.0 [!DNL Google BigQuery]. |
| `refreshToken` | Le jeton d’actualisation vous permet d’obtenir de nouveaux jetons d’accès pour votre API. Les jetons d’accès ont une durée de vie limitée et peuvent expirer au cours de votre projet. Vous pouvez utiliser le jeton d’actualisation pour vous authentifier et demander des jetons d’accès ultérieurs pour votre projet, si nécessaire. |
| `largeResultsDataSetId` | (Facultatif) Identifiant de jeu de données [!DNL Google BigQuery] précréé et requis pour permettre la prise en charge de jeux de résultats volumineux. |

Pour obtenir des instructions détaillées sur la génération des informations d’identification OAuth 2.0 pour les API [!DNL Google], consultez le guide d’authentification [[!DNL Google] OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) suivant.

>[!TAB Authentification du service]

Pour vous authentifier à l’aide de l’authentification de service, indiquez les valeurs appropriées pour les informations d’identification suivantes.

**Remarque** : votre compte de service doit disposer des autorisations suffisantes, telles que : **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** et **[!DNL BigQuery Data Owner]**, pour réussir l’authentification avec l’authentification de service.

| Informations d’identification | Description |
| --- | --- |
| `projectId` | L’identifiant du [!DNL Google BigQuery] sur lequel vous souhaitez effectuer une requête. |
| `keyFileContent` | Fichier de clé utilisé pour authentifier le compte de service. Vous pouvez récupérer cette valeur à partir du [[!DNL Google Cloud service accounts] tableau de bord](https://console.cloud.google.com). Le contenu du fichier de clé est au format JSON. Vous devez l’encoder en [!DNL Base64] lors de l’authentification à Experience Platform. |
| `largeResultsDataSetId` | (Facultatif) Identifiant de jeu de données [!DNL Google BigQuery] précréé et requis pour permettre la prise en charge de jeux de résultats volumineux. |

Pour plus d’informations sur l’utilisation des comptes de service dans [!DNL Google BigQuery], consultez le guide sur [l’utilisation de comptes de service dans [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

### Authentification à Experience Platform sur AWS {#aws}

Vous devez fournir les informations d’identification suivantes pour connecter votre compte [!DNL Google BigQuery] à Experience Platform sur AWS.

| Informations d’identification | Description |
| --- | --- |
| `projectId` | L’identifiant du [!DNL Google BigQuery] sur lequel vous souhaitez effectuer une requête. |
| `keyFileContent` | Fichier de clé utilisé pour authentifier le compte de service. Vous pouvez récupérer cette valeur à partir du [[!DNL Google Cloud service accounts] tableau de bord](https://console.cloud.google.com). Le contenu du fichier de clé est au format JSON. Vous devez l’encoder en [!DNL Base64] lors de l’authentification à Experience Platform. |
| `datasetId` | Identifiant du jeu de données [!DNL Google BigQuery]. Cet identifiant représente l’emplacement de vos tables de données. |

## Connexion de [!DNL Google BigQuery] à Experience Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Google BigQuery] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

- [Créer une connexion de base BigQuery Google à l’aide de l’API Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

### Utilisation de l’interface utilisateur

- [Créer une connexion source BigQuery Google dans l’interface utilisateur](../../tutorials/ui/create/databases/bigquery.md)
- [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)

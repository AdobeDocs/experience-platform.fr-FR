---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur Google AdWords à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: b9e9207741044f118d53ab8eb3d3d6cd7451132d
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 1%

---


# Création d’un connecteur Google AdWords à l’aide de l’API du service de flux

>[!NOTE]
>Le connecteur Google AdWords est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Le service de flux permet de collecter et de centraliser les données client provenant de diverses sources disparates au sein de l’Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API du service de flux pour vous guider dans les étapes de connexion de l’Experience Platform à Google AdWords.

## Prise en main

Ce guide exige une compréhension pratique des éléments suivants de l&#39;Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance Platform unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à la publicité à l’aide de l’API de service de flux.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte à AdWords, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| **Informations d’identification** | **Description** |
| -------------- | --------------- |
| ID client client client | ID client du compte AdWords. |
| Jeton de développement | Jeton de développeur associé au compte de gestionnaire. |
| Actualiser le jeton | Jeton d’actualisation obtenu auprès de Google pour autoriser l’accès à AdWords. |
| ID client | ID client de l’application Google utilisé pour acquérir le jeton d’actualisation. |
| Secret client | Le secret client de l&#39;application google utilisé pour acquérir le jeton d&#39;actualisation. |
| ID de spécification de connexion | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour Google AdWords est : `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Pour plus d&#39;informations sur ces valeurs, consultez ce document [](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de l’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour passer des appels aux API Platform, vous devez d’abord suivre le didacticiel [d’](../../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de l’Experience Platform, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte Google AdWords, car elle peut être utilisée pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une nouvelle connexion AdWords, configurée par les propriétés fournies dans la charge utile :


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.clientCustomerID` | ID client de votre compte AdWords. |
| `auth.params.developerToken` | Jeton de développeur de votre compte AdWords. |
| `auth.params.refreshToken` | Jeton d’actualisation de votre compte AdWords. |
| `auth.params.clientID` | ID client de votre compte AdWords. |
| `auth.params.clientSecret` | Le secret client de votre compte AdWords. |
| `connectionSpec.id` | ID de spécification de connexion Google AdWords : `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion Google AdWords à l’aide de l’API du service de flux et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des systèmes de publicité à l’aide de l’API](../../explore/advertising.md)de service de flux.

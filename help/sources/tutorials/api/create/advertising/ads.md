---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur d’annonces Google à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: 950fa88ed6c9235bff98658763b662113bb76caa

---


# Création d’un connecteur d’annonces Google à l’aide de l’API du service de flux

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API du service de flux pour vous guider tout au long des étapes nécessaires à la connexion de la plateforme d’expérience aux publicités Google.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à l’annonce à l’aide de l’API de service de flux.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte aux publicités, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| **Informations d’identification** | **Description** |
| -------------- | --------------- |
| ID client client client client | ID client du compte Publicités. |
| Jeton Développeur | Jeton de développeur associé au compte du gestionnaire. |
| Actualiser le jeton | Jeton d’actualisation obtenu auprès de Google pour autoriser l’accès aux publicités. |
| ID client | ID client de l’application Google utilisé pour acquérir le jeton d’actualisation. |
| Secret client | Le secret client de l’application google utilisé pour acquérir le jeton d’actualisation. |
| ID de spécification de connexion | Identificateur unique nécessaire pour créer une connexion. L’ID de spécification de connexion pour les publicités Google est : `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Pour plus d&#39;informations sur ces valeurs, reportez-vous à ce [Publicités](https://developers.google.com/adwords/api/docs/guides/authentication)Google.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../../../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type : `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte Google Ads, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format API**

```https
POST /connections
```

**Requête**

Pour créer une connexion Google Publics, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande POST. L&#39;ID de spécification de connexion pour les publicités Google est `221c7626-58f6-4eec-8ee2-042b0226f03b`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-ads connection",
        "description": "Connection for google-ads",
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
| `auth.params.clientCustomerID` | ID client de votre compte Publicités. |
| `auth.params.developerToken` | Jeton de développeur de votre compte Publicités. |
| `auth.params.refreshToken` | Jeton d’actualisation de votre compte Publicités. |
| `auth.params.clientID` | ID client de votre compte Publicités. |
| `auth.params.clientSecret` | Le secret client de votre compte Publicités. |
| `connectionSpec.id` | ID de spécification de connexion Google Ads : `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion Google Publicités à l’aide de l’API du service de flux et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des systèmes publicitaires à l’aide de l’API](../../explore/advertising.md)de service de flux.

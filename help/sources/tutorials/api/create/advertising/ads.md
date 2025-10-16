---
title: Connexion de Google Ads à Experience Platform à l’aide d’API
description: Découvrez comment connecter Adobe Experience Platform à Google Ads à l’aide de l’API Flow Service.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: a0977e98219797eda14dd8d7ddb6cf3f1410cef0
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 27%

---

# Connexion de [!DNL Google Ads] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Lisez ce tutoriel pour savoir comment connecter votre compte [!DNL Google Ads] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Google Ads] à l’aide de l’API [!DNL Flow Service].

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

### Collecter les informations d’identification requises

Pour plus d’informations sur l’authentification, consultez la [[!DNL Google Ads] présentation de la source](../../../../connectors/advertising/ads.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification Google Ads dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour Google Ads :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v19"

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
| `auth.params.clientCustomerID` | Identifiant client de votre compte [!DNL Google Ads]. |
| `auth.params.loginCustomerID` | Identifiant client de connexion correspondant à votre compte [!DNL Google Ads] Manager. |
| `auth.params.developerToken` | Jeton de développeur de votre compte [!DNL Google Ads]. |
| `auth.params.refreshToken` | Jeton d’actualisation de votre compte [!DNL Google Ads]. |
| `auth.params.clientID` | Identifiant client de votre compte [!DNL Google Ads]. |
| `auth.params.clientSecret` | Secret client de votre compte [!DNL Google Ads]. |
| `auth.params.googleAdsApiVersion` | Version de l’API [!DNL Google Ads] que vous utilisez. Experience Platform prend actuellement en charge la version `v19` et ultérieure. Assurez-vous d’utiliser l’une de ces versions prises en charge pour garantir la compatibilité. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Google Ads] : `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Créer un flux de données pour ingérer des données publicitaires

Ce tutoriel vous a permis de créer une connexion de base [!DNL Google Ads] à l’aide de l’API [!DNL Flow Service] et de connecter votre compte [!DNL Google Ads] à Experience Platform. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données publicitaires dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/advertising.md)

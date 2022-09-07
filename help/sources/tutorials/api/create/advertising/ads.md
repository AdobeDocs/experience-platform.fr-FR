---
keywords: Experience Platform;accueil;rubriques les plus consultées;annonces Google;publicités Google;publicités Google;publicités Google
title: Création d’une connexion de base Google Ads à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Google Ads à l’aide de l’API Flow Service.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 23%

---

# Créez une connexion de base Google Ads à l’aide du [!DNL Flow Service] API

>[!NOTE]
>
>La source Google Ads est en version bêta. Voir [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création d’une connexion de base pour Google Ads à l’aide du [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Environnements de test](../../../../../sandboxes/home.md): Experience Platform fournit des environnements de test virtuels qui divisent une instance d’Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à Google Ads à l’aide de la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à Google Ads, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `clientCustomerId` | L’ID client est le numéro de compte correspondant au compte client Google Ads que vous souhaitez gérer avec l’API Google Ads. Cet identifiant suit le modèle de `123-456-7890`. |
| `developerToken` | Le jeton de développement vous permet d’accéder à l’API Google Ads. Vous pouvez utiliser le même jeton de développement pour effectuer des requêtes sur tous vos comptes Google Ads. Récupération du jeton de développement par [connexion à votre compte de gestionnaire](https://ads.google.com/home/tools/manager-accounts/) puis en accédant à la [!DNL API Center] page. |
| `refreshToken` | Le jeton d’actualisation fait partie de [!DNL OAuth2] authentification. Ce jeton vous permet de régénérer vos jetons d’accès après leur expiration. |
| `clientId` | L’ID client est utilisé en tandem avec le secret client dans le cadre de [!DNL OAuth2] authentification. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à Google. |
| `clientSecret` | Le secret client est utilisé en tandem avec l’ID client dans le cadre de [!DNL OAuth2] authentification. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à Google. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour Google Ads est : `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Lisez le document de présentation de l’API pour [en savoir plus sur la prise en main de Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison tout en fournissant vos informations d’authentification Google Ads dans le cadre des paramètres de requête.

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
| `auth.params.clientCustomerID` | Identifiant client de votre compte Google Ads. |
| `auth.params.developerToken` | Jeton de développeur de votre compte Google Ads. |
| `auth.params.refreshToken` | Jeton d’actualisation de votre compte Google Ads. |
| `auth.params.clientID` | Identifiant client de votre compte Google Ads. |
| `auth.params.clientSecret` | Le secret client de votre compte Google Ads. |
| `connectionSpec.id` | L’identifiant de spécification de connexion Google Ads : `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion de base Google Ads à l’aide de la variable [!DNL Flow Service] API. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants :

* [Explorez la structure et le contenu de vos tableaux de données à l’aide du [!DNL Flow Service] API](../../explore/tabular.md)
* [Créez un flux de données pour importer des données publicitaires dans Platform à l’aide du [!DNL Flow Service] API](../../collect/advertising.md)

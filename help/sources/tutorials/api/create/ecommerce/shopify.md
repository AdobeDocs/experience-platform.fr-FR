---
keywords: Experience Platform;accueil;rubriques populaires;Shopify;shopify;e-commerce
title: Créer une connexion de base au connecteur Shopify à l’aide de l’API Flow Service
description: Découvrez comment connecter Shopify à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: 845af785bbc008b664a81e522ae66bd3c10a980e
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 33%

---

# Créez une connexion de base à [!DNL Shopify] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Lisez ce guide pour savoir comment créer une connexion de base pour le connecteur source [!DNL Shopify] à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d&#39;Adobe Experience Platform :

* [[!DNL Sources]](../../../../home.md) : utilisez les sources pour importer facilement des données à partir de divers systèmes et plateformes externes. Cette fonctionnalité vous permet d’organiser, d’étiqueter et d’enrichir vos données entrantes afin d’en tirer davantage de valeur à l’aide des services Experience Platform.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md) : les sandbox vous permettent de tester, de tester et de développer des expériences digitales en toute sécurité en fournissant des espaces distincts dans votre instance Experience Platform, afin que vous puissiez apporter des modifications sans affecter votre environnement de production.

### Collecter les informations d’identification requises

Vous devez disposer d’informations d’authentification [!DNL Shopify] valides pour créer une connexion de base. Pour plus d’informations sur les informations d’identification requises et sur la manière de les obtenir, reportez-vous à la [[!DNL Shopify] présentation du connecteur source](../../../../connectors/ecommerce/shopify.md#prerequisites).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Shopify] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

### Authentification de base

La requête suivante crée une connexion de base pour [!DNL Shopify] à l’aide de l’authentification de base :

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Shopify source",
      "description": "Shopify source",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
          "version": "1.0"
      }
  }
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | Point d’entrée du serveur [!DNL Shopify]. |
| `auth.params.accessToken` | Jeton d’accès de votre compte utilisateur [!DNL Shopify]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Shopify] : `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

+++

+++Réponse

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

+++

### Basé sur le jeton d’accès

La requête suivante crée une connexion de base pour [!DNL Shopify] à l’aide de l’authentification de base :

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Create shopify v2 Test Connection",
    "description": "Connection creation for Shopify",
    "auth": {
      "specName": "Access Token Based",
      "params": {
        "host": "{HOST}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    },
    "connectionSpec": {
      "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
      "version": "1.0"
    }
}'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | Point d’entrée du serveur [!DNL Shopify]. |
| `auth.params.accessToken` | Jeton d’accès de votre compte utilisateur [!DNL Shopify]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Shopify] : `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

+++

+++Réponse

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "92a00150-f3cc-4283-8fc4-6232725bcf33",
    "etag": "\"bb04d1f7-0000-0200-0000-69807e830000\""
}
```

+++

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Shopify] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants :

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créer un flux de données pour importer des données E-Commerce dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/ecommerce.md)

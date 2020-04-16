---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur HubSpot à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: c08650ca1655e248f0a0f8a6b371c5fd005aab1c

---


# Création d’un connecteur HubSpot à l’aide de l’API du service de flux

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API du service de flux pour vous guider tout au long des étapes nécessaires à la connexion de la plate-forme d’expérience à HubSpot.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à HubSpot à l’aide de l’API du service de flux.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte à HubSpot, vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| ID client | ID client associé à votre application HubSpot. |
| Secret client | Le secret client associé à votre application HubSpot. |
| Access Token | Le obtenu lors de l’authentification initiale de votre intégration OAuth. |
| Actualiser le jeton | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |
| ID de spécification de connexion | Identificateur unique nécessaire pour créer une connexion. L’ID de spécification de connexion pour HubSpot est : `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Pour plus d’informations sur la prise en main, reportez-vous à ce [HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

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

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte HubSpot, car elle peut être utilisée pour créer plusieurs connecteurs source pour importer des données différentes.

**Format API**

```https
POST /connections
```

**Requête**

Pour créer une connexion HubSpot, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande POST. L&#39;ID de spécification de connexion pour HubSpot est `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.clientId` | ID client associé à votre application HubSpot. |
| `auth.params.clientSecret` | Le secret client associé à votre application HubSpot. |
| `auth.params.accessToken` | Le obtenu lors de l’authentification initiale de votre intégration OAuth. |
| `auth.params.refreshToken` | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée pour l’API, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

En suivant ce didacticiel, vous avez créé une connexion HubSpot à l’aide de l’API du service de flux et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant de connexion dans le didacticiel suivant lorsque vous apprendrez à [explorer les systèmes d’automatisation marketing à l’aide de l’API](../../explore/marketing-automation.md)du service de flux.
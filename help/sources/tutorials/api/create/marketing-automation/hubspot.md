---
keywords: Experience Platform;accueil;rubriques les plus consultées;zone réactive;zone réactive
solution: Experience Platform
title: Création d’une connexion source HubSpot à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à HubSpot à l’aide de l’API Flow Service.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 33%

---

# Créez une connexion source [!DNL HubSpot] à l’aide de l’API [!DNL Flow Service]

[!DNL Flow Service] sert à collecter et à centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables.

Ce tutoriel utilise l’API [!DNL Flow Service] pour vous guider tout au long des étapes permettant de connecter [!DNL Experience Platform] à [!DNL HubSpot].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL HubSpot] à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL HubSpot], vous devez fournir les propriétés de connexion suivantes :

| Credential | Description |
| ---------- | ----------- |
| `clientId` | ID client associé à votre application [!DNL HubSpot]. |
| `clientSecret` | Le secret client associé à votre application [!DNL HubSpot]. |
| `accessToken` | Jeton d’accès obtenu lors de l’authentification initiale de votre intégration OAuth. |
| `refreshToken` | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |
| `connectionSpec` | Identifiant unique nécessaire pour créer une connexion. L’identifiant de spécification de connexion pour [!DNL HubSpot] est : `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Pour plus d’informations sur la prise en main, reportez-vous à ce [document HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte [!DNL HubSpot], car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer différentes données.

**Format d’API**

```https
POST /connections
```

**Requête**

Pour créer une connexion [!DNL HubSpot], son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L’identifiant de spécification de connexion pour [!DNL HubSpot] est `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

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
| `auth.params.clientId` | ID client associé à votre application [!DNL HubSpot]. |
| `auth.params.clientSecret` | Le secret client associé à votre application [!DNL HubSpot]. |
| `auth.params.accessToken` | Jeton d’accès obtenu lors de l’authentification initiale de votre intégration OAuth. |
| `auth.params.refreshToken` | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

En suivant ce tutoriel, vous avez créé une connexion [!DNL HubSpot] à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant de connexion dans le tutoriel suivant lorsque vous apprendrez à [explorer les systèmes d’automatisation du marketing à l’aide de l’API Flow Service](../../explore/marketing-automation.md).

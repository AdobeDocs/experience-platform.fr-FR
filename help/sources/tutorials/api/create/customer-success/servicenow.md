---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur ServiceNow à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 14%

---


# Création d’un [!DNL ServiceNow] connecteur à l’aide de l’ [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL ServiceNow] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [!DNL Flow Service] API pour vous guider dans les étapes de la connexion [!DNL Experience Platform] à un [!DNL ServiceNow] serveur.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to a [!DNL ServiceNow] server using the [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] se connecter à [!DNL ServiceNow], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL ServiceNow] server. |
| `username` | Nom d’utilisateur utilisé pour la connexion au [!DNL ServiceNow] serveur pour l’authentification. |
| `password` | Mot de passe de connexion au [!DNL ServiceNow] serveur pour l’authentification. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)ServiceNow.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Rechercher les spécifications de connexion

Pour créer une [!DNL ServiceNow] connexion, un ensemble de spécifications de [!DNL ServiceNow] connexion doit exister dans [!DNL Flow Service]. La première étape pour se connecter [!DNL Platform] à [!DNL ServiceNow] est de récupérer ces spécifications.

**Format d’API**

Chaque source disponible possède son propre ensemble de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d&#39;authentification. L’envoi d’une demande de GET au point de `/connectionSpecs` terminaison renverra les spécifications de connexion pour toutes les sources disponibles. Vous pouvez également inclure la requête `property=name=="service-now"` pour obtenir des informations spécifiques pour [!DNL ServiceNow].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="service-now"
```

**Requête**

La requête suivante récupère les spécifications de connexion pour [!DNL ServiceNow].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="service-now"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les spécifications de connexion pour [!DNL ServiceNow], y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion de base.

```json
{
    "items": [
        {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "name": "service-now",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to ServiceNow server",
                        "properties": {
                            "endpoint": {
                                "type": "string",
                                "description": "The endpoint of the ServiceNow server (http://<instance>.service-now.com)."
                            },
                            "username": {
                                "type": "string",
                                "description": "The user name used to connect to the ServiceNow server for authentication."
                            },
                            "password": {
                                "type": "string",
                                "description": "password to connect to the ServiceNow server for authentication.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "endpoint",
                            "username",
                            "password"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Créer une connexion de base

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base est requise par [!DNL ServiceNow] compte, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for service-now",
        "description": "Base connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| ------------- | --------------- |
| `auth.params.server` | Point de terminaison de votre [!DNL ServiceNow] serveur. |
| `auth.params.username` | Nom d’utilisateur utilisé pour la connexion au [!DNL ServiceNow] serveur pour l’authentification. |
| `auth.params.password` | Mot de passe de connexion au [!DNL ServiceNow] serveur pour l’authentification. |
| `connectionSpec.id` | ID de spécification de connexion associé à [!DNL ServiceNow]. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre gestion de la relation client à l’étape suivante.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion [!DNL ServiceNow] de base à l’aide de l’ [!DNL Flow Service] API et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant de connexion de base dans le didacticiel suivant lorsque vous apprendrez à [explorer les systèmes de réussite des clients à l’aide de l’API](../../explore/customer-success.md)Flow Service.
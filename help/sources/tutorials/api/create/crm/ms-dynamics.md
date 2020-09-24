---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Création d’un connecteur Microsoft Dynamics à l’aide de l’API du service de flux
topic: overview
type: Tutorial
description: Ce didacticiel utilise l'API Flow Service pour vous guider à travers les étapes de connexion de Platform à un compte Microsoft Dynamics (ci-après appelé "Dynamics") pour la collecte de données de gestion de la relation client.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 14%

---


# Création d’un [!DNL Microsoft Dynamics] connecteur à l’aide de l’ [!DNL Flow Service] API

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [!DNL Flow Service] API pour vous guider à travers les étapes de connexion [!DNL Platform] à un [!DNL Microsoft Dynamics] (ci-après appelé &quot;Dynamics&quot;) compte pour la collecte de données de gestion de la relation client.

Si vous préférez utiliser l&#39;interface utilisateur dans [!DNL Experience Platform], le didacticiel [sur l&#39;interface utilisateur du connecteur](../../../ui/create/crm/dynamics.md) Dynamics source fournit des instructions détaillées pour exécuter des actions similaires.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): E[!DNL xperience Platform] fournit des sandbox virtuels qui partitionnent une seule [!DNL Platform] instance en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect [!DNL Platform] to a Dynamics account using the [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] se connecter à [!DNL Dynamics], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `serviceUri` | URL de service de votre [!DNL Dynamics] instance. |
| `username` | Nom d’utilisateur de votre compte [!DNL Dynamics] d’utilisateur. |
| `password` | Mot de passe de votre [!DNL Dynamics] compte. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)Dynamics.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Rechercher les spécifications de connexion

Avant de vous connecter [!DNL Platform] à un [!DNL Dynamics] compte, vous devez vérifier que les spécifications de connexion existent pour [!DNL Dynamics]. Si les spécifications de connexion n&#39;existent pas, une connexion ne peut pas être établie.

Chaque source disponible possède son propre ensemble de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d&#39;authentification. Vous pouvez rechercher les spécifications de connexion en [!DNL Dynamics] exécutant une demande de GET et en utilisant les paramètres de requête.

**Format d’API**

L&#39;envoi d&#39;une demande de GET sans paramètres de requête retournera des spécifications de connexion pour toutes les sources disponibles. Vous pouvez inclure la requête `property=name=="dynamics-online"` pour obtenir des informations spécifiques pour [!DNL Dynamics].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Requête**

La requête suivante récupère les spécifications de connexion pour [!DNL Dynamics].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les spécifications de connexion pour [!DNL Dynamics], y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion de base.

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Créer une connexion de base

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base est requise par [!DNL Dynamics] compte, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

Effectuez la requête de POST suivante pour créer une connexion de base.

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
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.serviceUri` | URI de service associé à votre [!DNL Dynamics] instance. |
| `auth.params.username` | Nom d’utilisateur associé à votre [!DNL Dynamics] compte. |
| `auth.params.password` | Mot de passe associé à votre [!DNL Dynamics] compte. |
| `connectionSpec.id` | Spécification `id` de connexion de votre [!DNL Dynamics] compte récupérée à l’étape précédente. |

**Réponse**

Une réponse réussie contient l’identifiant unique de la connexion de base (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion de base pour votre [!DNL Dynamics] compte à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet identifiant de connexion de base dans le didacticiel suivant lorsque vous apprendrez à [explorer les systèmes de gestion de la relation client à l’aide de l’API](../../explore/crm.md)de service de flux.
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur Microsoft Dynamics à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: 6c86cec91774f3444dc90042cd7ad5c71429aabd

---


# Création d’un connecteur Microsoft Dynamics à l’aide de l’API du service de flux

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API du service de flux pour vous guider tout au long des étapes nécessaires à la connexion de Platform à un compte Microsoft Dynamics (ci-après dénommé &quot;Dynamics&quot;) pour la collecte de données CRM.

Si vous préférez utiliser l’interface utilisateur dans Experience Platform, le didacticiel [sur l’interface utilisateur du connecteur source](../../../ui/create/crm/dynamics-salesforce.md) Dynamics ou Salesforce fournit des instructions étape par étape pour exécuter des actions similaires.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir connecter Platform à un compte Dynamics à l’aide de l’API du service de flux.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte à Dynamics, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `serviceUri` | URL de service de votre instance Dynamics. |
| `username` | Nom d’utilisateur de votre compte utilisateur Dynamics. |
| `password` | mot de passe de votre compte Dynamics. |

Pour plus d&#39;informations sur la prise en main, consultez [ce](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)Dynamics.

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

## Rechercher les spécifications de connexion

Avant de connecter Platform à un compte Dynamics, vous devez vérifier que les spécifications de connexion existent pour Dynamics. Si les spécifications de connexion n&#39;existent pas, une connexion ne peut pas être établie.

Chaque source disponible possède son propre jeu de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d’authentification. Vous pouvez rechercher des spécifications de connexion pour Dynamics en exécutant une requête GET et en utilisant des paramètres de .

**Format API**

L&#39;envoi d&#39;une requête GET sans paramètres  retournera les spécifications de connexion pour toutes les sources disponibles. Vous pouvez inclure le `property=name=="dynamics-online"` pour obtenir des informations spécifiques à Dynamics.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Requête**

La requête suivante récupère les spécifications de connexion pour Dynamics.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les spécifications de connexion pour Dynamics, y compris son identifiant unique (`id`). Cet ID est requis à l’étape suivante pour créer une connexion de base.

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

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base est requise par compte Dynamics, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

Effectuez la requête POST suivante pour créer une connexion de base.

**Format API**

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
| `auth.params.serviceUri` | URI de service associé à votre instance Dynamics. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte Dynamics. |
| `auth.params.password` | mot de passe associé à votre compte Dynamics. |
| `connectionSpec.id` | Spécification `id` de connexion de votre compte Dynamics récupérée à l’étape précédente. |

**Réponse**

Une réponse réussie contient l’identifiant unique de la connexion de base (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion de base pour votre compte Dynamics à l’aide des API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet ID de connexion de base dans le didacticiel suivant lorsque vous apprendrez à [explorer des systèmes CRM à l’aide de l’API](../../explore/crm.md)du service de flux.
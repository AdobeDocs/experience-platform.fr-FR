---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur Salesforce à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: cc999ce1ab426f412c0cc2b69173a336a14024f3
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 1%

---


# Création d’un connecteur Salesforce à l’aide de l’API du service de flux

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API de service de flux pour vous guider tout au long des étapes de connexion de la plate-forme à un compte Salesforce pour la collecte de données de gestion de la relation client.

Si vous préférez utiliser l’interface utilisateur dans Experience Platform, le didacticiel [sur l’interface utilisateur du connecteur source](../../../ui/create/crm/dynamics-salesforce.md) Dynamics ou Salesforce fournit des instructions détaillées pour exécuter des actions similaires.

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plate-forme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour connecter la plate-forme à un compte Salesforce à l’aide de l’API de service de flux.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte à Salesforce, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `environmentUrl` | URL de l&#39;instance source Salesforce. |
| `username` | Nom d’utilisateur du compte utilisateur Salesforce. |
| `password` | Mot de passe du compte utilisateur Salesforce. |
| `securityToken` | Jeton de sécurité pour le compte utilisateur Salesforce. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)Salesforce.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Rechercher les spécifications de connexion

Avant de connecter Plateforme à un compte Salesforce, vous devez vérifier que les spécifications de connexion existent pour Salesforce. Si les spécifications de connexion n&#39;existent pas, une connexion ne peut pas être établie.

Chaque source disponible possède son propre ensemble de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d&#39;authentification. Vous pouvez vérifier les spécifications de connexion de Salesforce en exécutant une requête GET et en utilisant des paramètres de requête.

**Format d’API**

L&#39;envoi d&#39;une demande GET sans paramètres de requête retournera les spécifications de connexion pour toutes les sources disponibles. Vous pouvez inclure la requête `property=name=="salesforce"` pour obtenir des informations spécifiques à Salesforce.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce"
```

**Requête**

La requête suivante récupère les spécifications de connexion pour Salesforce.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name==%22salesforce%22' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les spécifications de connexion pour Salesforce, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion de base.

```json
{
    "items": [
        {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "name": "salesforce",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Créer une connexion de base

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base est requise par compte Salesforce, car elle peut être utilisée pour créer plusieurs connecteurs de source afin d’importer des données différentes.

Effectuez la requête POST suivante pour créer une connexion de base.

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
        "name": "Salesforce Base Connection",
        "description": "Base connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.username` | Nom d’utilisateur associé à votre compte Salesforce. |
| `auth.params.password` | Mot de passe associé à votre compte Salesforce. |
| `auth.params.securityToken` | Jeton de sécurité associé à votre compte Salesforce. |
| `connectionSpec.id` | Spécification `id` de connexion de votre compte Salesforce récupérée à l&#39;étape précédente. |

**Réponse**

Une réponse réussie contient l&#39;identifiant unique (`id`) de la connexion de base. Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion de base pour votre compte Salesforce à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet identifiant de connexion de base dans le didacticiel suivant lorsque vous apprendrez à [explorer les systèmes de gestion de la relation client à l’aide de l’API](../../explore/crm.md)de service de flux.
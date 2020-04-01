---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Créer des destinations de marketing par courrier électronique
topic: tutorial
translation-type: tm+mt
source-git-commit: 7ee83b5bf14ec802801cfbc17141c02ceeaccd82

---


# Créez des destinations de marketing par courrier électronique et activez les données dans la plateforme de données clientes en temps réel d’Adobe.

Ce didacticiel explique comment utiliser les appels d’API pour établir une connexion aux données d’Adobe Experience Platform, créer une destination [marketing par](../../rtcdp/destinations/email-marketing-destinations.md)courrier électronique, créer un flux de données vers votre nouvelle destination créée et activer les données vers votre nouvelle destination créée.

Ce didacticiel utilise la destination Adobe Campaign  dans tous les exemples, mais les étapes sont identiques pour toutes les destinations de marketing par courrier électronique.

![Présentation : étapes de création d’une destination et d’activation de segments](../images/destinations/flow-api-destinations-steps-overview.png)

Si vous préférez utiliser l’interface utilisateur du CDP en temps réel d’Adobe pour connecter une destination et activer des données, reportez-vous aux didacticiels [Connexion d’une destination](../../rtcdp/destinations/connect-destination.md) et [Activation des  et des segments de à une destination](../../rtcdp/destinations/activate-destinations.md) .

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
* [Service](../../catalog/home.md)de catalogue : Le catalogue est le système d’enregistrement de l’emplacement et de la lignée des données dans la plateforme d’expérience.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour activer les données vers des destinations marketing par courrier électronique dans Adobe CDP en temps réel.

### Collecte des informations d’identification requises

Pour terminer les étapes de ce didacticiel, vous devez disposer des informations d’identification suivantes, selon le type de destination vers laquelle vous connectez et activez les segments.

* Pour les connexions Amazon S3 aux plateformes de marketing par courrier électronique : `accessId`, `secretKey`
* Pour les connexions SFTP aux plateformes de marketing par courrier électronique : `domain`, `port`, `username`, `password` ou `ssh key` (selon la méthode de connexion à l’emplacement FTP)

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes obligatoires et facultatifs

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Les ressources de la plateforme d’expérience peuvent être isolées dans des sandbox virtuels spécifiques. Dans les demandes aux API de plateforme, vous pouvez spécifier le nom et l’ID du sandbox dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name : `{SANDBOX_NAME}`

>[!Note] :
>Pour plus d’informations sur les sandbox dans Experience Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type : `application/json`

<!--

### Definitions

Before starting this tutorial, familiarize yourself with the following terms which we'll use throughout the tutorial:

**Flow**: 

**Base Connection**: 

**Target Connection**: 

**Source Connection**: 

-->

### Documentation Swagger

Ce didacticiel de Swagger contient une documentation de référence pour tous les appels d’API. Voir https://platform.adobe.io/data/foundation/flowservice/swagger#/. Nous vous recommandons d’utiliser ce didacticiel et la page de documentation Swagger en parallèle.

## Obtenir le  des destinations disponibles {#get-the-list-of-available-destinations}

![Etape de présentation des étapes de destination 1](../images/destinations/flow-api-destinations-step1.png)

Dans un premier temps, vous devez décider vers quelle destination marketing par courrier électronique activer les données. Pour commencer, effectuez un appel pour demander un  de destinations disponibles auquel vous pouvez vous connecter et activer des segments. Effectuez la requête GET suivante sur le `connectionSpecs` point de terminaison pour renvoyer un de destinations disponibles :

**Format API**

```http
GET /connectionSpecs
```

**Requête**

<!--

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \    
    -H 'Content-Type: application/json' \
```

-->

```
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Réponse**

Une réponse réussie contient un  de destinations disponibles et leurs identifiants uniques (`id`). Stockez la valeur de la destination que vous prévoyez d’utiliser, car elle sera requise dans d’autres étapes. Si, par exemple, vous souhaitez vous connecter et diffuser des segments vers  Adobe Campaign, recherchez le fragment de code suivant dans la réponse :

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Connexion à vos données de plateforme d’expérience {#connect-to-your-experience-platform-data}

![Etape de présentation des étapes de destination 2](../images/destinations/flow-api-destinations-step2.png)

Ensuite, vous devez vous connecter à vos données de plateforme d’expérience afin de pouvoir exporter  données et les activer dans votre destination préférée. Il s&#39;agit de deux étapes décrites ci-après.

1. Tout d’abord, vous devez effectuer un appel pour autoriser l’accès à vos données dans Experience Platform, en configurant une connexion de base.
2. Ensuite, à l’aide de l’ID de connexion de base, vous effectuerez un autre appel au cours duquel vous créez une connexion source, qui établit la connexion aux données de votre plateforme d’expérience.


### Autoriser l’accès à vos données dans Experience Platform

**Format API**

```http
POST /connections
```

**Requête**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            }
           }'
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME} \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`: Utilisez l’ID de spécification de connexion pour le service de  unifié - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Réponse**

Une réponse réussie contient l’identifiant unique de la connexion de base (`id`). Stockez cette valeur comme elle est requise à l’étape suivante pour créer la connexion source.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Connexion à vos données de plateforme d’expérience

**Format API**

```http
POST /sourceConnections
```

**Requête**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
  "name": "Connecting to Unified Profile Service",
  "description": "Optional",
  "baseConnectionId": "{BASE_CONNECTION_ID}",
  "connectionSpec": {
    "id": "{CONNECTION_SPEC}",
    "version": "1.0"
  },
  "data": {
    "format": "CSV",
    "schema": null
  }
  }
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Utilisez l’ID que vous avez obtenu à l’étape précédente.
* `{CONNECTION_SPEC_ID}`: Utilisez l’ID de spécification de connexion pour le service de  unifié - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la nouvelle connexion source au service de  unifié. Ceci confirme que vous êtes connecté avec succès à vos données de plateforme d’expérience. Stocker cette valeur comme elle est requise dans une étape ultérieure.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Se connecter à la destination marketing par courrier électronique {#connect-to-email-marketing-destination}

![Etape de présentation des étapes de destination 3](../images/destinations/flow-api-destinations-step3.png)

Au cours de cette étape, vous configurez une connexion à la destination marketing par courrier électronique souhaitée. Il s&#39;agit de deux étapes décrites ci-après.

1. Tout d’abord, vous devez effectuer un appel pour autoriser l’accès au de messagerie en configurant une connexion de base.
2. Ensuite, à l’aide de l’ID de connexion de base, vous effectuerez un autre appel lors de la création d’une connexion de , qui spécifie l’emplacement dans votre compte  de où les données exportées seront diffusées, ainsi que le format des données qui seront exportées.

### Autoriser l’accès à la destination marketing par courrier électronique

**Format API**

```http
POST /connections
```

**Requête**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "S3 Connection for Adobe Campaign",
            "description": "ACME company holiday campaign",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            },
            "auth": {
                "specName": "{S3 or SFTP}",
                "params": {
                    "accessId": "{ACCESS_ID}",
                    "secretKey": "{SECRET_KEY}"
                }
            }
           }'
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "your company's holiday campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{S3 or SFTP}",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Utilisez l’ID de spécification de connexion que vous avez obtenu lors de l’étape [Obtenez le  des destinations](#get-the-list-of-available-destinations)disponibles.
* `{S3 or SFTP}`: renseignez le type de connexion souhaité pour cette destination. Dans le catalogue [de](../../rtcdp/destinations/destinations-catalog.md)destination, faites défiler l’écran jusqu’à la destination préférée pour voir si les types de connexion S3 et/ou SFTP sont pris en charge.
* `{ACCESS_ID}`: Votre ID d’accès pour votre  Amazon S3 l’emplacement  de votre.
* `{SECRET_KEY}`: Votre clé secrète pour votre  Amazon S3 l’emplacement  de votre.

**Réponse**

Une réponse réussie contient l’identifiant unique de la connexion de base (`id`). Stocker cette valeur comme elle est requise à l’étape suivante pour créer une connexion .

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Spécifier   emplacement et format de données du

**Format API**

```http
POST /targetConnections
```

**Requête**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \    
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
   "baseConnectionId": "{BASE_CONNECTION_ID}",
   "name": "TargetConnection for Adobe Campaign",
   "data": {
       "format": "CSV",
       "schema": {
           "id": "1.0",
           "version": "1.0"
       },
    "connectionSpec": {
    "id": "{CONNECTION_SPEC_ID}",
    "version": "1.0"
   },
   "params": {
       "mode": "S3",
       "bucketName": "{BUCKETNAME}",
       "path": "{FILEPATH}"
    }
    }
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnection": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKETNAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Utilisez l’ID de connexion de base que vous avez obtenu à l’étape ci-dessus.
* `{CONNECTION_SPEC_ID}`: Utilisez les spécifications de connexion que vous avez obtenues lors de l’étape [Obtenez le  des destinations](#get-the-list-of-available-destinations)disponibles.
* `{BUCKETNAME}`: Votre compartiment Amazon S3, où le CDP en temps réel dépose l’exportation des données.
* `{FILEPATH}`: Chemin d’accès dans le répertoire du compartiment Amazon S3 où le CDP en temps réel dépose l’exportation des données.

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion de l’ à votre destination de marketing par courrier électronique. Stockez cette valeur comme elle est requise dans les étapes ultérieures.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Création d’un flux de données

![Étape 4 de présentation des étapes de destination](../images/destinations/flow-api-destinations-step4.png)

A l’aide des ID que vous avez obtenus lors des étapes précédentes, vous pouvez désormais créer un flux de données entre les données de votre plateforme d’expérience et la destination vers laquelle vous allez activer les données. Considérez cette étape comme la construction du pipeline, par lequel les données seront acheminées ultérieurement, entre la plateforme d’expérience et la destination souhaitée.

Pour créer un flux de données, exécutez une requête POST, comme illustré ci-dessous, tout en fournissant les valeurs mentionnées ci-dessous dans la charge utile.

Effectuez la requête POST suivante pour créer un flux de données.

**Format API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ],
        "transformations": [
            {
                "name": "GeneralTransform",
                "params": {
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

* `{FLOW_SPEC_ID}`: Utilisez le flux pour la destination marketing par courrier électronique à laquelle vous souhaitez vous connecter. Pour obtenir la spécification de flux, effectuez une opération GET sur le `flowspecs` point de fin. Voir la documentation de Swagger ici : https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. Dans la réponse, recherchez `upsTo` et copiez l’ID correspondant de la destination marketing par courrier électronique à laquelle vous souhaitez vous connecter. Par exemple, pour  Adobe Campaign, recherchez `upsToCampaign` et copiez le `id` paramètre.
* `{SOURCE_CONNECTION_ID}`: Utilisez l’ID de connexion source que vous avez obtenu lors de l’étape [Connexion à votre plateforme](#connect-to-your-experience-platform-data)d’expérience.
* `{TARGET_CONNECTION_ID}`: Utilisez l’ID de connexion  que vous avez obtenu lors de l’étape [Connexion à la destination](#connect-to-email-marketing-destination)marketing par courrier électronique.

**Réponse**

Une réponse réussie renvoie l’ID (`id`) du flux de données nouvellement créé et une `etag`. Notez les deux valeurs. comme vous le feriez à l’étape suivante, pour activer les segments.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Activer les données vers votre nouvelle destination

![Etape de présentation des étapes de destination 5](../images/destinations/flow-api-destinations-step5.png)

Après avoir créé toutes les connexions et le flux de données, vous pouvez désormais activer vos données  de sur la plateforme de marketing par courrier électronique. Au cours de cette étape, vous sélectionnez les segments et les attributs de que vous envoyez à la destination et vous pouvez planifier et envoyer des données à la destination.

Pour activer les segments vers votre nouvelle destination, vous devez effectuer une opération JSON PATCH, comme dans l’exemple ci-dessous. Vous pouvez activer plusieurs segments et attributs  de dans un seul appel. Pour en savoir plus sur JSON PATCH, consultez la spécification [](https://tools.ietf.org/html/rfc6902)RFC.

**Format API**

```http
PATCH /flows
```

**Requête**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "operator": "EXISTS",
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

* `{DATAFLOW_ID}`: Utilisez le flux de données que vous avez obtenu à l’étape précédente.
* `{ETAG}`: Utilisez la balise que vous avez obtenue à l’étape précédente.
* `{SEGMENT_ID}`: Indiquez l’ID de segment que vous souhaitez exporter vers cette destination. Pour récupérer les ID de segment pour les segments que vous souhaitez activer, accédez à https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/ et recherchez l’ `GET /segment/jobs` opération.
* `{PROFILE_ATTRIBUTE}`: Par exemple, `"person.lastName"`

**Réponse**

Recherchez une réponse 202 OK. Aucun corps de réponse n’est renvoyé. Pour vérifier que la requête était correcte, voir l’étape suivante, Validez le flux de données.

## Validation du flux de données

![Etape de présentation des étapes de destination 6](../images/destinations/flow-api-destinations-step6.png)

En guise de dernière étape du didacticiel, vous devez vérifier que les segments et les attributs  ont bien été mappés au flux de données.

Pour valider ce paramètre, exécutez la requête GET suivante :

**Format API**

```http
GET /flows
```

**Requête**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Utilisez le flux de données de l’étape précédente.
* `{ETAG}`: Utilisez l’étiquette de l’étape précédente.

**Réponse**

La réponse renvoyée doit inclure dans le `transformations` paramètre les segments et les attributs de que vous avez envoyés à l’étape précédente. Voici un exemple `transformations` de paramètre dans la réponse :

```
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                "selectors": []
            },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à connecter le CDP en temps réel à l’une de vos destinations de marketing par courrier électronique préférées et à configurer un flux de données vers la destination correspondante. Les données sortantes peuvent désormais être utilisées dans la destination pour les campagnes par courrier électronique, les publicités ciblées et de nombreux autres cas d’utilisation. Pour plus d’informations, consultez les pages suivantes :

* [Présentation des destinations](../../rtcdp/destinations/destinations-overview.md)
* [Présentation du catalogue des destinations](../../rtcdp/destinations/destinations-catalog.md)
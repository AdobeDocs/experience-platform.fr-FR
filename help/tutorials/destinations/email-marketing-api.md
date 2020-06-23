---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Créer des destinations de marketing par courriel
topic: tutorial
translation-type: tm+mt
source-git-commit: ed9d6eadeb00db51278ea700f7698a1b5590632f
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---


# Créez des destinations de marketing par courrier électronique et activez les données dans Adobe Real-time Customer Data Platform

Ce didacticiel explique comment utiliser les appels d’API pour se connecter à vos données d’Adobe Experience Platform, créer une destination [marketing par](../../rtcdp/destinations/email-marketing-destinations.md)courriel, créer un flux de données vers votre nouvelle destination créée et activer les données vers votre nouvelle destination créée.

Ce didacticiel utilise la destination de l’Adobe Campaign dans tous les exemples, mais les étapes sont identiques pour toutes les destinations de marketing par courriel.

![Présentation : étapes de création d’une destination et d’activation de segments](../images/destinations/flow-api-destinations-steps-overview.png)

Si vous préférez utiliser l’interface utilisateur dans Adobe Real-time CDP pour connecter une destination et activer des données, consultez les didacticiels [Connexion d’une destination](../../rtcdp/destinations/connect-destination.md) et [Activation de profils et de segments à une destination](../../rtcdp/destinations/activate-destinations.md) .

## Prise en main

Ce guide exige une compréhension pratique des éléments suivants de l&#39;Adobe Experience Platform :

* [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
* [Service](../../catalog/home.md)de catalogue : Le catalogue est le système d’enregistrement pour l’emplacement et le lignage des données dans l’Experience Platform.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance Platform unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour activer les données vers les destinations de marketing par courriel dans Adobe Real-time CDP.

### Collecte des informations d’identification requises

Pour suivre les étapes de ce didacticiel, vous devez disposer des informations d’identification suivantes, en fonction du type de destinations vers lesquelles vous connectez et activez les segments.

* Pour les connexions Amazon S3 aux plateformes de marketing par courrier électronique : `accessId`, `secretKey`
* Pour les connexions SFTP aux plateformes de marketing par courrier électronique : `domain`, `port`, `username`, `password` ou `ssh key` (selon la méthode de connexion à l’emplacement FTP)

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de l’Experience Platform.

### Rassembler les valeurs des en-têtes obligatoires et facultatifs

Pour passer des appels aux API Platform, vous devez d’abord suivre le didacticiel [d’](../authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Les ressources de l&#39;Experience Platform peuvent être isolées dans des sandbox virtuels spécifiques. Dans les demandes aux API Platform, vous pouvez spécifier le nom et l’ID du sandbox dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name : `{SANDBOX_NAME}`

>[!Note] :
>Pour plus d’informations sur les sandbox dans l’Experience Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

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

Vous trouverez dans ce didacticiel de Swagger la documentation de référence correspondante pour tous les appels d’API. Reportez-vous à la documentation de l’API [Flow Service sur Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). Nous vous recommandons d’utiliser ce didacticiel et la page de documentation Swagger en parallèle.

## Obtenir la liste des destinations disponibles {#get-the-list-of-available-destinations}

![Etapes de destination - Présentation de l’étape 1](../images/destinations/flow-api-destinations-step1.png)

Dans un premier temps, vous devez décider à quelle destination marketing par courriel activer les données. Pour commencer, effectuez un appel pour demander une liste de destinations disponibles à laquelle vous pouvez connecter et activer des segments. Effectuez la requête GET suivante sur le point de `connectionSpecs` terminaison pour renvoyer une liste de destinations disponibles :

**Format d’API**

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

Une réponse réussie contient une liste de destinations disponibles et leurs identifiants uniques (`id`). Stockez la valeur de la destination que vous prévoyez d’utiliser, car elle sera nécessaire dans d’autres étapes. Par exemple, si vous souhaitez connecter et diffuser des segments à l’Adobe Campaign, recherchez le fragment de code suivant dans la réponse :

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Se connecter à vos données d’Experience Platform {#connect-to-your-experience-platform-data}

![Etape de présentation des étapes de destination 2](../images/destinations/flow-api-destinations-step2.png)

Ensuite, vous devez vous connecter à vos données d’Experience Platform afin de pouvoir exporter les données de profil et les activer dans votre destination préférée. Il s&#39;agit de deux étapes décrites ci-dessous.

1. Tout d&#39;abord, vous devez effectuer un appel pour autoriser l&#39;accès à vos données dans l&#39;Experience Platform, en configurant une connexion de base.
2. Ensuite, en utilisant l&#39;ID de connexion de base, vous effectuerez un autre appel dans lequel vous créez une connexion source, qui établit la connexion à vos données Experience Platform.


### Autoriser l’accès à vos données dans l’Experience Platform

**Format d’API**

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


* `{CONNECTION_SPEC_ID}`: Utilisez l&#39;identifiant de spécification de connexion pour Unified Profil Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Réponse**

Une réponse réussie contient l&#39;identifiant unique (`id`) de la connexion de base. Conservez cette valeur comme elle est requise à l’étape suivante pour créer la connexion source.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Se connecter à vos données d’Experience Platform

**Format d’API**

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
* `{CONNECTION_SPEC_ID}`: Utilisez l&#39;identifiant de spécification de connexion pour Unified Profil Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la nouvelle connexion source au service de Profil unifié. Ceci confirme que vous avez réussi à vous connecter à vos données Experience Platform. Conservez cette valeur telle qu’elle est requise dans une étape ultérieure.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Se connecter à la destination marketing par courrier électronique {#connect-to-email-marketing-destination}

![Etape de présentation des étapes de destination 3](../images/destinations/flow-api-destinations-step3.png)

Au cours de cette étape, vous configurez une connexion à la destination marketing par courrier électronique de votre choix. Il s&#39;agit de deux étapes décrites ci-dessous.

1. Tout d&#39;abord, vous devez effectuer un appel pour autoriser l&#39;accès au prestataire de messagerie en configurant une connexion de base.
2. Ensuite, à l’aide de l’ID de connexion de base, vous effectuerez un autre appel dans lequel vous créez une connexion de cible, qui spécifie l’emplacement dans votre compte d’enregistrement où les données exportées seront livrées, ainsi que le format des données qui seront exportées.

### Autoriser l’accès à la destination marketing par courrier électronique

**Format d’API**

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

* `{CONNECTION_SPEC_ID}`: Utilisez l&#39;identifiant de spécification de connexion que vous avez obtenu lors de l&#39;étape [Obtenir la liste des destinations](#get-the-list-of-available-destinations)disponibles.
* `{S3 or SFTP}`: renseignez le type de connexion souhaité pour cette destination. Dans le catalogue [de](../../rtcdp/destinations/destinations-catalog.md)destination, faites défiler l’écran vers votre destination préférée pour voir si les types de connexion S3 et/ou SFTP sont pris en charge.
* `{ACCESS_ID}`: Votre ID d’accès pour votre emplacement d’enregistrement Amazon S3.
* `{SECRET_KEY}`: Votre clé secrète pour votre emplacement d’enregistrement Amazon S3.

**Réponse**

Une réponse réussie contient l&#39;identifiant unique (`id`) de la connexion de base. Conservez cette valeur comme elle est requise à l’étape suivante pour créer une connexion à une cible.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Définition de l’emplacement et du format des données de l’enregistrement

**Format d’API**

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
* `{CONNECTION_SPEC_ID}`: Utilisez la spécification de connexion que vous avez obtenue lors de l&#39;étape [Obtenir la liste des destinations](#get-the-list-of-available-destinations)disponibles.
* `{BUCKETNAME}`: Votre compartiment Amazon S3, où CDP en temps réel dépose l’exportation de données.
* `{FILEPATH}`: Chemin d’accès dans le répertoire du compartiment Amazon S3 où le CDP en temps réel dépose l’exportation des données.

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion de cible à votre destination de marketing par courrier électronique. Stocker cette valeur comme elle est requise dans les étapes ultérieures.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Création d’un flux de données

![Etapes de destination - présentation de l’étape 4](../images/destinations/flow-api-destinations-step4.png)

A l’aide des identifiants que vous avez obtenus lors des étapes précédentes, vous pouvez maintenant créer un flux de données entre les données de votre Experience Platform et la destination vers laquelle vous allez activer les données. Considérez cette étape comme la construction du pipeline, à travers lequel les données seront acheminées ultérieurement, entre l’Experience Platform et la destination souhaitée.

Pour créer un flux de données, exécutez une requête POST, comme illustré ci-dessous, tout en fournissant les valeurs mentionnées ci-dessous dans la charge utile.

Effectuez la requête POST suivante pour créer un flux de données.

**Format d’API**

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

* `{FLOW_SPEC_ID}`: Utilisez le flux pour la destination marketing par courrier électronique à laquelle vous souhaitez vous connecter. Pour obtenir la spécification de flux, effectuez une opération GET sur le `flowspecs` point de terminaison. Voir la documentation de Swagger ici : https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. Dans la réponse, recherchez `upsTo` et copiez l’ID correspondant de la destination marketing par courrier électronique à laquelle vous souhaitez vous connecter. Par exemple, pour l’Adobe Campaign, recherchez `upsToCampaign` et copiez le `id` paramètre.
* `{SOURCE_CONNECTION_ID}`: Utilisez l’ID de connexion source que vous avez obtenu lors de l’étape [Connexion à votre Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Utilisez l’ID de connexion à la cible que vous avez obtenu lors de l’étape [Connexion à la destination](#connect-to-email-marketing-destination)marketing par courrier électronique.

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du flux de données nouvellement créé et un `etag`identifiant. Notez les deux valeurs. comme vous le ferez à l’étape suivante, pour activer les segments.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Activer les données vers votre nouvelle destination

![Etape de présentation des étapes de destination 5](../images/destinations/flow-api-destinations-step5.png)

Après avoir créé toutes les connexions et le flux de données, vous pouvez désormais activer vos données de profil sur la plateforme de marketing par courrier électronique. Au cours de cette étape, vous sélectionnez les segments et les attributs de profil que vous envoyez à la destination et vous pouvez planifier et envoyer des données à la destination.

Pour activer des segments sur votre nouvelle destination, vous devez effectuer une opération JSON PATCH, comme dans l’exemple ci-dessous. Vous pouvez activer plusieurs segments et attributs de profil en un seul appel. Pour en savoir plus sur JSON PATCH, consultez la spécification [](https://tools.ietf.org/html/rfc6902)RFC.

**Format d’API**

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
* `{SEGMENT_ID}`: Indiquez l’ID de segment à exporter vers cette destination. Pour récupérer les ID de segment pour les segments que vous souhaitez activer, accédez à https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/ et recherchez l’ `GET /segment/jobs` opération.
* `{PROFILE_ATTRIBUTE}`: Par exemple, `"person.lastName"`

**Réponse**

Recherchez une réponse 202 OK. Aucun corps de réponse n’est renvoyé. Pour vérifier que la requête était correcte, voir l’étape suivante, Valider le flux de données.

## Validation du flux de données

![Etape de présentation des étapes de destination 6](../images/destinations/flow-api-destinations-step6.png)

En guise de dernière étape du didacticiel, vous devez vérifier que les segments et les attributs de profil ont bien été mappés au flux de données.

Pour valider ce paramètre, effectuez la requête GET suivante :

**Format d’API**

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
* `{ETAG}`: Utilisez la balise de l’étape précédente.

**Réponse**

La réponse renvoyée doit inclure dans le `transformations` paramètre les segments et les attributs de profil que vous avez envoyés à l’étape précédente. Un exemple `transformations` de paramètre de la réponse peut se présenter comme suit :

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

En suivant ce didacticiel, vous avez réussi à connecter le CDP en temps réel à l’une de vos destinations de marketing par courrier électronique préférées et à configurer un flux de données vers la destination correspondante. Les données sortantes peuvent désormais être utilisées dans la destination pour les campagnes par courriel, les publicités ciblées et de nombreux autres cas d’utilisation. Consultez les pages suivantes pour plus de détails :

* [Présentation des destinations](../../rtcdp/destinations/destinations-overview.md)
* [Présentation du catalogue des destinations](../../rtcdp/destinations/destinations-catalog.md)
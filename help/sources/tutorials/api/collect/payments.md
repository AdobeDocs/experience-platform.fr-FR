---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Collecte de données de paiement via des connecteurs source et des API
topic: overview
translation-type: tm+mt
source-git-commit: 3d8682eb1a33b7678ed814e5d6d2cb54d233c03e

---


# Collecte de données de paiement via des connecteurs source et des API

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel décrit les étapes de récupération des données d’une application de paiement et de leur assimilation dans la plateforme par le biais des connecteurs source et des API.

## Prise en main

Ce didacticiel vous demande d&#39;avoir accès à un système de paiement via une connexion de base valide, ainsi que des informations sur le fichier que vous souhaitez importer dans Platform (y compris le chemin et la structure du fichier). Si vous ne disposez pas de ces informations, reportez-vous au didacticiel sur l’ [exploration d’une application de paiements à l’aide de l’API](../explore/payments.md) de service de flux avant d’essayer ce didacticiel.

Ce didacticiel vous demande également de bien comprendre les composants suivants d’Adobe Experience Platform :

* [Système](../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Guide](../../../../xdm/api/getting-started.md)du développeur du Registre des  : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels vers l’API de Registre . Cela inclut votre `{TENANT_ID}`, le concept de &quot;&quot; et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
* [Service](../../../../catalog/home.md)de catalogue : Le catalogue est le système d’enregistrement de l’emplacement et de la lignée des données dans la plateforme d’expérience.
* [Importation](../../../../ingestion/batch-ingestion/overview.md)par lot : L’API d’assimilation par lot vous permet d’assimiler des données dans la plateforme d’expérience sous forme de fichiers de commandes.
* [Sandbox](../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à une application de paiements à l’aide de l’API de service de flux.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type : `application/json`

## Création d’une classe XDM ad hoc et d’une  de

Pour importer des données externes dans Platform via des connecteurs source, une classe XDM ad hoc et un  de doivent être créés pour les données source brutes.

Pour créer une classe ad hoc et un  de, suivez les étapes décrites dans le didacticiel [ de](../../../../xdm/tutorials/ad-hoc.md)ad hoc. Lors de la création d’une classe ad hoc, tous les champs trouvés dans les données source doivent être décrits dans le corps de la requête.

Continuez à suivre les étapes décrites dans le guide du développeur jusqu’à ce que vous ayez créé un  ad hoc. Obtenez et stockez l’identifiant unique (`$id`) du  ad hoc, puis passez à l’étape suivante de ce didacticiel.

## Création d’une connexion source {#source}

Une fois un XDM ad hoc créé, vous pouvez désormais créer une connexion source à l’aide d’une requête POST sur l’API du service de flux. Une connexion source se compose d’un ID de connexion, d’un fichier de données source et d’une référence au qui décrit les données source.

**Format API**

```https
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal source connection",
        "baseConnectionId": "24151d58-ffa7-4960-951d-58ffa7396097",
        "description": "Paypal",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/396f583b57577b2f2fca79c2cb88e9254992f5fa70ce5f1a",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "PayPal.Catalog_Products"
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | ID de connexion de votre application de paiements |
| `data.schema.id` | Le  `$id` du XDM ad hoc. |
| `params.path` | Chemin d’accès du fichier source. |
| `connectionSpec.id` | ID de spécification de connexion de votre application de paiements. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source nouvellement créée. Cet ID est requis dans les étapes suivantes pour créer une connexion .

```json
{
    "id": "2c48a152-3d49-43cb-88a1-523d49e3cbcb",
    "etag": "\"8000c843-0000-0200-0000-5e8917ea0000\""
}
```

## Création d’un  XDM {#target}

Dans les étapes précédentes, un XDM ad hoc a été créé pour structurer les données source. Pour que les données source soient utilisées dans Platform, un de  doit également être créé pour structurer les données source en fonction de vos besoins. Le  est ensuite utilisé pour créer un jeu de données de plateforme dans lequel les données source sont contenues. Ce  le XDM  étend également la classe de  XDM individuels.

Un XDM  peut être créé en exécutant une requête POST sur l’API [de registre de l’](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Si vous préférez utiliser l’interface utilisateur dans la plateforme d’expérience, le didacticiel [de l’éditeur de ](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-ui.html) fournit des instructions étape par étape pour exécuter des actions similaires dans l’éditeur de  de.

**Format API**

```https
POST /tenant/schemas
```

**Requête**

L’exemple de requête suivant crée un  XDM qui étend la classe de XDM Individuel.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Target schema for payments",
        "description": "Target schema for payments",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            },
                    {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle  de, y compris son identifiant unique (`$id`). Cet identifiant est requis dans les étapes suivantes pour créer un jeu de données, un mappage et un flux de données .

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
    "meta:altId": "_{TENANT_ID}.schemas.14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for payments",
    "type": "object",
    "description": "Target schema for Paypal",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1586042956286,
        "repo:lastModifiedDate": 1586042956286,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "952e8912724d7f43cbc1471e3987bc5b6899519c186126b7c50619f2dddf8650"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’un jeu de données de 

Vous pouvez créer un jeu de données  en exécutant une requête POST sur l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog Service, en indiquant l’ID du  de  dans la charge utile.

**Format API**

```https
POST /dataSets
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target dataset for payments",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `schemaRef.id` | Le `$id` du XDM . |

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;ID du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’ID du jeu de données est une chaîne générée par le système en lecture seule qui est utilisée pour référencer le jeu de données dans les appels d’API. Stockez l’ID du jeu de données  du, comme requis dans les étapes suivantes pour créer une connexion  et un flux de données.

```json
[
    "@/dataSets/5e8918669cbbee18ad9771f3"
]
```

## Création d’une connexion de base de jeux de données

Pour importer des données externes dans la plateforme, une connexion de base de données de jeu de plateformes d’expérience doit d’abord être acquise.

Pour créer une connexion de base de jeux de données, suivez les étapes décrites dans le didacticiel [sur la connexion de base de jeux de](../create-dataset-base-connection.md)données.

Continuez à suivre les étapes décrites dans le guide du développeur jusqu’à ce que vous ayez créé une connexion de base de jeux de données. Récupérez et stockez l’identifiant unique (`$id`), puis utilisez-le comme identifiant de connexion à l’étape suivante pour créer une connexion .

## Création d’une connexion 

Vous disposez maintenant des identifiants uniques pour une connexion de base de jeux de données, un  de  et un jeu de données de  dedonnées. Vous pouvez désormais créer une connexion  à l’aide de l’API du service de flux pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format API**

```https
POST /targetConnections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "72c47da8-c225-40c0-847d-a8c22550c01b",
        "name": "Target Connection for payments",
        "description": "Target Connection for payments",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722"
            }
        },
        "params": {
            "dataSetId": "5e8918669cbbee18ad9771f3"
        },
            "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | ID de votre connexion de base de jeux de données. |
| `data.schema.id` | Le `$id` du XDM . |
| `params.dataSetId` | ID du jeu de données . |
| `connectionSpec.id` | ID de spécification de connexion pour votre application de paiements. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion . Cette valeur est requise dans une étape ultérieure pour créer un flux de données.

```json
{
    "id": "c8e12917-ac33-44d7-a129-17ac3364d7b7",
    "etag": "\"0f015874-0000-0200-0000-5e8918e60000\""
}
```

## Création d’un mappage {#mapping}

Pour que les données source soient assimilées dans un jeu de données  de, elles doivent d’abord être mappées sur le auquel le jeu de données de l’analyse adhère. Pour ce faire, vous devez exécuter une requête POST sur l’API [du service de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) conversion avec des mappages de données définis dans la charge utile de la demande.

**Format API**

```https
POST /mappingSets
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Product_Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.name",
                "sourceAttribute": "Product_Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.description",
                "sourceAttribute": "Description",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.type",
                "sourceAttribute": "Type",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `xdmSchema` | Le `$id` du XDM . |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Cet identifiant est requis dans une étape ultérieure pour créer un flux de données.

```json
{
    "id": "b54a8dc38e8d4e31a2dc096e413ae8e5",
    "version": 0,
    "createdDate": 1586043319604,
    "modifiedDate": 1586043319604,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Spécifications de flux de données de recherche {#specs}

Un flux de données est responsable de la collecte de données à partir de sources et de leur transmission dans la plateforme. Pour créer un flux de données, vous devez d’abord obtenir les spécifications du flux de données en exécutant une requête GET à l’API du service de flux. Les spécifications du flux de données sont chargées de collecter les données d&#39;une base de données externe ou d&#39;un système NoSQL.

**Format API**

```https
GET /flowSpecs?property=name=="CRMToAEP"
```

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```


**Réponse**

Une réponse réussie renvoie les détails de la spécification de flux de données responsable de l’importation des données de votre application de paiements dans Platform. Cet identifiant est requis à l’étape suivante pour créer un nouveau flux de données.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            }
        }
    ]
}
```

## Création d’un flux de données

La dernière étape vers la collecte des données est de créer un flux de données. A ce stade, vous devez préparer les valeurs requises suivantes :

* [ID de connexion source](#source)
* [ID de connexion](#target)
* [ID de mappage](#mapping)
* [ID de spécification du flux de données](#specs)

Un flux de données est responsable de la planification et de la collecte de données à partir d’une source. Vous pouvez créer un flux de données en exécutant une requête POST tout en fournissant les valeurs mentionnées précédemment dans la charge utile.

**Format API**

```https
POST /flows
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataflow between payments Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "2c48a152-3d49-43cb-88a1-523d49e3cbcb"
        ],
        "targetConnectionIds": [
            "c8e12917-ac33-44d7-a129-17ac3364d7b7"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "b54a8dc38e8d4e31a2dc096e413ae8e5",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

**Réponse**

Une réponse réussie renvoie l’ID `id` du flux de données nouvellement créé.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur source pour collecter les données d’une application de paiement sur une base planifiée. Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que les  de clients en temps réel et l’espace de travail des sciences de données. Pour plus d’informations, reportez-vous au  suivant :

* [Présentation du profil client en temps réel](../../../../profile/home.md)
* [Présentation de l’espace de travail Data Science](../../../../data-science-workspace/home.md)
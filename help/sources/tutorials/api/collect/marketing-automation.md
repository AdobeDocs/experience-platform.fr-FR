---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Collecte de données d’automatisation marketing via des connecteurs source et des API
topic: overview
translation-type: tm+mt
source-git-commit: 2f7961a4ca0bc0fec2ed1f50f5101e4dd734a282

---


# Collecte de données d’automatisation marketing via des connecteurs source et des API

Ce didacticiel décrit les étapes à suivre pour récupérer les données d’un système d’automatisation marketing et les intégrer à la plate-forme par le biais des connecteurs source et des API.

## Prise en main

Ce didacticiel nécessite que vous disposiez d’informations sur le fichier que vous souhaitez importer dans Platform, y compris le chemin et la structure du fichier. Si vous ne disposez pas de ces informations, reportez-vous au didacticiel sur l’ [exploration d’une application d’automatisation marketing à l’aide de l’API](../../api/create/marketing-automation/hubspot.md) de service de flux avant d’essayer ce didacticiel.

Ce didacticiel vous demande également de bien comprendre les composants suivants d’Adobe Experience Platform :

* [Système](../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Guide](../../../../xdm/api/getting-started.md)du développeur du Registre des  : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels vers l’API de Registre . Cela inclut votre `{TENANT_ID}`, le concept de &quot;&quot; et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
* [Service](../../../../catalog/home.md)de catalogue : Le catalogue est le système d’enregistrement de l’emplacement et de la lignée des données dans la plateforme d’expérience.
* [Importation](../../../../ingestion/batch-ingestion/overview.md)par lot : L’API d’assimilation par lot vous permet d’assimiler des données dans la plateforme d’expérience sous forme de fichiers de commandes.
* [Sandbox](../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à un système d’automatisation marketing à l’aide de l’API de service de flux.

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

Une fois un XDM ad hoc créé, vous pouvez désormais créer une connexion source à l’aide d’une requête POST sur l’API du service de flux. Une connexion source se compose d’une connexion de base, d’un fichier de données source et d’une référence au qui décrit les données source.

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
        "name": "Marketing automation source connection",
        "baseConnectionId": "2fce94c1-9a93-4971-8e94-c19a93097129",
        "description": "Marketing automation source connection",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/80a6e931bd5e00190b72daafb4e1e4f7913a114808be9ac0",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Hubspot.Contacts"
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | ID de connexion de votre application d’automatisation marketing |
| `data.schema.id` | Le  `$id` du XDM ad hoc. |
| `params.path` | Chemin d’accès du fichier source. |
| `connectionSpec.id` | ID de spécification de connexion de votre application d’automatisation marketing. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source nouvellement créée. Stockez cette valeur comme elle est requise dans les étapes suivantes pour créer une connexion .

```json
{
    "id": "c315c0ae-a339-44c4-95c0-aea33964c420",
    "etag": "\"67010af9-0000-0200-0000-5e9795c40000\""
}
```

## Création d’un  XDM {#target}

Dans les étapes précédentes, un XDM ad hoc a été créé pour structurer les données source. Pour que les données source soient utilisées dans Platform, un de  doit également être créé pour structurer les données source en fonction de vos besoins. Le  est ensuite utilisé pour créer un jeu de données de plateforme dans lequel les données source sont contenues.

Un XDM  peut être créé en exécutant une requête POST sur l’API [de registre de l’](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Si vous préférez utiliser l’interface utilisateur dans la plateforme d’expérience, le didacticiel [de l’éditeur de ](../../../../xdm/tutorials/create-schema-ui.md) fournit des instructions étape par étape pour exécuter des actions similaires dans l’éditeur de  de.

**Format API**

```https
POST /schemaregistry/tenant/schemas
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
        "title": "Target schema for marketing automation",
        "description": "Target schema for marketing automation",
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

Une réponse réussie renvoie les détails de la nouvelle  de, y compris son identifiant unique (`$id`). Stockez cet ID comme requis dans les étapes suivantes pour créer un jeu de données, un mappage et un flux de données  de.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
    "meta:altId": "_{TENANT_ID}.schemas.63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for marketing automation",
    "type": "object",
    "description": "Target schema for marketing automation",
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
        "repo:createdDate": 1586992941717,
        "repo:lastModifiedDate": 1586992941717,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CREATED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{CREATED_USER_ID}",
        "eTag": "d11e63a422b84a843cdd58d0ba8a16ce0a2068eda49ab380c1605ddd10efdf23",
        "meta:globalLibVersion": "1.9.2"
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
POST /catalog/dataSets
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
        "name": "Target dataset for marketing automation",
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
    "@/dataSets/5e9797ac6d771118ad8356db"
]
```

## Création d’une connexion de base de jeux de données

Afin de créer une connexion  et d&#39;assimiler des données externes dans la plateforme, une connexion de base de jeux de données doit d&#39;abord être acquise.

Pour créer une connexion de base de jeux de données, suivez les étapes décrites dans le didacticiel [sur la connexion de base de jeux de](../create-dataset-base-connection.md)données.

Continuez à suivre les étapes décrites dans le guide du développeur jusqu’à ce que vous ayez créé une connexion de base de jeux de données. Obtenez et stockez l’identifiant unique (`$id`) de la connexion de base, puis passez à l’étape suivante de ce didacticiel.

## Création d’une connexion 

Vous disposez maintenant des identifiants uniques pour une connexion de base de jeux de données, un  et un jeu de données de  dedonnées. A l’aide de ces identifiants, vous pouvez créer une connexion  à l’aide de l’API du service de flux afin de spécifier le jeu de données qui contiendra les données source entrantes.

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
        "baseConnectionId": "44b1c1e43-a5ee-4d86-9c1e-43a5eebd8601",
        "name": "Target Connection for marketing automation",
        "description": "Target Connection for marketing automation",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e9797ac6d771118ad8356db
        },
            "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | ID de votre connexion de base de jeux de données. |
| `data.schema.id` | Le `$id` du XDM . |
| `params.dataSetId` | ID du jeu de données . |
| `connectionSpec.id` | ID de spécification de connexion pour votre automatisation marketing. |

>[!IMPORTANT] Lors de la création d&#39;une connexion , veillez à utiliser la valeur de connexion de base du jeu de données pour la connexion de base `id` plutôt que l&#39;ID de connexion de votre connecteur source tiers.

```json
{
    "id": "fd82157f-0eea-4c81-8215-7f0eeaec8139",
    "etag": "\"5301d5ac-0000-0200-0000-5e97981a0000\""
}
```

## Création d’un mappage {#mapping}

Pour que les données source soient assimilées dans un jeu de données  de, elles doivent d’abord être mappées sur le auquel le jeu de données de l’analyse adhère. Pour ce faire, il effectue une requête POST vers l’API du service de conversion avec des mappages de données définis dans la charge utile de la requête.

**Format API**

```https
POST /conversion/mappingSets
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
        "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "Properties_Firstname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "Properties_Lastname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "repositoryCreatedBy",
                "sourceAttribute": "Added_At",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Portal_Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propriété | Description |
| --- | --- |
| `xdmSchema` | ID du  XDM . |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Stockez cette valeur, car elle est requise ultérieurement pour créer un flux de données.

```json
{
    "id": "280a3cc950894945bf815c5fc60f3803",
    "version": 0,
    "createdDate": 1586993661034,
    "modifiedDate": 1586993661034,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Spécifications de flux de données de recherche {#specs}

Un flux de données est responsable de la collecte de données à partir de sources et de leur transmission dans la plateforme. Pour créer un flux de données, vous devez d’abord obtenir les spécifications de flux de données responsables de la collecte des données d’automatisation du marketing.

**Format API**

```https
GET /flowSpecs?property=name=="CRMToAEP"
```

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la spécification de flux de données responsable de l’importation des données de votre système d’automatisation marketing dans Platform. Stocker la valeur du `id` champ comme elle est requise à l’étape suivante pour créer un nouveau flux de données.

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

La dernière étape de la collecte des données d’automatisation du marketing consiste à créer un flux de données. Les valeurs requises suivantes sont désormais préparées :

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
        "name": "Dataflow for marketing automation",
        "description": "Dataflow for marketing automation",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "c315c0ae-a339-44c4-95c0-aea33964c420"
        ],
        "targetConnectionIds": [
            "fd82157f-0eea-4c81-8215-7f0eeaec8139"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "280a3cc950894945bf815c5fc60f3803",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "<START TIME>",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `flowSpec.id` | ID de spécification du flux de données. |
| `sourceConnectionIds` | ID de connexion source. |
| `targetConnectionIds` | ID de connexion . |
| `transformations.params.mappingId` | ID de mappage. |

**Réponse**

Une réponse réussie renvoie l’ID (`id`) du flux de données nouvellement créé.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur source pour collecter les données d’un système d’automatisation marketing sur une base planifiée. Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que les  de clients en temps réel et l’espace de travail des sciences de données. Pour plus d’informations, reportez-vous au  suivant :

* [Présentation du profil client en temps réel](../../../../profile/home.md)
* [Présentation de l’espace de travail Data Science](../../../../data-science-workspace/home.md)
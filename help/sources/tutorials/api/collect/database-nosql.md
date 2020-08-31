---
keywords: Experience Platform;home;popular topics; flow service; database; sql; no sql; data warehouse
solution: Experience Platform
title: Collecte de données à partir d’une base de données tierce via des connecteurs et des API source
topic: overview
description: Ce didacticiel décrit les étapes à suivre pour récupérer des données d’une base de données tierce et les importer dans la plate-forme par le biais des connecteurs source et de l’API du service de flux.
translation-type: tm+mt
source-git-commit: 6578fd607d6f897a403d0af65c81dafe3dc12578
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 12%

---


# Collecte de données à partir d’une base de données tierce via des connecteurs et des API source

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel décrit les étapes à suivre pour récupérer des données d’une base de données tierce et les intégrer dans [!DNL Platform] des connecteurs source et dans l’ [[ !DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API.

## Prise en main

Ce didacticiel nécessite une connexion valide à une base de données tierce, ainsi que des informations sur le fichier que vous souhaitez importer [!DNL Platform] (y compris le chemin et la structure du fichier). Si vous ne disposez pas de ces informations, consultez le didacticiel sur l’ [exploration d’une base de données à l’aide de l’API](../explore/database-nosql.md) Flow Service avant de tenter ce didacticiel.

Ce didacticiel nécessite également une bonne compréhension des composants suivants de Adobe Experience Platform :

* [[ ! Système de modèle de données d’expérience (XDM) DNL]](../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Guide](../../../../xdm/api/getting-started.md)du développeur du registre des schémas : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels à l&#39;API de registre du Schéma. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
* [[ !Service de catalogue DNL]](../../../../catalog/home.md): Le catalogue est le système d’enregistrement pour l’emplacement et le lignage des données à l’intérieur [!DNL Experience Platform].
* [[ ! Apport du lot DNL]](../../../../ingestion/batch-ingestion/overview.md): L&#39;API d&#39;importation par lot vous permet d&#39;assimiler des données dans [!DNL Experience Platform] des fichiers de commandes.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à une base de données tierce à l’aide de l’ [[ !DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion source {#source}

You can create a source connection by making a POST request to the [!DNL Flow Service] API. Une connexion source se compose d’un identifiant de connexion, d’un chemin d’accès au fichier de données source et d’un identifiant de spécification de connexion.

Pour créer une connexion source, vous devez également définir une valeur d’énumération pour l’attribut de format de données.

Utilisez les valeurs d’énumération suivantes pour les connecteurs **basés sur des** fichiers :

| Data.format | Valeur maximale |
| ----------- | ---------- |
| Fichiers délimités | `delimited` |
| Fichiers JSON | `json` |
| Fichiers de parquet | `parquet` |

Pour tous les connecteurs **basés sur des** tables, utilisez la valeur enum : `tabular`.

**Format d’API**

```http
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
        "name": "Database Source Connector",
        "baseConnectionId": "d5cbb5bc-44cc-41a2-8bb5-bc44ccf1a2fb",
        "description": "A test source connector for a third-party database",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "ADMIN.E2E"
        },
        "connectionSpec": {
            "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | ID de connexion de la source de base de données tierce. |
| `params.path` | Chemin d’accès du fichier source. |
| `connectionSpec.id` | ID de spécification de connexion de la source de base de données tierce. Consultez l’ [annexe](#appendix) pour une liste d’ID de spécification de base de données. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est requis lors des étapes suivantes pour créer une connexion à une cible.

```json
{
    "id": "2f7356d9-a866-47ea-b356-d9a86687ea7a",
    "etag": "\"c8006055-0000-0200-0000-5ecd79520000\""
}
```

## Création d’un schéma XDM cible {#target-schema}

Dans les étapes précédentes, un schéma XDM ad hoc a été créé pour structurer les données source. Pour que les données source soient utilisées dans [!DNL Platform], un schéma de cible doit également être créé pour structurer les données source en fonction de vos besoins. Le schéma de cible est ensuite utilisé pour créer un [!DNL Platform] jeu de données dans lequel les données source sont contenues. Ce schéma XDM de cible étend également la [!DNL XDM Individual Profile] classe.

Un schéma XDM de cible peut être créé en exécutant une requête de POST sur l&#39;API [de registre du](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schéma. If you would prefer to use the user interface in [!DNL Experience Platform], the [Schema Editor tutorial](../../../../xdm/tutorials/create-schema-ui.md) provides step-by-step instructions for performing similar actions in the Schema Editor.

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

L&#39;exemple de demande suivant crée un schéma XDM qui étend la [!DNL Individual Profile] classe XDM.

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
        "title": "Database Source Connector Target Schema",
        "description": "Target schema for a third-party database",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
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

A successful response returns details of the newly created schema including its unique identifier (`$id`). Cet identifiant est requis dans les étapes suivantes pour créer un jeu de données de cible, un mappage et un flux de données.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
    "meta:altId": "_{TENANT_ID}.schemas.c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for an Oracle connector 5/26/20",
    "type": "object",
    "description": "Target schema for Database",
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
        "repo:createdDate": 1590523478581,
        "repo:lastModifiedDate": 1590523478581,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "34fdf36fc3029999a07270c4e7719d8a627f7e93e2fbc13888b3c11fb08983c0",
        "meta:globalLibVersion": "1.10.2.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’un jeu de données cible

Un jeu de données de cible peut être créé en exécutant une requête de POST sur l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog Service, en fournissant l’identifiant du schéma de cible dans la charge utile.

**Format d’API**

```http
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
        "name": "Target dataset for a third-party database source connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `schemaRef.id` | ID du schéma XDM de cible. |

**Réponse**

A successful response returns an array containing the ID of the newly created dataset in the format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API. Stockez l’ID du jeu de données de cible tel qu’il est requis dans les étapes suivantes pour créer une connexion à une cible et un flux de données.

```json
[
    "@/dataSets/5ecd766e4bab17191b78e892"
]
```

## Création d’une connexion à une cible {#target-connection}

Vous disposez maintenant des identifiants uniques pour une connexion de base de jeux de données, un schéma de cible et un jeu de données de cible. A l’aide de ces identifiants, vous pouvez créer une connexion de cible à l’aide de l’API [[ !DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

```http
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
        "name": "Target Connection for a third-party database source connector",
        "description": "Target Connection for a third-party database source connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ecd766e4bab17191b78e892"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `data.schema.id` | Le schéma `$id` XDM de la cible. |
| `params.dataSetId` | ID du jeu de données de cible rassemblé à l’étape précédente. |
| `connectionSpec.id` | ID de spécification de connexion fixe pour le lac de données. Cet identifiant de spécification de connexion est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la nouvelle connexion à la cible. Cette valeur est requise à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "e66fdb22-06df-48ac-afdb-2206dff8ac10",
    "etag": "\"7e03773a-0000-0200-0000-5ecd768d0000\""
}
```

## Création d’un mappage {#mapping}

Pour que les données source soient assimilées à un jeu de données de cible, elles doivent d’abord être mises en correspondance avec le schéma de cible auquel adhère le jeu de données de cible. Pour ce faire, il effectue une requête de POST à l’ [!DNL Conversion Service] API avec des mappages de données définis dans la charge utile de la requête.

**Format d’API**

```http
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "NAME",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "DOB",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "ID",
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
| `xdmSchema` | Le schéma `$id` XDM de la cible. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau mappage, y compris son identifiant unique (`id`). Cet identifiant est nécessaire à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "d9d94124417d4df48ea3d00e28eb4327",
    "version": 0,
    "createdDate": 1590523552440,
    "modifiedDate": 1590523552440,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Récupérer les spécifications de flux de données {#specs}

Un flux de données est responsable de la collecte de données provenant de sources et de leur intégration dans [!DNL Platform]les sources. Pour créer un flux de données, vous devez d’abord obtenir les spécifications du flux de données en exécutant une demande de GET à l’ [[ !DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API. Les spécifications de flux de données sont responsables de la collecte de données à partir d&#39;une base de données externe ou d&#39;un système NoSQL.

**Format d’API**

```http
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

Une réponse réussie renvoie les détails de la spécification de flux de données qui est responsable de l&#39;introduction des données de votre base de données ou système NoSQL dans [!DNL Platform]. Cet identifiant est requis à l’étape suivante pour créer un nouveau flux de données.

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

La dernière étape de la collecte des données consiste à créer un flux de données. A ce stade, les valeurs requises suivantes doivent être préparées :

* [ID de connexion source](#source)
* [ID de connexion à la cible](#target)
* [ID de mappage](#mapping)
* [ID de spécification du flux de données](#specs)

Un flux de données est responsable de la planification et de la collecte des données d’une source. Vous pouvez créer un flux de données en exécutant une requête de POST tout en fournissant les valeurs mentionnées précédemment dans la charge utile.

Pour planifier une assimilation, vous devez d&#39;abord définir la valeur du temps de début en secondes. Ensuite, vous devez définir la valeur de fréquence sur l’une des cinq options suivantes : `once`, `minute`, `hour`, `day`ou `week`. La valeur d&#39;intervalle désigne la période entre deux ingérations consécutives et la création d&#39;une assimilation ponctuelle ne nécessite pas la définition d&#39;un intervalle. Pour toutes les autres fréquences, la valeur de l’intervalle doit être égale ou supérieure à `15`.

**Format d’API**

```http
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
        "name": "Dataflow for a third-party database and Platform,
        "description": "collecting ADMIN.E2E",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "89cf81c9-47b4-463a-8f81-c947b4863afb"
        ],
        "targetConnectionIds": [
            "e66fdb22-06df-48ac-afdb-2206dff8ac10"
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
                    "mappingId": "d9d94124417d4df48ea3d00e28eb4327",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1590523836",
            "frequency":"minute",
            "interval":"15",
            "backfill": "true"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `flowSpec.id` | Identifiant [de spécification de](#specs) flux récupéré à l’étape précédente. |
| `sourceConnectionIds` | ID [de connexion](#source) source récupéré lors d’une étape précédente. |
| `targetConnectionIds` | ID [de connexion à la](#target-connection) cible récupéré lors d’une étape précédente. |
| `transformations.params.mappingId` | ID [de](#mapping) mappage récupéré lors d’une étape précédente. |
| `transformations.params.deltaColum` | Colonne désignée utilisée pour différencier les données nouvelles et existantes. Les données incrémentielles seront ingérées en fonction de l’horodatage de la colonne sélectionnée. Le format de date pris en charge pour `deltaColumn` est `yyyy-MM-dd HH:mm:ss`. Si vous utilisez Azure Table Enregistrement, le format pris en charge pour `deltaColumn` est `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | ID de mappage associé à votre base de données. |
| `scheduleParams.startTime` | Heure de début du flux de données dans l’époque. |
| `scheduleParams.frequency` | Fréquence à laquelle le flux de données va collecter les données. Les valeurs acceptables sont les suivantes : `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un entier non nul. L&#39;intervalle n&#39;est pas requis lorsque la fréquence est définie comme `once` et doit être supérieure ou égale à `15` pour d&#39;autres valeurs de fréquence. |

**Réponse**

A successful response returns the ID (`id`) of the newly created dataflow.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données qui y sont ingérées afin d’afficher des informations sur les exécutions de flux, l’état d’achèvement et les erreurs. Pour plus d&#39;informations sur la surveillance des flux de données, consultez le didacticiel sur la [surveillance des flux de données dans l&#39;API. ](../monitor.md)


## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur source pour collecter les données d’une base de données tierce sur une base planifiée. Les données entrantes peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

* [Présentation du profil client en temps réel](../../../../profile/home.md)
* [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)

## Annexe

La section suivante liste les différents connecteurs source d’enregistrement de cloud et leurs spécifications de connexion.

### Spécification de connexion

| Nom du connecteur | Identifiant de la spécification de connexion |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive] on [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark] on [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL CouchBase] | `1fe283f6-9bec-11ea-bb37-0242ac130002` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL Phoenix] | `102706fb-a5cd-42ee-afe0-bc42f017ff43` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |
---
keywords: Experience Platform;home;popular topics;Collect protocol data;protocol data
solution: Experience Platform
title: Collecte de données de protocole par le biais des connecteurs et des API source
topic: overview
type: Tutorial
description: Ce didacticiel décrit les étapes à suivre pour récupérer les données d'une application de protocoles et les intégrer à la plate-forme par le biais des connecteurs et des API source.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 12%

---


# Collecte de données de protocole par le biais des connecteurs et des API source

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel décrit les étapes à suivre pour récupérer des données d’une application de protocole tierce et les intégrer dans [!DNL Platform] des connecteurs source et dans l’ [[ !DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API.

## Prise en main

Ce didacticiel vous demande d&#39;avoir accès à un système de protocole par le biais d&#39;une connexion de base valide et d&#39;informations sur le fichier que vous souhaitez importer [!DNL Platform], y compris le chemin et la structure de la table. Si vous ne disposez pas de ces informations, consultez le didacticiel sur l’ [exploration des systèmes de protocole à l’aide de l’API](../explore/protocols.md) Flow Service avant de tester ce didacticiel.

* [[ ! Système de modèle de données d’expérience (XDM) DNL]](../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Guide](../../../../xdm/api/getting-started.md)du développeur du registre des schémas : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels à l&#39;API de registre du Schéma. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
* [[ !Service de catalogue DNL]](../../../../catalog/home.md): Le catalogue est le système d’enregistrement pour l’emplacement et le lignage des données à l’intérieur [!DNL Experience Platform].
* [[ ! Apport du lot DNL]](../../../../ingestion/batch-ingestion/overview.md): L&#39;API d&#39;importation par lot vous permet d&#39;assimiler des données dans [!DNL Experience Platform] des fichiers de commandes.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to a protocols application using the [!DNL Flow Service] API.

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

Utilisez les valeurs d’énumération suivantes pour les connecteurs basés sur des fichiers :

| Data.format | Valeur maximale |
| ----------- | ---------- |
| Fichiers délimités | `delimited` |
| Fichiers JSON | `json` |
| Fichiers de parquet | `parquet` |

Pour tous les connecteurs basés sur une table, utilisez la valeur enum : `tabular`.

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
        "name": "Protocols source connection",
        "baseConnectionId": "a5c6b647-e784-4b58-86b6-47e784ab580b",
        "description": "Protocols source connection to ingest Orders",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "Orders"
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | ID de connexion de votre application de protocoles |
| `params.path` | Chemin d’accès du fichier source. |
| `connectionSpec.id` | ID de spécification de connexion de votre application de protocoles. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est requis lors des étapes suivantes pour créer une connexion à une cible.

```json
{
    "id": "0a768941-ddfb-499d-b689-41ddfbf99db0",
    "etag": "\"8f00753e-0000-0200-0000-5e8a547d0000\""
}
```

## Création d’un schéma XDM cible {#target-schema}

Dans les étapes précédentes, un schéma XDM ad hoc a été créé pour structurer les données source. Pour que les données source soient utilisées dans [!DNL Platform], un schéma de cible doit également être créé pour structurer les données source en fonction de vos besoins. Le schéma de cible est ensuite utilisé pour créer un [!DNL Platform] jeu de données dans lequel les données source sont contenues. Ce schéma XDM de cible étend également la [!DNL Individual Profile] classe XDM.

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
        "title": "Target schema for protocols",
        "description": "Target schema for protocols",
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

A successful response returns details of the newly created schema including its unique identifier (`$id`). Cet identifiant est requis dans les étapes suivantes pour créer un jeu de données de cible, un mappage et un flux de données.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:altId": "_{TENANT_ID}.schemas.e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Protocols target schema",
    "type": "object",
    "description": "Protocols target schema",
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
    "imsOrg": "7DC732555AECDB4C0A494036@AdobeOrg",
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
        "repo:createdDate": 1586124086523,
        "repo:lastModifiedDate": 1586124086523,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "8b281c23af03ff6a8b7d8061c62d73f7bcbfa1fc7dbabebfb4d8ca77130576ca"
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
        "name": "Protocols target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `schemaRef.id` | Le schéma `$id` XDM de la cible. |

**Réponse**

A successful response returns an array containing the ID of the newly created dataset in the format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API. Stockez l’ID du jeu de données de cible tel qu’il est requis dans les étapes suivantes pour créer une connexion à une cible et un flux de données.

```json
[
    "@/dataSets/5e8a55ca53662c18af37a83a"
]
```

## Création d’une connexion à une cible {#target-connection}

Une connexion de cible représente la connexion à la destination où se trouvent les données saisies. Pour créer une connexion de cible, vous devez fournir l’identifiant de spécification de connexion fixe associé au lac de données. Cet identifiant de spécification de connexion est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma de cible d’un jeu de données de cible et de l’ID de spécification de connexion au lac de données. A l’aide de ces identifiants, vous pouvez créer une connexion de cible à l’aide de l’ [!DNL Flow Service] API pour spécifier le jeu de données qui contiendra les données source entrantes.

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
        "name": "Target Connection for protocols",
        "description": "Target Connection for protocols",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            }
        },
        "params": {
            "dataSetId": "5e8a55ca53662c18af37a83a"
        },
            "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `data.schema.id` | Le schéma `$id` XDM de la cible. |
| `params.dataSetId` | ID du jeu de données de cible. |
| `connectionSpec.id` | ID de spécification de connexion fixe au lac de données. Cet ID est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la nouvelle connexion à la cible. Cette valeur est requise à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "576d5ecf-f114-4587-ad5e-cff1144587f4",
    "etag": "\"13013506-0000-0200-0000-5e8a56d80000\""
}
```

## Création d’un mappage {#mapping}

Pour que les données source soient assimilées à un jeu de données de cible, elles doivent d’abord être mises en correspondance avec le schéma de cible auquel adhère le jeu de données de cible. Pour ce faire, il effectue une requête de POST à l’API [du service de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) conversion avec des mappages de données définis dans la charge utile de la requête.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "OrderID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "CustomerID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "EmployeeID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "createdByBatchID",
                "sourceAttribute": "OrderDate",
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
    "id": "37409d3017e24a3eb4a2dc21020f7a5b",
    "version": 0,
    "createdDate": 1586124873209,
    "modifiedDate": 1586124873209,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Rechercher les spécifications des flux de données {#specs}

Un flux de données est responsable de la collecte de données provenant de sources et de leur intégration dans [!DNL Platform]les sources. Pour créer un flux de données, vous devez d’abord obtenir les spécifications du flux de données en exécutant une demande de GET à l’ [!DNL Flow Service] API. Les spécifications de flux de données sont responsables de la collecte de données à partir d&#39;une application de protocoles externes.

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

Une réponse réussie renvoie les détails de la spécification de flux de données responsable de l&#39;introduction des données de votre application de protocoles dans [!DNL Platform]. Cet identifiant est requis à l’étape suivante pour créer un nouveau flux de données.

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
        "name": "Creating a dataflow for a protocols source",
        "description": "Creating a dataflow for a protocols source",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "0a768941-ddfb-499d-b689-41ddfbf99db0"
        ],
        "targetConnectionIds": [
            "576d5ecf-f114-4587-ad5e-cff1144587f4"
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
                    "mappingId": "7409d3017e24a3eb4a2dc21020f7a5b",
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

| Propriété | Description |
| -------- | ----------- |
| `flowSpec.id` | Identifiant [de spécification de](#specs) flux récupéré à l’étape précédente. |
| `sourceConnectionIds` | ID [de connexion](#source) source récupéré lors d’une étape précédente. |
| `targetConnectionIds` | ID [de connexion à la](#target-connection) cible récupéré lors d’une étape précédente. |
| `transformations.params.mappingId` | ID [de](#mapping) mappage récupéré lors d’une étape précédente. |
| `transformations.params.deltaColum` | Colonne désignée utilisée pour différencier les données nouvelles et existantes. Les données incrémentielles seront ingérées en fonction de l’horodatage de la colonne sélectionnée. Le format pris en charge pour `deltaColumn` l’utilisation de Generic OData est `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | ID de mappage associé à votre base de données. |
| `scheduleParams.startTime` | Heure de début du flux de données dans l’époque. |
| `scheduleParams.frequency` | Fréquence à laquelle le flux de données va collecter les données. Les valeurs acceptables sont les suivantes : `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un entier non nul. L&#39;intervalle n&#39;est pas requis lorsque la fréquence est définie comme `once` et doit être supérieure ou égale à `15` pour d&#39;autres valeurs de fréquence. |

**Réponse**

A successful response returns the ID `id` of the newly created dataflow.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données qui y sont ingérées afin d’afficher des informations sur les exécutions de flux, l’état d’achèvement et les erreurs. Pour plus d&#39;informations sur la surveillance des flux de données, consultez le didacticiel sur la [surveillance des flux de données dans l&#39;API. ](../monitor.md)


## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur source pour collecter des données d’une application de protocoles sur une base planifiée. Les données entrantes peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

* [Présentation du profil client en temps réel](../../../../profile/home.md)
* [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)
---
keywords: Experience Platform;home;popular topics; flow service; payment; paypal
solution: Experience Platform
title: Collecte de données de paiement via les connecteurs et les API source
topic: overview
description: Ce didacticiel décrit les étapes à suivre pour récupérer les données d’une application de paiement tierce et les intégrer à la plate-forme par le biais des connecteurs source et de l’API de service de flux.
translation-type: tm+mt
source-git-commit: 6578fd607d6f897a403d0af65c81dafe3dc12578
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 12%

---


# Collecte de données de paiement via les connecteurs et les API source

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel décrit les étapes à suivre pour récupérer des données d’un système de paiement tiers et les intégrer dans [!DNL Platform] des connecteurs source et dans l’ [[ !DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API.

## Prise en main

Ce didacticiel vous demande d&#39;avoir accès à un système de paiement par le biais d&#39;une connexion valide, ainsi que des informations sur le fichier que vous souhaitez importer [!DNL Platform] (y compris le chemin et la structure du fichier). Si vous ne disposez pas de ces informations, consultez le didacticiel sur l’ [exploration d’une application de paiement à l’aide de l’API](../explore/payments.md) de service de flux avant de tenter ce didacticiel.

Ce didacticiel nécessite également une bonne compréhension des composants suivants de Adobe Experience Platform :

* [[ ! Système de modèle de données d’expérience (XDM) DNL]](../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Guide](../../../../xdm/api/getting-started.md)du développeur du registre des schémas : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels à l&#39;API de registre du Schéma. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
* [[ !Service de catalogue DNL]](../../../../catalog/home.md): Le catalogue est le système d’enregistrement pour l’emplacement et le lignage des données à l’intérieur [!DNL Experience Platform].
* [[ ! Apport du lot DNL]](../../../../ingestion/batch-ingestion/overview.md): L&#39;API d&#39;importation par lot vous permet d&#39;assimiler des données dans [!DNL Experience Platform] des fichiers de commandes.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to a payments application using the [!DNL Flow Service] API.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Création d’une classe et d’un schéma XDM ad hoc

Pour importer des données externes dans [!DNL Platform] les connecteurs source, une classe XDM ad hoc et un schéma doivent être créés pour les données source brutes.

Pour créer une classe et un schéma ad hoc, suivez les étapes décrites dans le didacticiel [schéma](../../../../xdm/tutorials/ad-hoc.md)ad hoc. Lors de la création d’une classe ad hoc, tous les champs trouvés dans les données source doivent être décrits dans le corps de la requête.

Continuez à suivre les étapes décrites dans le guide du développeur jusqu’à ce que vous ayez créé un schéma ad hoc. Récupérez et stockez l’identifiant unique (`$id`) du schéma ad hoc, puis passez à l’étape suivante de ce didacticiel.

## Création d’une connexion source {#source}

Avec un schéma XDM ad hoc créé, une connexion source peut désormais être créée à l’aide d’une requête de POST envoyée à l’ [!DNL Flow Service] API. Une connexion source se compose d’un ID de connexion, d’un fichier de données source et d’une référence au schéma qui décrit les données source.

Pour créer une connexion source, vous devez également définir une valeur d’énumération pour l’attribut de format de données.

Utilisez les valeurs d’énumération suivantes pour les connecteurs **basés sur des** fichiers :

| Data.format | Valeur maximale |
| ----------- | ---------- |
| Fichiers délimités | `delimited` |
| Fichiers JSON | `json` |
| Fichiers de parquet | `parquet` |

Pour tous les connecteurs **basés sur des** tables, utilisez la valeur enum : `tabular`.

**Format d’API**

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
            "format": "tabular",
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
| `baseConnectionId` | ID de connexion unique de l’application de paiement tierce à laquelle vous accédez. |
| `data.schema.id` | Le schéma `$id` XDM ad hoc. |
| `params.path` | Chemin d’accès du fichier source. |
| `connectionSpec.id` | ID de spécification de connexion de votre application de paiement. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est requis lors des étapes suivantes pour créer une connexion à une cible.

```json
{
    "id": "2c48a152-3d49-43cb-88a1-523d49e3cbcb",
    "etag": "\"8000c843-0000-0200-0000-5e8917ea0000\""
}
```

## Création d’un schéma XDM cible {#target-schema}

Dans les étapes précédentes, un schéma XDM ad hoc a été créé pour structurer les données source. Pour que les données source soient utilisées dans [!DNL Platform], un schéma de cible doit également être créé pour structurer les données source en fonction de vos besoins. Le schéma de cible est ensuite utilisé pour créer un [!DNL Platform] jeu de données dans lequel les données source sont contenues. Ce schéma XDM de cible étend également la [!DNL Individual Profile] classe XDM.

Un schéma XDM de cible peut être créé en exécutant une requête de POST sur l&#39;API [de registre du](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schéma. If you would prefer to use the user interface in [!DNL Experience Platform], the [Schema Editor tutorial](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/tutorials/create-schema-ui.html) provides step-by-step instructions for performing similar actions in the Schema Editor.

**Format d’API**

```https
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

A successful response returns details of the newly created schema including its unique identifier (`$id`). Cet identifiant est requis dans les étapes suivantes pour créer un jeu de données de cible, un mappage et un flux de données.

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

## Création d’un jeu de données cible

Un jeu de données de cible peut être créé en exécutant une requête de POST sur l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog Service, en fournissant l’identifiant du schéma de cible dans la charge utile.

**Format d’API**

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
| `schemaRef.id` | Le schéma `$id` XDM de la cible. |

**Réponse**

A successful response returns an array containing the ID of the newly created dataset in the format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API. Stockez l’ID du jeu de données de cible tel qu’il est requis dans les étapes suivantes pour créer une connexion à une cible et un flux de données.

```json
[
    "@/dataSets/5e8918669cbbee18ad9771f3"
]
```

## Création d’une connexion à une cible {#target-connection}

Une connexion de cible représente la connexion à la destination où se trouvent les données saisies. Pour créer une connexion de cible, vous devez fournir l’identifiant de spécification de connexion fixe associé au lac de données. Cet identifiant de spécification de connexion est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma de cible d’un jeu de données de cible et de l’ID de spécification de connexion au lac de données. A l’aide de ces identifiants, vous pouvez créer une connexion de cible à l’aide de l’ [!DNL Flow Service] API pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

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
        "name": "Target Connection for payments",
        "description": "Target Connection for payments",
        "data": {
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
| `data.schema.id` | Le schéma `$id` XDM de la cible. |
| `params.dataSetId` | ID du jeu de données de cible. |
| `connectionSpec.id` | ID de spécification de connexion fixe au lac de données. Cet ID est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la nouvelle connexion à la cible. Cette valeur est requise à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "c8e12917-ac33-44d7-a129-17ac3364d7b7",
    "etag": "\"0f015874-0000-0200-0000-5e8918e60000\""
}
```

## Création d’un mappage {#mapping}

Pour que les données source soient assimilées à un jeu de données de cible, elles doivent d’abord être mises en correspondance avec le schéma de cible auquel adhère le jeu de données de cible. Pour ce faire, il effectue une requête de POST à l’API [du service de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) conversion avec des mappages de données définis dans la charge utile de la requête.

**Format d’API**

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
| `xdmSchema` | Le schéma `$id` XDM de la cible. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau mappage, y compris son identifiant unique (`id`). Cet identifiant est nécessaire à une étape ultérieure pour créer un flux de données.

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

## Rechercher les spécifications des flux de données {#specs}

Un flux de données est responsable de la collecte de données provenant de sources et de leur intégration dans [!DNL Platform]les sources. Pour créer un flux de données, vous devez d’abord obtenir les spécifications du flux de données en exécutant une demande de GET à l’ [!DNL Flow Service] API. Les spécifications de flux de données sont responsables de la collecte de données à partir d&#39;une base de données externe ou d&#39;un système NoSQL.

**Format d’API**

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

Une réponse positive renvoie les détails de la spécification de flux de données qui est responsable de l&#39;introduction des données de votre demande de paiement dans [!DNL Platform]. Cet identifiant est requis à l’étape suivante pour créer un nouveau flux de données.

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
            "frequency": "minute",
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
| `transformations.params.deltaColum` | Colonne désignée utilisée pour différencier les données nouvelles et existantes. Les données incrémentielles seront ingérées en fonction de l’horodatage de la colonne sélectionnée. Le format de date pris en charge pour `deltaColumn` est `yyyy-MM-dd HH:mm:ss`. |
| `transformations.params.mappingId` | ID de mappage associé à votre base de données. |
| `scheduleParams.startTime` | Heure de début du flux de données dans l’époque. |
| `scheduleParams.frequency` | Fréquence à laquelle le flux de données va collecter les données. Les valeurs acceptables sont les suivantes : `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un entier non nul. L&#39;intervalle n&#39;est pas requis lorsque la fréquence est définie comme `once` et doit être supérieure ou égale à `15` pour d&#39;autres valeurs de fréquence. |

**Réponse**

A successful response returns the ID `id` of the newly created dataflow.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données qui y sont ingérées afin d’afficher des informations sur les exécutions de flux, l’état d’achèvement et les erreurs. Pour plus d&#39;informations sur la surveillance des flux de données, consultez le didacticiel sur la [surveillance des flux de données dans l&#39;API. ](../monitor.md)


## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur source pour collecter les données d&#39;une application de paiement sur une base planifiée. Les données entrantes peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

* [Présentation du profil client en temps réel](../../../../profile/home.md)
* [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)
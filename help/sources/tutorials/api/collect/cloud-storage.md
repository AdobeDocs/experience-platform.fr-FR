---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Collecte de données d’enregistrement Cloud via les connecteurs et les API source
topic: overview
translation-type: tm+mt
source-git-commit: 2a8e8f2deffca06782f0ad9b8154ee763c05f06d
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 2%

---


# Collecte de données d’enregistrement Cloud via les connecteurs et les API source

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates au sein de Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel décrit les étapes à suivre pour récupérer les données d’un enregistrement cloud tiers et les amener à la plate-forme par le biais des connecteurs et API source.

## Prise en main

Ce didacticiel nécessite que vous ayez accès à un enregistrement cloud tiers via une connexion valide et des informations sur le fichier que vous souhaitez importer dans Platform, y compris le chemin et la structure du fichier. Si vous ne disposez pas de ces informations, consultez le didacticiel sur l’ [exploration d’un enregistrement cloud tiers à l’aide de l’API](../explore/cloud-storage.md) Flow Service avant de tenter ce didacticiel.

Ce didacticiel nécessite également une bonne compréhension des composants suivants de Adobe Experience Platform :

- [Système](../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Guide](../../../../xdm/api/getting-started.md)du développeur du registre des Schémas : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels à l&#39;API de registre du Schéma. Cela inclut votre `{TENANT_ID}`nom, le concept de &quot;conteneurs&quot; et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accepter et à ses valeurs possibles).
- [Service](../../../../catalog/home.md)de catalogue : Le catalogue est le système d’enregistrement pour l’emplacement et le lignage des données dans la plate-forme d’expérience.
- [Importation](../../../../ingestion/batch-ingestion/overview.md)par lot : L’API d’importation par lot vous permet d’assimiler des données dans la plate-forme d’expérience sous forme de fichiers par lot.
- [Sandbox](../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à un enregistrement cloud à l’aide de l’API de service de flux.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

- Content-Type : `application/json`

## Création d’une classe et d’un schéma XDM ad hoc

Pour importer des données externes dans la plate-forme via des connecteurs source, une classe XDM ad hoc et un schéma doivent être créés pour les données source brutes.

Pour créer une classe et un schéma ad hoc, suivez les étapes décrites dans le didacticiel [schéma](../../../../xdm/tutorials/ad-hoc.md)ad hoc. Lors de la création d’une classe ad hoc, tous les champs trouvés dans les données source doivent être décrits dans le corps de la requête.

Continuez à suivre les étapes décrites dans le guide du développeur jusqu’à ce que vous ayez créé un schéma ad hoc. L’identifiant unique (`$id`) du schéma ad hoc est nécessaire pour passer à l’étape suivante de ce didacticiel.

## Création d’une connexion source {#source}

Avec un schéma XDM ad hoc créé, une connexion source peut désormais être créée à l’aide d’une requête POST envoyée à l’API du service de flux. Une connexion source se compose d’un ID de connexion, d’un fichier de données source et d’une référence au schéma qui décrit les données source.

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
        "name": "Test source connection for a Cloud Storage connector",
        "baseConnectionId": "ac33bd66-1565-4915-b3bd-6615657915c4",
        "description": "Test source connection for a Cloud Storage connector",
        "data": {
            "format": "delimited",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/22a4ab59462a64de551d42dd10ec1f19d8d7246e3f90072a",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/backfil/data8.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `baseConnectionId` | ID de connexion unique du système d’enregistrement cloud tiers auquel vous accédez. |
| `data.schema.id` | ID du schéma XDM ad hoc. |
| `params.path` | Chemin d’accès au fichier source auquel vous accédez. |
| `connectionSpec.id` | Identifiant de spécification de connexion associé à votre système d’enregistrement Cloud tiers spécifique. Consultez l’ [annexe](#appendix) pour une liste d’ID de spécification de connexion. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est nécessaire à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "8bae595c-8548-4716-ae59-5c85480716e9",
    "etag": "\"4a00038b-0000-0200-0000-5ebc47fd0000\""
}
```

## Création d’un schéma XDM cible {#target}

Dans les étapes précédentes, un schéma XDM ad hoc a été créé pour structurer les données source. Pour que les données source soient utilisées dans Platform, un schéma de cible doit également être créé pour structurer les données source en fonction de vos besoins. Le schéma de cible est ensuite utilisé pour créer un jeu de données de plateforme dans lequel les données source sont contenues.

Un schéma XDM de cible peut être créé en exécutant une requête POST sur l&#39;API [de registre du](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schéma.

Si vous préférez utiliser l’interface utilisateur dans la plate-forme d’expérience, le didacticiel [Editeur de](../../../../xdm/tutorials/create-schema-ui.md) Schéma fournit des instructions détaillées pour exécuter des actions similaires dans l’éditeur de Schéma.

**Format d’API**

```http
POST /schemaregistry/tenant/schemas
```

**Requête**

L&#39;exemple de demande suivant crée un schéma XDM qui étend la classe de Profil XDM Individuel.

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
        "title": "Target schema for a Cloud Storage connector",
        "description": "Target schema for a Cloud Storage connector",
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

Une réponse réussie renvoie les détails du schéma nouvellement créé, y compris son identifiant unique (`$id`). Cet identifiant est requis dans les étapes suivantes pour créer un jeu de données de cible, un mappage et un flux de données.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:altId": "_{TENANT_ID}.schemas.e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Cloud Storage connector",
    "type": "object",
    "description": "Target schema for Cloud Storage",
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
        "repo:createdDate": 1589398474190,
        "repo:lastModifiedDate": 1589398474190,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "f07723475e933dc30ed411d97986a36f13aa20c820463dd8cf7b74e63f4e7801",
        "meta:globalLibVersion": "1.10.1.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’un jeu de données de cible

Un jeu de données de cible peut être créé en exécutant une requête POST sur l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog Service, en fournissant l’ID du schéma de cible dans la charge utile.

**Format d’API**

```http
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
        "name": "Target dataset for a Cloud Storage connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `schemaRef.id` | ID du schéma XDM de cible. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;ID du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’ID de jeu de données est une chaîne générée par le système en lecture seule qui est utilisée pour référencer le jeu de données dans les appels d’API. L’ID du jeu de données de cible est requis dans les étapes suivantes pour créer une connexion à une cible et un flux de données.

```json
[
    "@/dataSets/5ebc4be8590b1b191a8dc4ca"
]
```

## Création d’une connexion à une cible

Une connexion de cible représente la connexion à la destination où se trouvent les données saisies. Pour créer une connexion de cible, vous devez fournir l’identifiant de spécification de connexion fixe associé au lac de données. Cet identifiant de spécification de connexion est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma de cible d’un jeu de données de cible et de l’identifiant de spécification de connexion au lac de données. A l’aide de ces identifiants, vous pouvez créer une connexion de cible à l’aide de l’API du service de flux pour spécifier le jeu de données qui contiendra les données source entrantes.

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ebc4be8590b1b191a8dc4ca"
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
| `params.dataSetId` | ID du jeu de données de cible. |
| `connectionSpec.id` | ID de spécification de connexion fixe au lac de données. Cet ID est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la nouvelle connexion à la cible. Cet identifiant est requis par la suite.

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## Création d’un mappage {#mapping}

Pour que les données source soient assimilées à un jeu de données de cible, elles doivent d’abord être mises en correspondance avec le schéma de cible auquel adhère le jeu de données de cible. Pour ce faire, il effectue une demande POST au service de conversion avec des mappages de données définis dans la charge utile de la demande.

**Format d’API**

```http
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "first_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "last_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "email",
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
| `xdmSchema` | ID du schéma XDM de cible. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau mappage, y compris son identifiant unique (`id`). Cette valeur est requise à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "febec6a6785e45ea9ed594422cc483d7",
    "version": 0,
    "createdDate": 1589398562232,
    "modifiedDate": 1589398562232,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Récupérer les spécifications de flux de données {#specs}

Un flux de données est chargé de collecter les données provenant de sources et de les intégrer à la plate-forme. Pour créer un flux de données, vous devez d’abord obtenir les spécifications de flux de données qui sont responsables de la collecte des données d’enregistrement de cloud.

**Format d’API**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la spécification de flux de données responsable de l’importation des données de votre enregistrement de cloud dans Platform. La réponse comprend un identifiant de spécification de flux unique. Cet identifiant est requis à l’étape suivante pour créer un nouveau flux de données.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "transformationSpecs": [
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
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Création d’un flux de données

La dernière étape de la collecte des données d’enregistrement de cloud consiste à créer un flux de données. A l’heure actuelle, les valeurs requises suivantes sont préparées :

- [ID de connexion source](#source)
- [ID de connexion à la Cible](#target)
- [ID de mappage](#mapping)
- [ID de spécification du flux de données](#specs)

Un flux de données est responsable de la planification et de la collecte des données d’une source. Vous pouvez créer un flux de données en exécutant une requête POST tout en fournissant les valeurs mentionnées précédemment dans la charge utile.

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
        "name": "Cloud Storage flow to AEP",
        "description": "Cloud Storage flow to AEP",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "8bae595c-8548-4716-ae59-5c85480716e9"
        ],
        "targetConnectionIds": [
            "1f5af99c-f1ef-4076-9af9-9cf1ef507678"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "febec6a6785e45ea9ed594422cc483d7",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1589398646",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `flowSpec.id` | ID de spécification de flux récupéré à l’étape précédente. |
| `sourceConnectionIds` | ID de connexion source récupéré lors d’une étape précédente. |
| `targetConnectionIds` | ID de connexion à la cible récupéré lors d’une étape précédente. |
| `transformations.params.mappingId` | ID de mappage récupéré lors d’une étape précédente. |
| `scheduleParams.startTime` | Heure début du flux de données en secondes. |
| `scheduleParams.frequency` | Les valeurs de fréquence sélectionnables sont les suivantes : `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un entier non nul. L&#39;intervalle n&#39;est pas requis lorsque la fréquence est définie comme `once` et doit être supérieure ou égale à `15` pour d&#39;autres valeurs de fréquence. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant (`id`) du flux de données nouvellement créé.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur source pour collecter les données de votre enregistrement cloud sur une base planifiée. Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que le Profil client en temps réel et l’espace de travail Data Science. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)

## Annexe {#appendix}

La section suivante liste les différents connecteurs source d’enregistrement de cloud et leurs spécifications de connexion.

### Spécification de connexion

| Nom du connecteur | Spécification de connexion |
| -------------- | --------------- |
| Amazon S3 (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| Amazon Kinesis (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| Blob Azure (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| Enregistrement Azure Data Lake Gen2 (ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| Hubs de Événement Azure (Événements Hubs) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| Enregistrement de fichier Azure | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| Enregistrement Google Cloud | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| HDFS | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
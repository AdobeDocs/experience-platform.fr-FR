---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Collecte de données d’enregistrement Cloud via les connecteurs et les API source
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 2%

---


# Collecte de données d’enregistrement Cloud via les connecteurs et les API source

Ce didacticiel décrit les étapes à suivre pour récupérer les données d’un enregistrement cloud tiers et les amener sur la plate-forme par le biais des connecteurs et API source.

## Prise en main

Ce didacticiel vous demande d&#39;avoir accès à un enregistrement cloud tiers par le biais d&#39;une connexion de base valide et d&#39;informations sur le fichier que vous souhaitez importer dans Platform, y compris le chemin et la structure du fichier. Si vous ne disposez pas de ces informations, consultez le didacticiel sur l’ [exploration d’un enregistrement cloud tiers à l’aide de l’API](../explore/cloud-storage.md) Flow Service avant de tenter ce didacticiel.

Ce didacticiel nécessite également une bonne compréhension des composants suivants d’Adobe Experience Platform :

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

Continuez à suivre les étapes décrites dans le guide du développeur jusqu’à ce que vous ayez créé un schéma ad hoc. Récupérez et stockez l’identifiant unique (`$id`) du schéma ad hoc, puis passez à l’étape suivante de ce didacticiel.

## Création d’une connexion source {#source}

Avec un schéma XDM ad hoc créé, une connexion source peut désormais être créée à l’aide d’une requête POST envoyée à l’API du service de flux. Une connexion source se compose d’une connexion de base, d’un fichier de données source et d’une référence au schéma qui décrit les données source.

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection for a cloud storage",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "description": "Source Connection to ingest data.csv",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/140c03de81b959db95879033945cfd4c",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/some/path/data.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
    }'
```

| Propriété | Description |
| --- | --- |
| `baseConnectionId` | ID d’une connexion de base pour un système d’enregistrement cloud. |
| `data.schema.id` | ID du schéma XDM ad hoc. |
| `params.path` | Chemin d’accès du fichier source. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion source nouvellement créée. Stocker cette valeur comme elle est requise dans les étapes suivantes pour créer une connexion à une cible.

```json
{
    "id": "9a603322-19d2-4de9-89c6-c98bd54eb184"
}
```

## Création d’un schéma XDM cible {#target}

Dans les étapes précédentes, un schéma XDM ad hoc a été créé pour structurer les données source. Pour que les données source soient utilisées dans Platform, un schéma de cible doit également être créé pour structurer les données source en fonction de vos besoins. Le schéma de cible est ensuite utilisé pour créer un jeu de données de plateforme dans lequel les données source sont contenues.

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
        "title": "Target schema for cloud storage source connector",
        "description": "",
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

Une réponse réussie renvoie les détails du schéma nouvellement créé, y compris son identifiant unique (`$id`). Enregistrez cet ID comme requis dans les étapes suivantes pour créer un jeu de données de cible, un mappage et un flux de données.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
    "meta:altId": "{TENANT_ID}.schemas.417a33eg81a221bd10495920574gfa2d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for cloud storage source connector",
    "description": "",
    "type": "object",
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
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "meta:containerId": "tenant",
    "meta:registryMetadata": {
        "eTag": "6m/FrIlXYU2+yH6idbcmQhKSlMo="
    }
}
```

## Création d’un jeu de données de cible

Un jeu de données de cible peut être créé en exécutant une requête POST sur l’API du service de catalogue, en fournissant l’ID du schéma de cible dans la charge utile.

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
        "name": "Target Dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `schemaRef.id` | ID du schéma XDM de cible. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;ID du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’ID de jeu de données est une chaîne générée par le système en lecture seule qui est utilisée pour référencer le jeu de données dans les appels d’API. Stockez l’ID du jeu de données de cible tel qu’il est requis dans les étapes suivantes pour créer une connexion à une cible et un flux de données.

```json
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Créer une connexion de base de jeux de données

Pour importer des données externes dans la plate-forme, une connexion de base de données de jeu de plateformes d’expérience doit d’abord être acquise.

Pour créer une connexion de base de jeux de données, suivez les étapes décrites dans le didacticiel [de connexion de base de](../create-dataset-base-connection.md)jeux de données.

Continuez à suivre les étapes décrites dans le guide du développeur jusqu’à ce que vous ayez créé une connexion de base de jeux de données. Récupérez et stockez l’identifiant unique (`$id`), puis utilisez-le comme identifiant de connexion de base à l’étape suivante pour créer une connexion de cible.

## Création d’une connexion à une cible

Vous disposez maintenant des identifiants uniques pour une connexion de base de jeux de données, un schéma de cible et un jeu de données de cible. A l’aide de ces identifiants, vous pouvez créer une connexion de cible à l’aide de l’API du service de flux pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

```http
POST /targetConnections
```

**Requête**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection",
        "description": "Target Connection for cloud storage data",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5c8c3c555033b814b69f947f"
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | ID de la connexion de base de votre jeu de données. |
| `data.schema.id` | Le schéma `$id` XDM de la cible. |
| `params.dataSetId` | ID du jeu de données de cible. |
| `connectionSpec.id` | ID de spécification de connexion de votre enregistrement cloud. |

>[!NOTE] Lors de la création d’une connexion de cible, veillez à utiliser la valeur de connexion de base de Data Lake pour la connexion de base `id` plutôt que la connexion de base de votre connecteur de source tiers.

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la nouvelle connexion à la cible. Stocker cette valeur comme elle est requise dans les étapes ultérieures.

```json
{
    "id": "4ee890c7-519c-4291-bd20-d64186b62da8",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Phone",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "Email",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
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

Une réponse réussie renvoie les détails du nouveau mappage, y compris son identifiant unique (`id`). Stocker cette valeur comme elle est requise à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
    "version": 1,
    "createdDate": 1568047685000,
    "modifiedDate": 1568047703000,
    "inputSchemaRef": {
        "id": null,
        "contentType": null
    },
    "outputSchemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "contentType": "1.0"
    },
    "mappings": [
        {
            "id": "7bbea5c0f0ef498aa20aa2e2e5c22290",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "Id",
            "destination": "_id",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "Id",
            "destinationXdmPath": "_id"
        },
        {
            "id": "def7fd7db2244f618d072e8315f59c05",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "FirstName",
            "destination": "person.name.firstName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "FirstName",
            "destinationXdmPath": "person.name.firstName"
        },
        {
            "id": "e974986b28c74ed8837570f421d0b2f4",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "LastName",
            "destination": "person.name.lastName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "LastName",
            "destinationXdmPath": "person.name.lastName"
        }
    ],
    "status": "PUBLISHED",
    "xdmVersion": "1.0",
    "schemaRef": {
        "id": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/2574494fdb01fa14c25b52d717ccb828"
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

Une réponse réussie renvoie les détails de la spécification de flux de données responsable de l’importation des données de votre enregistrement cloud dans la plate-forme. Stocker la valeur du `id` champ comme elle est requise à l’étape suivante pour créer un nouveau flux de données.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
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
        "name": "Dataflow between cloud storage and Platform",
        "description": "collecting data.csv",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "9a603322-19d2-4de9-89c6-c98bd54eb184"
        ],
        "targetConnectionIds": [
            "4ee890c7-519c-4291-bd20-d64186b62da8"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "mode": "append"
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea"
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
| --- | --- |
| `flowSpec.id` | ID de spécification du flux de données |
| `sourceConnectionIds` | ID de connexion source |
| `targetConnectionIds` | ID de connexion à la Cible |
| `transformations.params.mappingId` | ID de mappage |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant (`id`) du flux de données nouvellement créé.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé un connecteur source pour collecter les données de votre enregistrement cloud sur une base planifiée. Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que le Profil client en temps réel et l’espace de travail Data Science. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)

## Annexe

La section suivante liste les différents connecteurs source d’enregistrement de cloud et leurs spécifications de connexion.

### Spécification de connexion

| Nom du connecteur | Spécification de connexion |
| -------------- | --------------- |
| Amazon S3 (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| Amazon Kinesis (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| Blob Azure (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| Enregistrement Azure Data Lake Gen2 (ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| Hubs de Événement Azure (EventHub) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| Enregistrement Google Cloud | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
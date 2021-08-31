---
keywords: Experience Platform;accueil;rubriques les plus consultées;base de données;base de données tierce
solution: Experience Platform
title: Collecte de données à partir d’une base de données à l’aide de connecteurs source et d’API
topic-legacy: overview
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour récupérer des données d’une base de données et les ingérer dans Platform à l’aide des connecteurs source et des API.
exl-id: 1e1f9bbe-eb5e-40fb-a03c-52df957cb683
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 20%

---

# Collecte de données à partir d’une base de données à l’aide des connecteurs source et des API

Ce tutoriel décrit les étapes à suivre pour récupérer des données d’une base de données tierce et les ingérer dans Platform via les connecteurs source et l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce tutoriel nécessite que vous disposiez d’une connexion valide à une base de données, ainsi que d’informations sur le fichier que vous souhaitez importer dans Platform (y compris le chemin et la structure du fichier). Si vous ne disposez pas de ces informations, consultez le tutoriel sur l’[exploration d’une base de données à l’aide de l’API Flow Service](../explore/database-nosql.md) avant de lancer ce tutoriel.

Ce tutoriel nécessite également une compréhension pratique des composants suivants de Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Guide](../../../../xdm/api/getting-started.md) de développement du registre des schémas : Inclut des informations importantes à connaître pour effectuer avec succès des appels vers l’API Schema Registry. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Le de catalogue constitue le système d’enregistrement de l’emplacement et de la liaison des données dans Experience Platform.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): L’API Batch Ingestion vous permet d’ingérer des données dans Experience Platform sous forme de fichiers de lots.
* [Environnements de test](../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à une base de données tierce à l’aide de l’API [!DNL Flow Service].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources d’Experience Platform, y compris celles appartenant à [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion source {#source}

Vous pouvez créer une connexion source en adressant une requête de POST à l’API [!DNL Flow Service]. Une connexion source se compose d’un identifiant de connexion, d’un chemin d’accès au fichier de données source et d’un identifiant de spécification de connexion.

Pour créer une connexion source, vous devez également définir une valeur d&#39;énumération pour l&#39;attribut data format.

Utilisez les valeurs d’énumération suivantes pour les connecteurs basés sur un fichier :

| Sur le format des données saisies | Valeur d’énumération |
| ----------- | ---------- |
| Délimité | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Pour tous les connecteurs basés sur un tableau, définissez la valeur sur `tabular`.

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
        "name": "Database source connection",
        "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
        "description": "Database source connection",
        "data": {
            "format": "tabular"
        },
        "params": {
            "tableName": "test1.Mytable",
            "columns": [
                {
                    "name": "TestID",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "Name",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "Datefield",
                    "type": "string",
                    "meta:xdmType": "date-time",
                    "xdm": {
                        "type": "string",
                        "format": "date-time"
                    }
                }
            ]
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `baseConnectionId` | Identifiant de connexion de la source de votre base de données. |
| `params.path` | Chemin d’accès du fichier source. |
| `connectionSpec.id` | L’identifiant de spécification de connexion de la source de votre base de données. Voir l’ [Annexe](#appendix) pour obtenir la liste des ID de spécification de base de données. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est requis lors des étapes suivantes pour créer une connexion cible.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Création d’un schéma XDM cible {#target-schema}

Pour que les données source soient utilisées dans Platform, un schéma XDM cible doit être créé pour structurer les données source en fonction de vos besoins. Le schéma XDM cible est ensuite utilisé pour créer un jeu de données Platform dans lequel les données source sont contenues. Ce schéma XDM cible étend également la classe [!DNL XDM Individual Profile] .

Vous pouvez créer un schéma XDM cible en adressant une requête de POST à l’[API Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

L’exemple de requête suivant crée un schéma XDM qui étend la classe XDM [!DNL Individual Profile].

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
        "title": "Database target XDM schema",
        "description": "Database target XDM schema",
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

Une réponse réussie renvoie les détails du schéma nouvellement créé, y compris son identifiant unique (`$id`). Cet identifiant est requis lors des étapes suivantes pour créer un jeu de données cible, un mappage et un flux de données.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
    "meta:altId": "_{TENANT_ID}.schemas.52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Database target XDM schema",
    "type": "object",
    "description": "Database target XDM schema",
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
        "repo:createdDate": 1612308675206,
        "repo:lastModifiedDate": 1612308675206,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIEDD_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "7c5c09e62421e6b172c925f059ac524a99f348dd837b5f13abd77ee91aa6bb61",
        "meta:globalLibVersion": "1.18.4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’un jeu de données cible

Un jeu de données cible peut être créé en adressant une requête de POST à l’[API Catalog Service](https://www.adobe.io/experience-platform-apis/references/catalog/), en fournissant l’identifiant du schéma cible dans la payload.

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
        "name": "Database target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `schemaRef.id` | L’identifiant du schéma XDM cible. |
| `schemaRef.contentType` | Version du schéma. Cette valeur doit être définie sur `application/vnd.adobe.xed-full-notext+json;version=1`, ce qui renvoie la dernière version mineure du schéma. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l’identifiant du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API. Stockez l’identifiant du jeu de données cible, car il est nécessaire lors des étapes suivantes pour créer une connexion cible et un flux de données.

```json
[
    "@/dataSets/6019e0e7c5dcf718db5ebc71"
]
```

## Créer une connexion cible {#target-connection}

Une connexion cible représente la connexion à la destination où se trouvent les données ingérées. Pour créer une connexion cible, vous devez indiquer l’identifiant de spécification de connexion fixe associé au lac de données. Cet identifiant de spécification de connexion est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma cible d’un jeu de données cible et de l’identifiant de spécification de connexion au lac de données. À l’aide de l’API [!DNL Flow Service], vous pouvez créer une connexion cible en spécifiant ces identifiants ainsi que le jeu de données qui contiendra les données source entrantes.

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
        "name": "Database target connection",
        "description": "Database target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "6019e0e7c5dcf718db5ebc71"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `data.schema.id` | `$id` du schéma XDM cible. |
| `data.schema.version` | Version du schéma. Cette valeur doit être définie sur `application/vnd.adobe.xed-full+json;version=1`, ce qui renvoie la dernière version mineure du schéma. |
| `params.dataSetId` | Identifiant du jeu de données cible rassemblé à l’étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion utilisé pour la connexion au lac de données. Cet identifiant est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique de la nouvelle connexion cible (`id`). Cette valeur est requise lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
    "etag": "\"c0038936-0000-0200-0000-6019e1190000\""
}
```

## Création d’un mappage {#mapping}

Pour que les données source soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible adhère. Pour ce faire, il vous suffit d’adresser une requête de POST à l’API [!DNL Conversion Service] avec des mappages de données définis dans le payload de la requête.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "TestID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.birthDate",
                "sourceAttribute": "Datefield",
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
| `xdmSchema` | `$id` du schéma XDM cible. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau mappage, y compris son identifiant unique (`id`). Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "0b090130b58b4819afc78b6dc98b484d",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Récupération des spécifications du flux de données {#specs}

Un flux de données est chargé de collecter des données à partir de sources et de les importer dans Platform. Pour créer un flux de données, vous devez d’abord obtenir les spécifications du flux de données en adressant une demande de GET à l’API [!DNL Flow Service]. Les spécifications de flux de données sont chargées de collecter les données d’une base de données externe ou d’un système NoSQL.

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

Une réponse réussie renvoie les détails de la spécification de flux de données responsable de l’importation des données de votre source dans Platform. La réponse inclut la spécification de flux unique `id` requise pour créer un nouveau flux de données.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "221c7626-58f6-4eec-8ee2-042b0226f03b",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "102706fb-a5cd-42ee-afe0-bc42f017ff43",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "optionSpec": {
                "name": "OptionSpec",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "errorDiagnosticsEnabled": {
                            "title": "Error diagnostics.",
                            "description": "Flag to enable detailed and sample error diagnostics summary.",
                            "type": "boolean",
                            "default": false
                        },
                        "partialIngestionPercent": {
                            "title": "Partial ingestion threshold.",
                            "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                            "type": "number",
                            "exclusiveMinimum": 0
                        }
                    }
                }
            },
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
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "once",
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "once"
                            }
                        }
                    },
                    "then": {
                        "allOf": [
                            {
                                "not": {
                                    "required": [
                                        "interval"
                                    ]
                                }
                            },
                            {
                                "not": {
                                    "required": [
                                        "backfill"
                                    ]
                                }
                            }
                        ]
                    },
                    "else": {
                        "required": [
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
            },
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
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

La dernière étape de la collecte de données consiste à créer un flux de données. A ce stade, les valeurs requises suivantes doivent être préparées :

* [ID de connexion source](#source)
* [Identifiant de connexion Target](#target)
* [ID de mappage](#mapping)
* [Identifiant de spécification du flux de données](#specs)

Un flux de données est chargé de planifier et de collecter les données d’une source. Vous pouvez créer un flux de données en exécutant une requête de POST tout en fournissant les valeurs mentionnées précédemment dans le payload de la requête.

Pour planifier une ingestion, vous devez d’abord définir la valeur de l’heure de début sur la durée en secondes. Vous devez ensuite définir la valeur de fréquence sur l’une des cinq options suivantes : `once`, `minute`, `hour`, `day` ou `week`. La valeur interval désigne la période entre deux ingestion consécutives et la création d’une ingestion unique ne nécessite pas de définition d’un intervalle. Pour toutes les autres fréquences, la valeur de l’intervalle doit être égale ou supérieure à `15`.

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
        "name": "Database dataflow using BigQuery",
        "description": "collecting test1.Mytable",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "b7581b59-c603-4df1-a689-d23d7ac440f3"
        ],
        "targetConnectionIds": [
            "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "Datefield",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1612310466",
            "frequency":"minute",
            "interval":"15",
            "backfill": "true"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `flowSpec.id` | L’ [identifiant de spécification de flux](#specs) récupéré à l’étape précédente. |
| `sourceConnectionIds` | [ID de connexion source](#source) récupéré à une étape précédente. |
| `targetConnectionIds` | [Identifiant de connexion cible](#target-connection) récupéré à une étape précédente. |
| `transformations.params.mappingId` | [ID de mappage](#mapping) récupéré à une étape précédente. |
| `transformations.params.deltaColum` | Colonne désignée utilisée pour différencier les données nouvelles des données existantes. Les données incrémentielles seront ingérées en fonction de l’horodatage de la colonne sélectionnée. Le format de date pris en charge pour `deltaColumn` est `yyyy-MM-dd HH:mm:ss`. Si vous utilisez Azure Table Storage, le format pris en charge pour `deltaColumn` est `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | Identifiant de mappage associé à votre base de données. |
| `scheduleParams.startTime` | Heure de début du flux de données dans l’époque. |
| `scheduleParams.frequency` | Fréquence à laquelle le flux de données collectera les données. Les valeurs possibles sont les suivantes : `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un entier non nul. L’intervalle n’est pas requis lorsque la fréquence est définie sur `once` et doit être supérieure ou égale à `15` pour les autres valeurs de fréquence. |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du nouveau flux de données créé.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Surveillance de votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les exécutions de flux, l’état d’achèvement et les erreurs. Pour plus d’informations sur la façon de surveiller les flux de données, consultez le tutoriel sur la [surveillance des flux de données dans l’API ](../monitor.md)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un connecteur source pour collecter des données d’une base de données selon un calendrier précis. Les données entrantes peuvent désormais être utilisées par les services Platform en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, consultez les documents suivants :

* [Présentation de Real-time Customer Profile](../../../../profile/home.md)
* [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)

## Annexe

La section suivante répertorie les différents connecteurs source de stockage dans le cloud et leurs spécifications de connexion.

### Spécification de connexion

| Nom du connecteur | Identifiant de spécification de connexion |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive] à [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark] à [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL Couchbase] | `1fe283f6-9bec-11ea-bb37-0242ac130002` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL Greenplum] | `37b6bf40-d318-4655-90be-5cd6f65d334b` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL Phoenix] | `102706fb-a5cd-42ee-afe0-bc42f017ff43` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |

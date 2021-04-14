---
keywords: Experience Platform ; accueil ; rubriques populaires ; données d’enregistrement en mode cloud ; données en flux continu ; flux continu
solution: Experience Platform
title: Collecte de données en flux continu à l’aide des connecteurs et des API source
topic: aperçu
type: Tutorial
description: Ce didacticiel décrit les étapes à suivre pour récupérer les données en flux continu et les amener sur la plate-forme à l’aide des connecteurs et des API source.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
translation-type: tm+mt
source-git-commit: a63208dcdbe6851262e567a89c00b160dffa0e41
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 22%

---

# Collecte de données en flux continu à l’aide des connecteurs et des API source

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel décrit les étapes à suivre pour récupérer les données d’un connecteur source de flux continu et les amener à [!DNL Experience Platform] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce didacticiel nécessite que vous disposiez d’un ID de connexion valide pour un connecteur de flux continu. Si vous ne disposez pas de ces informations, consultez les didacticiels suivants sur la création d’une connexion source de flux continu avant de tenter ce didacticiel :

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL HTTP API]](../create/streaming/http.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

Ce didacticiel nécessite également une bonne compréhension des composants suivants de Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Guide](../../../../xdm/api/getting-started.md) du développeur du registre des schémas : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels à l&#39;API de registre du Schéma. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Le catalogue est le système d’enregistrement pour l’emplacement et le lignage des données à l’intérieur  [!DNL Experience Platform].
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): L’assimilation en flux continu pour  [!DNL Platform] permet aux utilisateurs d’envoyer en temps réel des données depuis les périphériques client et serveur  [!DNL Experience Platform] en temps réel.
- [Sandbox](../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour collecter avec succès des données de flux continu à l’aide de l’API [!DNL Flow Service].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

- `Content-Type: application/json`

## Créer une connexion source {#source}

Vous pouvez créer une connexion source en adressant une requête de POST à l&#39;API [!DNL Flow Service]. Une connexion source se compose d’un identifiant de connexion, d’un chemin d’accès au fichier de données source et d’un identifiant de spécification de connexion.

Pour créer une connexion source, vous devez également définir une valeur d’énumération pour l’attribut de format de données.

Utilisez les valeurs d’énumération suivantes pour les connecteurs basés sur des fichiers :

| Sur le format des données saisies | Valeur maximale |
| ----------- | ---------- |
| Délimité | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Pour tous les connecteurs basés sur une table, définissez la valeur sur `tabular`.

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
        "name": "Test source connector for streaming data",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "connectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
        "description": "Test source connector for streaming data",
        "data": {
            "format": "delimited"
        },
            "connectionSpec": {
            "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `providerId` | ID de fournisseur de votre connecteur de diffusion en continu. |
| `connectionId` | ID de connexion unique de votre connecteur de diffusion en continu. |
| `connectionSpec.id` | Identifiant de spécification de connexion associé à votre connecteur de diffusion en continu spécifique. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est nécessaire à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Obtenir l’URL du point de terminaison de diffusion {#get-endpoint}

Une fois la connexion source créée, vous pouvez désormais récupérer votre URL de point de terminaison de diffusion en continu.

**Format d’API**

```http
GET /flowservice/sourceConnections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de la sourceConnections que vous avez créée précédemment. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/sourceConnections/e96d6135-4b50-446e-922c-6dd66672b6b2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la connexion demandée. L’URL du point de terminaison de diffusion en continu est automatiquement créée avec la connexion et peut être récupérée à l’aide de la valeur `inletUrl`.

```json
{
    "items": [
        {
            "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
            "createdAt": 1617743929826,
            "updatedAt": 1617743930363,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG}",
            "name": "Test source connector for streaming data",
            "description": "Test source connector for streaming data",
            "baseConnectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
            "state": "enabled",
            "data": {
                "format": "delimited",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "params": {
                "sourceId": "Streaming raw data",
                "inletUrl": "https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b",
                "inletId": "2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b",
                "dataType": "raw",
                "name": "hgtest"
            },
            "version": "\"d6006bc1-0000-0200-0000-606cd03a0000\"",
            "etag": "\"d6006bc1-0000-0200-0000-606cd03a0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
                    "connectionSpec": {
                        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                        "version": "1.0"
                    }
                }
            }
        }
    ]
}
```


## Créer un schéma XDM de cible {#target-schema}

Pour que les données source soient utilisées dans [!DNL Platform], un schéma de cible doit être créé pour structurer les données source en fonction de vos besoins. Le schéma de cible est ensuite utilisé pour créer un jeu de données [!DNL Platform] contenant les données source. Ce schéma XDM de cible étend également la classe XDM [!DNL Individual Profile].

Un schéma XDM de cible peut être créé en exécutant une requête de POST à l&#39;[API de registre de Schéma](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

L&#39;exemple de demande suivant crée un schéma XDM qui étend la classe XDM [!DNL Individual Profile].

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
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
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

Une réponse réussie renvoie les détails du schéma nouvellement créé, y compris son identifiant unique (`$id`). Cet identifiant est requis dans les étapes suivantes pour créer un jeu de données de cible, un mappage et un flux de données.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
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
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’un jeu de données cible

Un jeu de données de cible peut être créé en exécutant une requête de POST à l&#39;[API du service de catalogue](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), en fournissant l&#39;identifiant du schéma de cible dans la charge utile.

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
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "fileDescription": {
            "format": "parquet"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        },
        "name": "Test streaming dataset"
    }'
```

| Propriété | Description |
| --- | --- |
| `schemaRef.id` | ID du schéma XDM de cible. |
| `schemaRef.contentType` | Version du schéma. Cette valeur doit être définie sur `application/vnd.adobe.xed-full-notext+json;version=1`, ce qui renvoie la dernière version mineure du schéma. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;ID du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API. L’ID du jeu de données de cible est requis dans les étapes suivantes pour créer une connexion à une cible et un flux de données.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Créer une connexion de cible {#target-connection}

Une connexion de cible représente la connexion à la destination où se trouvent les données saisies. Pour créer une connexion de cible, vous devez fournir l’identifiant de spécification de connexion fixe associé au lac de données. Cet identifiant de spécification de connexion est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma de cible d’un jeu de données de cible et de l’identifiant de spécification de connexion au lac de données. A l’aide de ces identifiants, vous pouvez créer une connexion de cible à l’aide de l’API [!DNL Flow Service] pour spécifier le jeu de données qui contiendra les données source entrantes.

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
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm"
        },
        "params": {
        "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `params.dataSetId` | ID du jeu de données de cible. |
| `connectionSpec.id` | ID de spécification de connexion utilisé pour la connexion au lac Data. Cet ID est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique de la nouvelle connexion à la cible (`id`). Cet identifiant est requis par la suite.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Créer un mappage {#mapping}

Pour que les données source soient assimilées à un jeu de données de cible, elles doivent d’abord être mises en correspondance avec le schéma de cible auquel adhère le jeu de données de cible. Pour ce faire, il effectue une demande de POST au service de conversion avec des mappages de données définis dans la charge utile de la demande.

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
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `xdmSchema` | `$id` du schéma XDM de cible. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau mappage, y compris son identifiant unique (`id`). Cet identifiant est nécessaire à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Rechercher les spécifications de flux de données {#specs}

Un flux de données est chargé de collecter les données provenant de sources et de les intégrer à [!DNL Platform]. Pour créer un flux de données, vous devez d&#39;abord obtenir les spécifications du flux de données en exécutant une demande de GET à l&#39;API [!DNL Flow Service]. Les spécifications de flux de données sont responsables de la collecte de données à partir d&#39;un connecteur de flux continu.
**Format d’API**

```http
GET /flowSpecs?property=name=="Steam data with transformation"
```

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="Steam data with transformation"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la spécification de flux de données responsable de l&#39;importation des données de votre connecteur de diffusion en continu dans [!DNL Platform]. Cet identifiant est requis à l’étape suivante pour créer un nouveau flux de données.

```json
{
    "items": [
        {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "name": "Steam data with transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "d27d4907-7351-47dd-bbc2-05a04365703d",
                "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb"
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
                        "description": "defines various params required for different mapping from Raw to XDM",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        },
                        "required": [
                            "mappingId"
                        ]
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "deleteSupported": false,
                        "updateSupported": false,
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
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

La dernière étape de la collecte des données en flux continu consiste à créer un flux de données. A l’heure actuelle, les valeurs requises suivantes sont préparées :

- [ID de connexion source](#source)
- [ID de connexion à la cible](#target)
- [ID de mappage](#mapping)
- [ID de spécification du flux de données](#specs)

Un flux de données est responsable de la planification et de la collecte des données d’une source. Vous pouvez créer un flux de données en exécutant une requête de POST tout en fournissant les valeurs mentionnées précédemment dans la charge utile.

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
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| Propriété | Description |
| --- | --- |
| `flowSpec.id` | ID de la spécification de flux [](#specs) récupéré à l’étape précédente. |
| `sourceConnectionIds` | L&#39;[identifiant de connexion source](#source) a été récupéré lors d&#39;une étape précédente. |
| `targetConnectionIds` | L&#39;[ID de connexion de cible](#target-connection) a été récupéré lors d&#39;une étape précédente. |
| `transformations.params.mappingId` | ID de mappage [](#mapping) récupéré lors d’une étape précédente. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant (`id`) du flux de données nouvellement créé.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Affichage des données brutes à ingérer {#ingest-data}

Maintenant que vous avez créé votre flux, vous pouvez envoyer votre message JSON au point de terminaison de diffusion que vous avez créé précédemment.

**Format d’API**

```http
POST /collection/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | La valeur `id` de la connexion en continu que vous venez de créer. |

**Requête**

L’exemple de requête ingère des données brutes au point de terminaison de diffusion en continu qui a été créé précédemment.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male"
      "birthday": {
          "year": 1984
          "month": 6
          "day": 9
      }
  }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails des informations nouvellement saisies.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Propriété | Description |
| -------- | ----------- |
| `{CONNECTION_ID}` | L’identifiant de la connexion en continu précédemment créée. |
| `xactionId` | Un identifiant unique généré côté serveur pour l’enregistrement que vous venez d’envoyer. Cet identifiant aide Adobe à suivre le cycle de vie de cet enregistrement sur différents systèmes et en cas de débogage. |
| `receivedTimeMs` : un horodatage (en millisecondes) indiquant l’heure de réception de la requête. |

## Étapes suivantes

En suivant ce didacticiel, vous avez créé un flux de données pour collecter des données en flux continu à partir de votre connecteur de diffusion en continu. Les données entrantes peuvent désormais être utilisées par les services [!DNL Platform] en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)

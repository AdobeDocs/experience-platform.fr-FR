---
keywords: Experience Platform;accueil;rubriques les plus consultées;données de stockage dans le cloud;données en continu;diffusion en continu
solution: Experience Platform
title: Création d’un flux de données en flux continu pour les données brutes à l’aide de l’API Flow Service
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour récupérer des données en continu et les introduire dans Platform à l’aide des connecteurs source et des API.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 39b5a2b76c28033b9e98dcefc4cdcaa9964f4d2e
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 44%

---

# Création d’un flux de données en continu pour les données brutes à l’aide de l’API [!DNL Flow Service]

Ce tutoriel décrit les étapes à suivre pour récupérer les données brutes d’un connecteur de source de diffusion en continu et les apporter à l’Experience Platform à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.
   - [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Guide du développeur de Schema Registry](../../../../xdm/api/getting-started.md) : inclut des informations importantes à connaître avant dʼeffectuer des appels vers l’API Schema Registry. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
- [[!DNL Catalog Service]](../../../../catalog/home.md) : Catalogue constitue le système d’enregistrement de l’emplacement et de la liaison des données dans Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md) : l’ingestion par flux pour Platform fournit aux utilisateurs une méthode pour envoyer en temps réel des données de périphériques côté client et côté serveur vers Experience Platform.
- [Sandbox](../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer correctement des appels vers les API Platform, consultez le guide de [Prise en main des API Platform](../../../../landing/api-guide.md).

### Créer une connexion source {#source}

Ce tutoriel nécessite également que vous disposiez d’un identifiant de connexion source valide pour un connecteur de diffusion en continu. Si vous ne disposez pas de ces informations, consultez les tutoriels suivants sur la création d’une connexion source en continu avant de lancer ce tutoriel :

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Créer un schéma XDM cible {#target-schema}

Pour que les données sources soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Le schéma cible est ensuite utilisé pour créer un jeu de données Platform dans lequel les données source sont contenues. Ce schéma XDM cible étend également la classe XDM [!DNL Individual Profile].

Pour créer un schéma XDM cible, envoyez une requête de POST au point de terminaison `/schemas` de l’[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie les détails du schéma nouvellement créé, y compris son identifiant unique (`$id`). Cet identifiant est requis lors des étapes suivantes pour créer un jeu de données cible, un mappage et un flux de données.

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
    "imsOrg": "{ORG_ID}",
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

## Créer un jeu de données cible

Avec un schéma XDM cible créé et son `$id` unique, vous pouvez désormais créer un jeu de données cible contenant vos données source. Pour créer un jeu de données cible, envoyez une requête de POST au point de terminaison `dataSets` de l’ [ API Catalog Service](https://www.adobe.io/experience-platform-apis/references/catalog/), tout en fournissant l’identifiant du schéma cible dans la payload.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du jeu de données à créer. |
| `schemaRef.id` | L’URI `$id` du schéma XDM sur lequel le jeu de données sera basé. |
| `schemaRef.contentType` | La version du schéma. Cette valeur doit être définie sur `application/vnd.adobe.xed-full-notext+json;version=1`, ce qui renvoie la dernière version mineure du schéma. Pour plus d’informations, reportez-vous à la section [contrôle de version des schémas](../../../../xdm/api/getting-started.md#versioning) du guide de l’API XDM. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l’identifiant du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API. L’identifiant du jeu de données cible est requis lors des étapes suivantes pour créer une connexion cible et un flux de données.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Créer une connexion cible {#target-connection}

Les connexions Target créent et gèrent une connexion de destination à Platform ou à tout emplacement où les données transférées arriveront. Les connexions Target contiennent des informations concernant la destination des données, le format des données et l’identifiant de connexion cible requis pour créer un flux de données. Les instances de connexion à Target sont spécifiques à un client et à une organisation.

Pour créer une connexion cible, envoyez une requête de POST au point de terminaison `/targetConnections` de l’API [!DNL Flow Service]. Dans le cadre de la requête, vous devez fournir le format de données, le `dataSetId` récupéré à l’étape précédente et l’identifiant de spécification de connexion fixe lié à [!DNL Data Lake]. Cet identifiant est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `data.format` | Le format spécifié des données que vous apportez au lac de données. |
| `params.dataSetId` | Identifiant du jeu de données cible généré à l’étape précédente. **Remarque** : vous devez fournir un identifiant de jeu de données valide lors de la création d’une connexion cible. Un identifiant de jeu de données non valide entraînera une erreur. |
| `connectionSpec.id` | Identifiant de spécification de connexion utilisé pour se connecter au lac de données. Cet identifiant est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique de la nouvelle connexion cible (`id`). Cet identifiant est requis aux étapes suivantes.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Créer un mappage {#mapping}

Pour que les données sources soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible se rattache.

Pour créer un jeu de mappage, envoyez une requête POST au point dʼentrée `mappingSets` de lʼ[[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) et indiquez votre schéma XDM cible `$id` et les détails des jeux de mappages que vous souhaitez créer.

**Format d’API**

```http
POST /mappingSets
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `xdmSchema` | La valeur `$id` du schéma XDM cible. |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

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

## Récupération d’une liste de spécifications de flux de données {#specs}

Un flux de données est chargé de collecter des données à partir de sources et de les importer dans Platform. Pour créer un flux de données, vous devez d’abord obtenir les spécifications du flux de données en adressant une demande de GET à l’API [!DNL Flow Service].

**Format d’API**

```http
GET /flowSpecs
```

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de spécifications de flux de données. L’identifiant de spécification de flux de données que vous devez récupérer pour créer un flux de données à l’aide de [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] ou [!DNL Google PubSub], est `d69717ba-71b4-4313-b654-49f9cf126d7a`.

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
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
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
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
        },
    ]
}
```

## Créer un flux de données

La dernière étape de la collecte de données en continu consiste à créer un flux de données. Vous disposez à présent des valeurs requises suivantes :

- [ID de connexion source](#source)
- [ID de connexion cible](#target)
- [Identifiant de mappage](#mapping)
- [ID de spécification de flux de données](#specs)

Un flux de données est chargé de planifier et de collecter les données provenant d’une source. Vous pouvez créer un flux de données en exécutant une requête POST et en fournissant les valeurs mentionnées précédemment dans la payload.

**Format d’API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
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
| `flowSpec.id` | [Identifiant de spécification de flux](#specs) récupéré à l’étape précédente. |
| `sourceConnectionIds` | [Identifiant de connexion source](#source) récupéré lors d’une étape précédente. |
| `targetConnectionIds` | [Identifiant de connexion cible](#target-connection) récupéré lors d’une étape précédente. |
| `transformations.params.mappingId` | [Identifiant de mappage](#mapping) récupéré lors d’une étape précédente. |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du flux de données nouvellement créé.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Données Post pour l’ingestion

Consultez l’exemple de charge utile ci-dessous pour obtenir des exemples de code json brut ou compatible XDM que vous pouvez envoyer pour ingestion.

>[!NOTE]
>
>Vous devez ajouter un délai d’au moins ~5 minutes entre la création du flux de données et l’ingestion des données en continu. Cela permet au flux de données d’être entièrement activé avant toute ingestion de données.

Les exemples suivants s’appliquent à tous les :

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

>[!BEGINTABS]

>[!TAB Données brutes]

```json
'{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB Données XDM]

```json
{
  "header": {
    "schemaRef": {
      "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
      "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
      }
    },
    "xdmEntity": {
      "_id": "acme",
      "workEmail": {
        "address": "mike@acme.com",
        "primary": true,
        "type": "work",
        "status": "active"
      },
      "person": {
        "gender": "male",
        "name": {
          "firstName": "Mike",
          "lastName": "Wazowski"
        },
        "birthDate": "1985-01-01"
      },
      "identityMap": {
        "ecid": [
          {
            "id": "01262118050522051420082102000000000000"
          }
        ]
      }
    }
  }
}
```

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour collecter des données en continu à partir de votre connecteur de diffusion en continu. Ces données entrantes peuvent désormais être utilisées par les services de Platform en aval, comme [!DNL Real-Time Customer Profile] et [!DNL Data Science Workspace]. Consultez les documents suivants pour plus d’informations :

- [Vue d’ensemble du profil client en temps réel](../../../../profile/home.md)
- [Présentation de l’espace de travail de science des données](../../../../data-science-workspace/home.md)

---
keywords: Experience Platform;accueil;rubriques populaires;données de stockage cloud
solution: Experience Platform
title: Créer un flux de données pour les sources de stockage cloud à l’aide de l’API Flow Service
type: Tutorial
description: Ce tutoriel décrit la procédure à suivre pour récupérer des données à partir d’un stockage cloud tiers afin de les importer dans Platform à l’aide des connecteurs source et des API.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 48aef63cffbdc52a6a96ef69e5db4f54274144b6
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 69%

---

# Créer un flux de données pour les sources de stockage cloud à l’aide de l’API [!DNL Flow Service]

Ce tutoriel décrit la procédure à suivre pour récupérer des données à partir d’une source de stockage cloud afin de les importer dans Platform à l’aide de l’API [[!DNL Flow Service] ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Pour créer un flux de données, vous devez déjà disposer d’un identifiant de connexion de base valide avec une source de stockage dans le cloud. Si vous ne disposez pas de cet ID, consultez la [présentation des sources](../../../home.md#cloud-storage) pour obtenir la liste des sources de stockage dans le cloud avec lesquelles vous pouvez créer une connexion de base.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.
   - [Principes de base de la composition des schémas](../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Guide du développeur de Schema Registry](../../../../xdm/api/getting-started.md) : inclut des informations importantes à connaître avant dʼeffectuer des appels vers l’API Schema Registry. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
- [[!DNL Catalog Service]](../../../../catalog/home.md) : Catalogue constitue le système d’enregistrement de l’emplacement et de la liaison des données dans Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md) : l’API Batch Ingestion vous permet d’ingérer des données dans Experience Platform sous forme de fichiers séquentiels.
- [Sandbox](../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer correctement des appels vers les API Platform, consultez le guide de [Prise en main des API Platform](../../../../landing/api-guide.md).

## Créer une connexion source {#source}

Vous pouvez créer une connexion source en envoyant une requête de POST au point de terminaison `sourceConnections` de l’API [!DNL Flow Service] tout en fournissant votre identifiant de connexion de base, le chemin d’accès au fichier source à ingérer et l’identifiant de spécification de connexion correspondant de votre source.

Lors de la création d&#39;une connexion source, vous devez également définir une valeur d&#39;énumération pour l&#39;attribut data format.

Utilisez les valeurs d’énumération suivantes pour les sources basées sur des fichiers :

| Format des données | Valeur d’énumération |
| ----------- | ---------- |
| Délimité | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Pour toutes les sources basées sur un tableau, définissez la valeur sur `tabular`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `baseConnectionId` | Identifiant de connexion de base de votre source de stockage dans le cloud. |
| `data.format` | Le format des données que vous souhaitez importer dans Platform. Les valeurs prises en charge sont : `delimited`, `JSON` et `parquet`. |
| `data.properties` | (Facultatif) Ensemble de propriétés que vous pouvez appliquer à vos données lors de la création d’une connexion source. |
| `data.properties.columnDelimiter` | (Facultatif) Un délimiteur de colonne à un seul caractère que vous pouvez spécifier lors de la collecte de fichiers plats. Toute valeur de caractère unique est un délimiteur de colonne autorisé. Si elle n’est pas fournie, une virgule (`,`) est utilisée comme valeur par défaut. **Remarque** : La propriété `columnDelimiter` ne peut être utilisée que lors de l’ingestion de fichiers délimités. |
| `data.properties.encoding` | (Facultatif) Une propriété qui définit le type de codage à utiliser lors de l’ingestion de vos données vers Platform. Les types de codage pris en charge sont : `UTF-8` et `ISO-8859-1`. **Remarque** : Le paramètre `encoding` n’est disponible que lors de l’ingestion de fichiers CSV délimités. D’autres types de fichiers seront ingérés avec l’encodage par défaut, `UTF-8`. |
| `data.properties.compressionType` | (Facultatif) Une propriété qui définit le type de fichier compressé pour l’ingestion. Les types de fichiers compressés pris en charge sont les suivants : `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` et `tar`. **Remarque** : La propriété `compressionType` ne peut être utilisée que lors de l’ingestion de fichiers délimités ou JSON. |
| `params.path` | Le chemin d’accès au fichier source auquel vous accédez. Ce paramètre pointe vers un fichier individuel ou un dossier entier.  **Remarque** : Vous pouvez utiliser un astérisque à la place du nom de fichier pour spécifier l’ingestion d’un dossier entier. Par exemple : `/acme/summerCampaign/*.csv` ingère l’intégralité du dossier `/acme/summerCampaign/`. |
| `params.type` | Type de fichier du fichier de données source que vous ingérez. Utilisez le type `file` pour ingérer un fichier individuel et le type `folder` pour ingérer un dossier entier. |
| `connectionSpec.id` | Identifiant de spécification de connexion associé à votre source de stockage dans le cloud spécifique. Consultez lʼ[annexe](#appendix) pour obtenir la liste des identifiants de spécification de connexion. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Utilisation d’expressions régulières pour sélectionner un ensemble spécifique de fichiers à ingérer {#regex}

Vous pouvez utiliser des expressions régulières pour ingérer un ensemble particulier de fichiers de votre source vers Platform lors de la création d’une connexion source.

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

Dans l’exemple ci-dessous, l’expression régulière est utilisée dans le chemin d’accès au fichier pour spécifier l’ingestion de tous les fichiers CSV dont le nom contient `premium`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### Configurer une connexion source pour ingérer les données de manière récursive

Lors de la création d’une connexion source, vous pouvez utiliser le paramètre `recursive` pour ingérer des données à partir de dossiers profondément imbriqués.

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

Dans l’exemple ci-dessous, le paramètre `recursive: true` informe [!DNL Flow Service] de lire tous les sous-dossiers de manière récursive pendant le processus d’ingestion.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## Créer un schéma XDM cible {#target-schema}

Pour que les données sources soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Le schéma cible est ensuite utilisé pour créer un jeu de données Platform contenant les données sources.

Un schéma XDM cible peut être créé en adressant une requête POST à l’[API Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, suivez le tutoriel sur la [création d’un schéma à l’aide de l’API](../../../../xdm/api/schemas.md).

## Créer un jeu de données cible {#target-dataset}

Un jeu de données cible peut être créé en adressant une requête POST à l’[API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) et en fournissant l’identifiant du schéma cible dans la payload.

Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, suivez le tutoriel sur la [création d’un jeu de données à l’aide de l’API](../../../../catalog/api/create-dataset.md).

## Créer une connexion cible {#target-connection}

Une connexion cible représente la connexion à la destination où se trouvent les données ingérées. Pour créer une connexion cible, vous devez indiquer l’identifiant de spécification de connexion fixe associé au lac de données. Cet identifiant de connexion spécifique est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma cible, d’un jeu de données cible et de l’identifiant de spécification de connexion au lac de données. À l’aide de ces identifiants, vous pouvez créer une connexion cible grâce à l’API [!DNL Flow Service] pour spécifier le jeu de données qui contiendra les données source entrantes.

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
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
| `data.schema.version` | La version du schéma. Cette valeur doit être définie sur `application/vnd.adobe.xed-full+json;version=1`, qui renvoie la dernière version mineure du schéma. |
| `params.dataSetId` | Identifiant du jeu de données cible généré à l’étape précédente. **Remarque** : vous devez fournir un identifiant de jeu de données valide lors de la création d’une connexion cible. Un identifiant de jeu de données non valide entraînera une erreur. |
| `connectionSpec.id` | Identifiant de spécification de connexion utilisé pour se connecter au lac de données. Cet identifiant est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique de la nouvelle connexion cible (`id`). Cet identifiant est requis aux étapes suivantes.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Créer un mappage {#mapping}

Pour que les données sources soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible se rattache.

Pour créer un jeu de mappages, envoyez une requête POST au point d’entrée `mappingSets` de l’[[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) tout en fournissant votre schéma XDM cible `$id` et les détails des jeux de mappages que vous souhaitez créer.

>[!TIP]
>
>Vous pouvez désormais mapper des types de données complexes, tels que des tableaux dans des fichiers JSON en utilisant un connecteur source d’espace de stockage.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
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
            }
        ]
    }'
```

| Propriété | Description |
| --- | --- |
| `xdmSchema` | Identifiant du schéma XDM cible. |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Cette valeur est requise lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Récupérer des spécifications du flux de données {#specs}

Un flux de données est chargé de collecter des données provenant de sources et de les importer dans Platform. Afin de créer un flux de données, vous devez d’abord obtenir les spécifications du flux de données responsables de la collecte des données de stockage dans le cloud.

**Format d’API**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!NOTE]
>
>Le payload de réponse JSON ci-dessous est masqué pour plus de concision. Sélectionnez &quot;payload&quot; pour afficher la payload de réponse.

+++ Afficher la payload

**Réponse**

Une réponse réussie renvoie les détails de la spécification du flux de données responsable de l’importation des données de votre source dans Platform. La réponse inclut la valeur `id` unique de spécification de flux requise pour créer un flux de données.

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
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
  },
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
  "transformationSpec": [
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
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## Créer un flux de données

La dernière étape de la collecte des données de stockage dans le cloud consiste à créer un flux de données. Vous disposez à présent des valeurs requises suivantes :

- [ID de connexion source](#source)
- [ID de connexion cible](#target)
- [Identifiant de mappage](#mapping)
- [ID de spécification de flux de données](#specs)

Un flux de données est chargé de planifier et de collecter les données provenant d’une source. Vous pouvez créer un flux de données en exécutant une requête POST et en fournissant les valeurs mentionnées précédemment dans la payload.

>[!NOTE]
>
>Pour l’ingestion par lots, chaque flux de données qui s’ensuit sélectionne les fichiers à ingérer à partir de votre source en fonction de la date et heure de leur **dernière modification**. Cela signifie que les flux de données par lot sélectionnent des fichiers de la source qui sont nouveaux ou qui ont été modifiés depuis la dernière exécution du flux de données.

Pour planifier une ingestion, vous devez d’abord définir la valeur de l’heure de début en temps Unix en secondes. Vous devez ensuite définir la valeur de fréquence sur l’une des cinq options suivantes : `once`, `minute`, `hour`, `day` ou `week`. La valeur de l’intervalle désigne la période entre deux ingestions consécutives et aucun intervalle ne doit être défini pour la création d’une ingestion unique. Pour toutes les autres fréquences, la valeur de l’intervalle doit être égale ou supérieure à `15`.

>[!IMPORTANT]
>
>Il est vivement recommandé de planifier votre flux de données pour une ingestion unique lors de l’utilisation du [connecteur FTP](../../../connectors/cloud-storage/ftp.md).

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
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `flowSpec.id` | [Identifiant de spécification de flux](#specs) récupéré à l’étape précédente. |
| `sourceConnectionIds` | [Identifiant de connexion source](#source) récupéré lors d’une étape précédente. |
| `targetConnectionIds` | [Identifiant de connexion cible](#target-connection) récupéré lors d’une étape précédente. |
| `transformations.params.mappingId` | L’[identifiant de mappage](#mapping) récupéré lors d’une étape précédente. |
| `scheduleParams.startTime` | Heure de début du flux de données en temps Unix. |
| `scheduleParams.frequency` | Fréquence de collecte des données par le flux de données. Les valeurs possibles sont les suivantes : `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un nombre entier non nul. La valeur minimale de l’intervalle accepté pour chaque fréquence est la suivante :<ul><li>**Une fois** : n/a</li><li>**Minute** : 15</li><li>**Heure** : 1</li><li>**Jour** : 1</li><li>**Semaine** : 1</li></ul> |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du flux de données nouvellement créé.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les exécutions du flux, le statut d’achèvement et les erreurs. Pour plus d’informations sur la surveillance des flux de données, consultez le tutoriel sur la [surveillance des flux de données dans l’API](../monitor.md)

## Étapes suivantes

Grâce à ce tutoriel, vous avez créé un connecteur source permettant de collecter les données de votre espace de stockage à intervalles réguliers. Ces données entrantes peuvent désormais être utilisées par les services Platform en aval, comme [!DNL Real-Time Customer Profile] et [!DNL Data Science Workspace]. Consultez les documents suivants pour plus d’informations :

- [Vue d’ensemble du profil client en temps réel](../../../../profile/home.md)
- [Présentation de l’espace de travail de science des données](../../../../data-science-workspace/home.md)

## Annexe {#appendix}

La section suivante répertorie les différents connecteurs de source de stockage dans le cloud et leurs spécifications de connexion.

### Spécification de connexion

| Nom du connecteur | Spécification de connexion |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (Concentrateur d’événements) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |

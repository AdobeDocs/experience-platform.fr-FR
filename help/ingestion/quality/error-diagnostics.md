---
keywords: Experience Platform ; accueil ; rubriques populaires ; assimilation par lots ; assimilation par lots ; assimilation partielle ; assimilation partielle ; extraction de l'erreur ; extraction de l'erreur ; extraction de l'erreur ; erreur ; assimilation partielle du lot ; assimilation partielle ; assimilation ; assimilation ; diagnostic d'erreur ; récupération des diagnostics d'erreur ; obtention d'erreurs ; obtention d'erreurs ; récupération des erreurs ;
solution: Experience Platform
title: Récupération des diagnostics d'erreur de gestion des données
topic-legacy: overview
description: Ce document fournit des informations sur la surveillance de l'assimilation des lots, la gestion des erreurs d'assimilation partielle des lots, ainsi qu'une référence pour les types d'assimilation partielle des lots.
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 35%

---

# Récupération des diagnostics d&#39;erreur d&#39;assimilation des données

Adobe Experience Platform propose deux méthodes de chargement et d’ingestion de données. Vous pouvez utiliser l’assimilation par lot, qui vous permet d’insérer des données à l’aide de différents types de fichiers (tels que les fichiers CSV), ou l’assimilation en flux continu, qui vous permet d’insérer leurs données dans [!DNL Platform] à l’aide de points de terminaison en flux continu en temps réel.

Ce document fournit des informations sur la surveillance de l&#39;assimilation des lots, la gestion des erreurs d&#39;assimilation partielle des lots, ainsi qu&#39;une référence pour les types d&#39;assimilation partielle des lots.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): Méthodes d’envoi des données à  [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Schema Registry], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

## Téléchargement des diagnostics d&#39;erreur {#download-diagnostics}

Adobe Experience Platform permet aux utilisateurs de télécharger les diagnostics d’erreur des fichiers d’entrée. Les diagnostics seront conservés dans un délai de [!DNL Platform] jusqu&#39;à 30 jours.

### Fichiers d’entrée de liste {#list-files}

La requête suivante récupère une liste de tous les fichiers fournis dans un lot finalisé.

**Format d’API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous recherchez. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des objets JSON détaillant l&#39;emplacement d&#39;enregistrement des diagnostics.

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Récupérer les diagnostics des fichiers d&#39;entrée {#retrieve-diagnostics}

Une fois que vous avez récupéré une liste de tous les différents fichiers d’entrée, vous pouvez récupérer les diagnostics du fichier individuel à l’aide de la requête suivante.

**Format d’API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous recherchez. |
| `{FILE}` | Nom du fichier auquel vous accédez. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des objets JSON contenant des objets `path` détaillant l&#39;emplacement d&#39;enregistrement des diagnostics. La réponse renvoie les objets `path` au format [Lignes JSON](https://jsonlines.org/).

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Récupérer les erreurs d&#39;assimilation par lots {#retrieve-errors}

Si les lots contiennent des échecs, vous devez récupérer les informations d’erreur sur ces échecs afin de pouvoir réassimiler les données.

### Vérification de l’état {#check-status}

Pour vérifier l’état du lot ingéré, vous devez indiquer l’identifiant du lot dans le chemin d’une requête GET.

**Format d’API**

```http
GET /catalog/batches/{BATCH_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | Valeur `id` du lot dont vous voulez vérifier l’état. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse sans erreurs**

Une réponse positive est renvoyée avec des informations détaillées sur l&#39;état du lot.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| Propriété | Description |
| -------- | ----------- |
| `metrics.failedRecordCount` | Nombre de lignes qui n’ont pas pu être traitées en raison de l’analyse, de la conversion ou de la validation. Cette valeur peut être déduite en soustrayant `inputRecordCount` de `outputRecordCount`. Cette valeur est générée sur tous les lots, même si `errorDiagnostics` est activé. |

**Réponse avec erreurs**

Si le lot comporte une ou plusieurs erreurs et que les diagnostics d’erreur sont activés, la réponse renvoie plus d’informations sur les erreurs, à la fois dans la charge utile elle-même et dans un fichier d’erreur téléchargeable. Notez que l&#39;état d&#39;un lot contenant des erreurs peut toujours avoir un état de réussite.

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `metrics.failedRecordCount` | Nombre de lignes qui n’ont pas pu être traitées en raison de l’analyse, de la conversion ou de la validation. Cette valeur peut être déduite en soustrayant `inputRecordCount` de `outputRecordCount`. Cette valeur est générée sur tous les lots, même si `errorDiagnostics` est activé. |
| `errors.recordCount` | Nombre de lignes qui ont échoué pour le code d’erreur spécifié. Cette valeur est **générée uniquement** si `errorDiagnostics` est activé. |

>[!NOTE]
>
>Si les diagnostics d’erreur ne sont pas disponibles, le message d’erreur suivant s’affiche à la place :
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Étapes suivantes {#next-steps}

Ce didacticiel explique comment surveiller les erreurs d&#39;assimilation partielle de lots. Pour plus d’informations sur l’ingestion par lots, consultez le [guide de développement de l’ingestion par lots](../batch-ingestion/api-overview.md).

## Annexe {#appendix}

Cette section fournit des informations supplémentaires sur les types d&#39;erreur d&#39;assimilation.

### Types d’erreurs d’ingestion par lots partielle {#partial-ingestion-types}

L&#39;assimilation partielle par lot comporte trois types d&#39;erreur différents lors de l&#39;assimilation de données :

- [Fichiers illisibles](#unreadable)
- [Schémas ou en-têtes non valides](#schemas-headers)
- [Lignes non analysables](#unparsable)

### Fichiers illisibles {#unreadable}

Si le lot ingéré contient des fichiers illisibles, les erreurs du lot seront jointes à celui-ci. Vous trouverez plus d’informations sur la récupération du lot rejeté dans le [guide sur la récupération des lots rejetés](../quality/retrieve-failed-batches.md).

### Schémas ou en-têtes non valides {#schemas-headers}

Si le lot ingéré comporte un schéma ou des en-têtes non valides, les erreurs du lot seront jointes à celui-ci. Vous trouverez plus d’informations sur la récupération du lot rejeté dans le [guide sur la récupération des lots rejetés](../quality/retrieve-failed-batches.md).

### Lignes non analysables {#unparsable}

Si le lot que vous avez assimilé contient des lignes non analysables, vous pouvez utiliser la requête suivante pour vue d’une liste de fichiers contenant des erreurs.

**Format d’API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | Valeur `id` du lot dans lequel vous récupérez les informations d’erreur. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste des fichiers qui contiennent des erreurs.

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Vous pouvez ensuite récupérer des informations détaillées sur les erreurs à l&#39;aide du [point de terminaison de récupération des diagnostics](#retrieve-diagnostics).

Vous trouverez ci-dessous un exemple de réponse de récupération du fichier d’erreur :

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```

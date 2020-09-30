---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;error diagnostics;retrieve error diagnostics;get error diagnostics;get error;get errors;retrieve errors;
solution: Experience Platform
title: Présentation de l’ingestion par lots partielle d’Adobe Experience Platform
topic: overview
description: Ce document fournit des informations sur la surveillance de l'assimilation des lots, la gestion des erreurs d'assimilation partielle des lots, ainsi qu'une référence pour les types d'assimilation partielle des lots.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 30%

---


# Récupération des diagnostics d&#39;erreur

Adobe Experience Platform propose deux méthodes de chargement et d’ingestion de données. You can either use batch ingestion, which allows you to insert data using various file types (such as CSVs), or streaming ingestion, which allows you to insert their data to [!DNL Platform] using streaming endpoints in real time.

Ce document fournit des informations sur la surveillance de l&#39;assimilation des lots, la gestion des erreurs d&#39;assimilation partielle des lots, ainsi qu&#39;une référence pour les types d&#39;assimilation partielle des lots.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[ ! Système de modèle de données d’expérience (XDM) DNL]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
- [[ !Ingestion des données Adobe Experience Platform DNL]](../home.md): Méthodes d’envoi des données à [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Schema Registry], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Téléchargement des diagnostics d&#39;erreur {#download-diagnostics}

Adobe Experience Platform permet aux utilisateurs de télécharger les diagnostics d’erreur des fichiers d’entrée. Les diagnostics seront conservés dans un délai [!DNL Platform] de 30 jours.

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

Une réponse réussie renvoie des objets JSON contenant `path` des objets détaillant l&#39;emplacement d&#39;enregistrement des diagnostics. La réponse renvoie les `path` objets au format Lignes [](https://jsonlines.org/) JSON.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Retrieve batch ingestion errors {#retrieve-errors}

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
| `metrics.failedRecordCount` | Nombre de lignes qui n’ont pas pu être traitées en raison de l’analyse, de la conversion ou de la validation. Cette valeur peut être déduite en soustrayant la valeur `inputRecordCount` de la `outputRecordCount`. Cette valeur est générée sur tous les lots, même si elle `errorDiagnostics` est activée. |

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
| `metrics.failedRecordCount` | Nombre de lignes qui n’ont pas pu être traitées en raison de l’analyse, de la conversion ou de la validation. Cette valeur peut être déduite en soustrayant la valeur `inputRecordCount` de la `outputRecordCount`. Cette valeur est générée sur tous les lots, même si elle `errorDiagnostics` est activée. |
| `errors.recordCount` | Nombre de lignes qui ont échoué pour le code d’erreur spécifié. Cette valeur est **générée uniquement** si `errorDiagnostics` elle est activée. |

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

Vous pouvez ensuite récupérer des informations détaillées sur les erreurs à l’aide du point de terminaison [de récupération des](#retrieve-diagnostics)diagnostics.

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

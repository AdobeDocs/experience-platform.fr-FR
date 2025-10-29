---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion par lots;Ingestion par lots;ingestion partielle;Ingestion partielle;Récupérer l’erreur;récupérer l’erreur;Récupérer l’erreur;Ingestion par lots partielle;ingestion partielle;ingestion;Ingestion;diagnostics d’erreur;récupérer les diagnostics d’erreur;obtenir les diagnostics d’erreur;obtenir l’erreur;obtenir les erreurs;récupérer les erreurs;
solution: Experience Platform
title: Récupération des diagnostics d’erreur d’ingestion de données
description: Ce document fournit des informations sur la surveillance de l’ingestion par lots, la gestion des erreurs d’ingestion par lots partiels ainsi qu’une référence pour les types d’ingestion par lots partiels.
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 36%

---

# Récupération des diagnostics d’erreur d’ingestion de données

Adobe Experience Platform propose deux méthodes de chargement et d’ingestion de données. Vous pouvez utiliser l’ingestion par lots, qui vous permet d’insérer des données à l’aide de divers types de fichiers (tels que des fichiers CSV), ou l’ingestion par flux, qui vous permet d’insérer leurs données dans les [!DNL Experience Platform] à l’aide de points d’entrée en continu en temps réel.

Ce document fournit des informations sur la surveillance de l’ingestion par lots, la gestion des erreurs d’ingestion par lots partiels ainsi qu’une référence pour les types d’ingestion par lots partiels.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md) : méthodes par lesquelles les données peuvent être envoyées à [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources d’[!DNL Experience Platform], y compris celles appartenant à l’[!DNL Schema Registry], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Téléchargement des diagnostics d’erreur {#download-diagnostics}

Adobe Experience Platform permet aux utilisateurs de télécharger les diagnostics d’erreur des fichiers d’entrée. Les diagnostics sont conservés pendant [!DNL Experience Platform] jours au maximum.

### Répertorier les fichiers d’entrée {#list-files}

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des objets JSON indiquant l’emplacement d’enregistrement des diagnostics.

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

### Récupération des diagnostics de fichier d’entrée {#retrieve-diagnostics}

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des objets JSON contenant des objets `path` indiquant l’emplacement d’enregistrement des diagnostics. La réponse renvoie les objets `path` au format [ Lignes JSON ](https://jsonlines.readthedocs.io/en/latest/).

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Récupérer les erreurs d’ingestion par lots {#retrieve-errors}

Si les lots contiennent des échecs, vous devez récupérer les informations d’erreur relatives à ces échecs afin de pouvoir réingérer les données.

### Vérification de l’état {#check-status}

Pour vérifier l’état du lot ingéré, vous devez fournir l’identifiant du lot dans le chemin d’accès d’une requête GET. Pour en savoir plus sur l’utilisation de cet appel API, consultez le [guide des points d’entrée de catalogue](../../catalog/api/list-objects.md).

**Format d’API**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | Valeur `id` du lot dont vous voulez vérifier l’état. |
| `{FILTER}` | Un paramètre de requête utilisé pour filtrer les résultats renvoyés dans la réponse. Plusieurs paramètres sont séparés par des esperluettes (`&`). Pour plus d’informations, consultez le guide sur le [filtrage des données du catalogue](../../catalog/api/filter-data.md). |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse sans erreur**

Une réponse réussie renvoie des informations détaillées sur le statut du lot.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | Nombre de lignes qui n’ont pas pu être traitées en raison d’une analyse, d’une conversion ou d’une validation. Cette valeur peut être dérivée en soustrayant la `inputRecordCount` de la `outputRecordCount` . Cette valeur est générée sur tous les lots, que le `errorDiagnostics` soit activé ou non. |

**Réponse avec erreurs**

Si le lot comporte une ou plusieurs erreurs et que les diagnostics d’erreur sont activés, la réponse renvoie plus d’informations sur les erreurs, à la fois dans la payload elle-même ainsi qu’un fichier d’erreur téléchargeable. Notez que le statut d’un lot contenant des erreurs peut toujours avoir le statut Succès .

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | Nombre de lignes qui n’ont pas pu être traitées en raison d’une analyse, d’une conversion ou d’une validation. Cette valeur peut être dérivée en soustrayant la `inputRecordCount` de la `outputRecordCount` . Cette valeur est générée sur tous les lots, que le `errorDiagnostics` soit activé ou non. |
| `errors.recordCount` | Nombre de lignes ayant échoué pour le code d’erreur spécifié. Cette valeur est générée **uniquement** si `errorDiagnostics` est activé. |

>[!NOTE]
>
>Si les diagnostics d’erreur ne sont pas disponibles, le message d’erreur suivant s’affiche à la place :
>
>```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Étapes suivantes {#next-steps}

Ce tutoriel explique comment surveiller les erreurs d’ingestion par lots partielles. Pour plus d’informations sur l’ingestion par lots, consultez le [guide de développement de l’ingestion par lots](../batch-ingestion/api-overview.md).

## Annexe {#appendix}

Cette section fournit des informations supplémentaires sur les types d’erreurs d’ingestion.

### Types d’erreurs d’ingestion par lots partielle {#partial-ingestion-types}

L’ingestion par lots partielle comporte trois types d’erreurs différents lors de l’ingestion de données :

- [Fichiers illisibles](#unreadable)
- [Schémas ou en-têtes non valides](#schemas-headers)
- [Lignes non analysables](#unparsable)

### Fichiers illisibles {#unreadable}

Si le lot ingéré contient des fichiers illisibles, les erreurs du lot seront jointes à celui-ci. Vous trouverez plus d’informations sur la récupération du lot rejeté dans le [guide sur la récupération des lots rejetés](../quality/retrieve-failed-batches.md).

### Schémas ou en-têtes non valides {#schemas-headers}

Si le lot ingéré comporte un schéma ou des en-têtes non valides, les erreurs du lot seront jointes à celui-ci. Vous trouverez plus d’informations sur la récupération du lot rejeté dans le [guide sur la récupération des lots rejetés](../quality/retrieve-failed-batches.md).

### Lignes non analysables {#unparsable}

Si le lot que vous avez ingéré contient des lignes non analysables, vous pouvez utiliser la requête suivante pour afficher une liste de fichiers contenant des erreurs.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste des fichiers comportant des erreurs.

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

Vous pouvez ensuite récupérer des informations détaillées sur les erreurs à l’aide du point d’entrée [récupération des diagnostics](#retrieve-diagnostics).

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

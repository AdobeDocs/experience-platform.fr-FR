---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’ingestion par lots partielle d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: ac75b1858b6a731915bbc698107f0be6043267d8
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 38%

---



# Ingestion par lots partielle

L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont traitées par lots séparément, avec des détails sur les raisons de leur non-validité.

Ce document fournit un tutoriel pour la gestion de l’ingestion par lots partielle.

En outre, l’[annexe](#appendix) de ce tutoriel contient une référence pour les types d’erreurs d’ingestion par lots partielle.

## Prise en main

Ce tutoriel nécessite une connaissance pratique des différents services Adobe Experience Platform impliqués dans l’ingestion par lots partielle. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [Ingestion par lots](./overview.md)[!DNL Platform] : méthode d’ingestion et de stockage de données de fichiers, par exemple de type CSV et Parquet, dans 
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

The following sections provide additional information that you will need to know in order to successfully make calls to [!DNL Platform] APIs.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Enable a batch for partial batch ingestion in the API {#enable-api}

>[!NOTE]
>
>Cette section décrit l&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;API. For instructions on using the UI, please read the [enable a batch for partial batch ingestion in the UI](#enable-ui) step.

Vous pouvez créer un nouveau lot avec l&#39;assimilation partielle activée.

Pour créer un nouveau lot, suivez les étapes décrites dans le guide [du développeur d&#39;assimilation](./api-overview.md)par lot. Once you reach the **[!UICONTROL Create batch]** step, add the following field within the request body:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propriété | Description |
| -------- | ----------- |
| `enableErrorDiagnostics` | Indicateur qui permet [!DNL Platform] de générer des messages d&#39;erreur détaillés sur votre lot. |
| `partialIngestionPercentage` | Pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Ainsi, dans cet exemple, un maximum de 5 % du lot peut être une erreur, avant qu’il ne soit endommagé. |


## Enable a batch for partial batch ingestion in the UI {#enable-ui}

>[!NOTE]
>
>Cette section décrit l&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;interface utilisateur. Si vous avez déjà activé un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;API, vous pouvez passer à la section suivante.

Pour activer un lot pour l’assimilation partielle via l’ [!DNL Platform] interface utilisateur, vous pouvez créer un nouveau lot par le biais des connexions source, créer un nouveau lot dans un jeu de données existant ou créer un nouveau lot par le biais du flux[!UICONTROL &quot;]Mapper le fichier CSV au fichier XDM&quot;.

### Créer une connexion source {#new-source}

Pour créer une connexion à la source, suivez les étapes répertoriées dans l&#39;aperçu [des](../../sources/home.md)sources. Once you reach the **[!UICONTROL Dataflow detail]** step, take note of the **[!UICONTROL Partial ingestion]** and **[!UICONTROL Error diagnostics]** fields.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the *[!UICONTROL Partial ingestion]* toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Le **[!UICONTROL seuil d’erreur]** vous permet de définir le pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

### Utilisation d’un jeu de données existant {#existing-dataset}

Pour utiliser un jeu de données existant, début en sélectionnant un jeu de données. La barre latérale droite contient des informations sur le jeu de données.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Le **[!UICONTROL seuil d’erreur]** vous permet de définir le pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

Désormais, vous pouvez transférer des données à l’aide du bouton **Ajouter les données** et elles seront ingérées à l’aide de l’assimilation partielle.

### Utilisation du flux &quot;[!UICONTROL Mapper le fichier CSV au schéma]XDM&quot; {#map-flow}

Pour utiliser le flux &quot;[!UICONTROL Mapper un fichier CSV au schéma]XDM&quot;, suivez les étapes répertoriées dans le didacticiel [](../tutorials/map-a-csv-file.md)Mapper un fichier CSV. Once you reach the **[!UICONTROL Add data]** step, take note of the **[!UICONTROL Partial ingestion]** and **[!UICONTROL Error diagnostics]** fields.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Le **[!UICONTROL seuil d’erreur]** vous permet de définir le pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

## Téléchargement de métadonnées au niveau du fichier {#download-metadata}

Adobe Experience Platform permet aux utilisateurs de télécharger les métadonnées des fichiers d’entrée. Les métadonnées seront conservées dans un délai [!DNL Platform] de 30 jours.

### Fichiers d’entrée de liste {#list-files}

La requête suivante vous permet de vue une liste de tous les fichiers fournis dans un lot finalisé.

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des objets JSON contenant des objets de chemin détaillant l’emplacement d’enregistrement des métadonnées.

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Récupération des métadonnées du fichier d’entrée {#retrieve-metadata}

Une fois que vous avez récupéré une liste de tous les différents fichiers d’entrée, vous pouvez récupérer les métadonnées du fichier individuel en utilisant le point de terminaison suivant.

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des objets JSON contenant des objets de chemin détaillant l’emplacement d’enregistrement des métadonnées.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Récupération des erreurs d’ingestion par lots partielle {#retrieve-errors}

Si les lots contiennent des défaillances, vous devrez récupérer les informations d’erreur les concernant afin de pouvoir ingérer à nouveau les données.

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
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse sans erreurs**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur l’état du lot.

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
| `metrics.failedRecordCount` | Nombre de lignes qui n’ont pas pu être traitées en raison de l’analyse, de la conversion ou de la validation. Cette valeur peut être déduite en soustrayant la valeur `inputRecordCount` de la `outputRecordCount`. Cette valeur sera générée sur tous les lots, même si `errorDiagnostics` elle est activée. |

**Réponse avec erreurs**

Si le lot comporte une ou plusieurs erreurs et que les diagnostics d&#39;erreur sont activés, l&#39;état est `success` accompagné d&#39;informations supplémentaires sur les erreurs fournies dans la réponse et dans un fichier d&#39;erreur téléchargeable.

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
| `metrics.failedRecordCount` | Nombre de lignes qui n’ont pas pu être traitées en raison de l’analyse, de la conversion ou de la validation. Cette valeur peut être déduite en soustrayant la valeur `inputRecordCount` de la `outputRecordCount`. Cette valeur sera générée sur tous les lots, même si `errorDiagnostics` elle est activée. |
| `errors.recordCount` | Nombre de lignes qui ont échoué pour le code d’erreur spécifié. Cette valeur est **générée uniquement** si `errorDiagnostics` elle est activée. |

>[!NOTE]
>
>Si les diagnostics d’erreur ne sont pas disponibles, le message d’erreur suivant s’affiche à la place :
> 
```json
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## Étapes suivantes {#next-steps}

Ce tutoriel explique comment créer ou modifier un jeu de données pour activer l’ingestion par lots partielle. Pour plus d’informations sur l’ingestion par lots, consultez le [guide de développement de l’ingestion par lots](./api-overview.md).

## Types d’erreurs d’ingestion par lots partielle {#appendix}

L&#39;assimilation partielle par lot comporte trois types d&#39;erreur différents lors de l&#39;assimilation de données.

- [Fichiers illisibles](#unreadable)
- [Schémas ou en-têtes non valides](#schemas-headers)
- [Lignes non analysables](#unparsable)

### Fichiers illisibles {#unreadable}

Si le lot ingéré contient des fichiers illisibles, les erreurs du lot seront jointes à celui-ci. Vous trouverez plus d’informations sur la récupération du lot rejeté dans le [guide sur la récupération des lots rejetés](../quality/retrieve-failed-batches.md).

### Schémas ou en-têtes non valides {#schemas-headers}

Si le lot ingéré comporte un schéma ou des en-têtes non valides, les erreurs du lot seront jointes à celui-ci. Vous trouverez plus d’informations sur la récupération du lot rejeté dans le [guide sur la récupération des lots rejetés](../quality/retrieve-failed-batches.md).

### Lignes non analysables {#unparsable}

Si le lot que vous avez assimilé contient des lignes non analysables, vous pouvez utiliser le point de terminaison suivant pour vue une liste de fichiers contenant des erreurs.

**Format d’API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | Valeur `id` du lot dans lequel vous récupérez les informations d’erreur. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec une liste des fichiers qui contiennent des erreurs.

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

Vous pouvez ensuite récupérer des informations détaillées sur les erreurs à l’aide du point de terminaison [de récupération des](#retrieve-metadata)métadonnées.

Vous trouverez ci-dessous un exemple de réponse de récupération du fichier d’erreur :

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```

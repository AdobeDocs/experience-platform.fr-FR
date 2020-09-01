---
keywords: Experience Platform;home;popular topics;data ingestion;batch;Batch;enable dataset;Batch ingestion overview;overview;batch ingestion overview;
solution: Experience Platform
title: Présentation de l’ingestion par lots d’Adobe Experience Platform
topic: overview
description: L’API Batch Ingestion vous permet d’ingérer des données dans Adobe Experience Platform sous forme de fichiers de lots. Les données en cours d’ingestion peuvent être les données du profil d’un fichier plat dans un système CRM (par exemple un fichier parquet) ou des données conformes à un schéma connu dans le registre Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 82%

---


# [!DNL Batch Ingestion] aperçu

The [!DNL Batch Ingestion] API allows you to ingest data into Adobe Experience Platform as batch files. Data being ingested can be the profile data from a flat file in a CRM system (such as a parquet file), or data that conforms to a known schema in the [!DNL Experience Data Model] (XDM) registry.

La [référence de l’API Data Ingestion](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) fournit des informations supplémentaires sur ces appels d’API.

Le diagramme suivant décrit le processus d’ingestion par lots :

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Utilisation de l’API

The [!DNL Data Ingestion] API allows you to ingest data as batches (a unit of data that consists of one or more files to be ingested as a single unit) into [!DNL Experience Platform] in three basic steps:

1. Création d’un nouveau filtre.
2. Chargez des fichiers vers un jeu de données spécifique qui correspond au schéma XDM des données.
3. Signale la fin du lot.


### [!DNL Data Ingestion] conditions préalables

- Les données à charger doivent être au format Parquet ou JSON.
- A dataset created in the [[!DNL Catalog services]](../../catalog/home.md).
- Le contenu du fichier parquet doit correspondre à un sous-ensemble du schéma du jeu de données en cours de chargement.
- Obtenez votre jeton d’accès unique après l’authentification.

### Bonnes pratiques d’ingestion par lots

- La taille du lot recommandée est comprise entre 256 Mo et 100 Go.
- Chaque lot doit contenir au maximum 1 500 fichiers.

Pour charger un fichier de plus de 512 Mo, vous devez le diviser en petits blocs. Vous trouverez des instructions pour charger un fichier volumineux [ici](#large-file-upload---create-file).

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

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

### Création d’un lot

Avant de pouvoir ajouter des données à un jeu de données, elles doivent être liées à un lot, qui sera ensuite chargé dans un jeu de données spécifié.

```http
POST /batches
```

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Propriété | Description |
| -------- | ----------- |
| `datasetId` | Identifiant du jeu de données dans lequel charger les fichiers. |

**Réponse**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Identifiant du lot qui vient d’être créé (utilisé dans les demandes ultérieures). |
| `relatedObjects.id` | Identifiant du jeu de données dans lequel charger les fichiers. |

## Chargement des fichiers

Une fois le nouveau lot créé avec succès pour le chargement, les fichiers peuvent désormais être chargés dans le jeu de données spécifique.

Vous pouvez charger des fichiers à l’aide de **l’API Small File Upload**. Toutefois, si vos fichiers sont trop volumineux et que la limite de la passerelle est dépassée (par exemple, délais d’expiration étendus, demandes de taille de corps dépassés et autres contraintes), vous pouvez passer à **l’API Large File Upload**. Cette API charge le fichier par blocs et assemble les données à l’aide de l’appel à l’**API Large File Upload Complete**.

>[!NOTE]
>
>Les exemples ci-dessous utilisent le format de fichier [parquet](https://parquet.apache.org/documentation/latest/). Vous trouverez un exemple d’utilisation du format de fichier JSON dans le [guide de développement de l’ingestion par lots](./api-overview.md).

### Chargement de petits fichiers

Une fois un lot créé, les données peuvent être chargées vers un jeu de données préexistant.  Le fichier en cours de chargement doit correspondre à son schéma XDM référencé.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot. |
| `{DATASET_ID}` | Identifiant du jeu de données dans lequel charger les fichiers. |
| `{FILE_NAME}` | Nom du fichier tel qu’il sera affiché dans le jeu de données. |

**Requête**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Chemin et nom du fichier à charger dans le jeu de données. |

**Réponse**

```JSON
#Status 200 OK, with empty response body
```

### Chargement de fichiers volumineux - création d’un fichier

Pour charger un fichier volumineux, le fichier doit être divisé en petits blocs qui seront chargés un par un.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot. |
| `{DATASET_ID}` | Identifiant du jeu de données qui ingère les fichiers. |
| `{FILE_NAME}` | Nom du fichier tel qu’il sera affiché dans le jeu de données. |

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse**

```JSON
#Status 201 CREATED, with empty response body
```

### Chargement de fichiers volumineux - chargement des parties suivantes

Une fois le fichier créé, tous les blocs suivants peuvent être chargés en exécutant des requêtes PATCH répétées, une pour chaque section du fichier.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot. |
| `{DATASET_ID}` | Identifiant du jeu de données dans lequel charger les fichiers. |
| `{FILE_NAME}` | Nom du fichier tel qu’il sera affiché dans le jeu de données. |

**Requête**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Chemin et nom du fichier à charger dans le jeu de données. |

**Réponse**

```JSON
#Status 200 OK, with empty response
```

## Signalement de la fin du lot

Une fois que tous les fichiers ont été chargés dans le lot, il peut être marqué comme étant terminé. Cette action crée les entrées [!DNL Catalog]**DataSetFile** de pour les fichiers terminés et les associe au lot généré ci-dessus. The [!DNL Catalog] batch is then marked as successful, which triggers downstream flows to ingest the available data.

**Requête**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot à charger dans le jeu de données. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Réponse**

```JSON
#Status 200 OK, with empty response
```

## Vérifier l’état du lot

En attendant que les fichiers soient chargés dans le lot, vous pouvez vérifier l’état du lot pour voir sa progression.

**Format d’API**

```http
GET /batch/{BATCH_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot en cours d’analyse. |

**Requête**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `{USER_ID}` | Identifiant de l’utilisateur qui a créé ou mis à jour le lot. |

Le champ `"status"` indique l’état actuel du lot demandé. Les lots peuvent avoir l’un des états suivants :

## États de l’ingestion par lot

| État | Description |
| ------ | ----------- |
| Abandonné | Le lot ne s’est pas terminé dans le délai prévu. |
| Interrompu | Une opération pour interrompre l’opération a été **explicitement** appelée (via l’API Batch Ingest) pour le lot spécifié. Une fois le lot **chargé**, il ne peut plus être interrompu. |
| Actif | Le lot a été converti avec succès et est disponible pour la consommation en aval. Cet état peut être utilisé de manière interchangeable avec **Succès**. |
| Supprimé | Les données du lot ont été entièrement supprimées. |
| Échoué | État final résultant d’une configuration incorrecte et/ou de mauvaises données. Les données d’un lot qui a échoué **ne s’affichent pas**. Cet état peut être utilisé de manière interchangeable avec **Échec**. |
| Inactif | La conversion du lot a réussi, mais a été annulée ou a expiré. Le lot n’est plus disponible pour la consommation en aval. |
| Chargé | Les données du lot sont transférées et le lot est prêt pour la promotion. |
| Chargement | Les données de ce lot sont en cours de chargement et le lot **n’est actuellement pas** prêt à être converti. |
| Nouvelle tentative | Les données de ce lot sont en cours de traitement. Cependant, en raison d’une erreur système ou transitoire, le lot a échoué. Par conséquent, une nouvelle tentative pour ce lot est en cours. |
| Évalué | La phase d’évaluation du processus de promotion d’un lot est terminée et la tâche d’ingestion a été exécutée. |
| Évaluation | Les données du lot sont en cours de traitement. |
| Bloqué | Les données du lot sont en cours de traitement. Toutefois, la promotion par lot est bloquée après un certain nombre de tentatives. |
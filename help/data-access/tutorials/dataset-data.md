---
keywords: Experience Platform;home;popular topics;data access;data access api;query data access
solution: Experience Platform
title: Présentation de Data Access
topic: tutorial
description: Ce document propose un tutoriel détaillé qui explique comment localiser, accéder et télécharger les données stockées dans un jeu de données à l’aide de l’API Data Access d’Adobe Experience Platform. Certaines des fonctionnalités uniques de l’API Data Access vous seront également présentées comme la pagination et les téléchargements partiels.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 72%

---


# Query dataset data using [!DNL Data Access] API

This document provides a step-by-step tutorial that covers how to locate, access, and download data stored within a dataset using the [!DNL Data Access] API in Adobe Experience Platform. You will also be introduced to some of the unique features of the [!DNL Data Access] API, such as paging and partial downloads.

## Prise en main

Ce didacticiel nécessite une compréhension pratique de la création et du remplissage d&#39;un jeu de données. Pour plus d’informations, consultez le [tutoriel sur la création de jeux de données](../../catalog/datasets/create.md).

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API Platform.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

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

## Graphique de séquences

This tutorial follows the steps outlined in the sequence diagram below, highlighting the core functionality of the [!DNL Data Access] API.</br>
![](../images/sequence_diagram.png)

The [!DNL Catalog] API allows you to retrieve information regarding batches and files. The [!DNL Data Access] API allows you to access and download these files over HTTP as either full or partial downloads, depending on the size of the file.

## Localisation des données

Before you can begin to use the [!DNL Data Access] API, you need to identify the location of the data that you want to access. In the [!DNL Catalog] API, there are two endpoints that you can use to browse an organization&#39;s metadata and retrieve the ID of a batch or file that you want to access:

- `GET /batches` : renvoie une liste de lots sous votre organisation
- `GET /dataSetFiles` : renvoie une liste de fichiers sous votre organisation

For a comprehensive list of endpoints in the [!DNL Catalog] API, please refer to the [API Reference](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

## Récupération d’une liste de lots sous votre organisation IMS

Using the [!DNL Catalog] API, you can return a list of batches under your organization:

**Format d’API**

```http
GET /batches
```

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse inclut un objet qui répertorie tous les lots associés à l’organisation IMS, chaque valeur de niveau supérieur représentant un lot. Les objets de lot individuels contiennent les détails pour ce lot spécifique. La réponse ci-dessous a été réduite pour gagner de l’espace.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### Filtrage de la liste de lots

Les filtres sont souvent nécessaires pour trouver un lot en particulier et récupérer des données pertinentes à un cas d’utilisation spécifique. Vous pouvez ajouter des paramètres à une requête `GET /batches` afin de filtrer la réponse renvoyée. La requête ci-dessous renverra tous les lots créés après une période spécifique, au sein d’un jeu de données particulier, triés selon la date à laquelle ils ont été créés.

**Format d’API**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Propriété | Description |
| -------- | ----------- |
| `{START_TIMESTAMP}` | La date et l’heure de départ en millisecondes (par exemple, 1514836799000). |
| `{DATASET_ID}` | L’identifiant du jeu de données. |
| `{SORT_BY}` | Trie la réponse en fonction de la valeur fournie. Par exemple, `desc:created` trie les objets en fonction de leur date de création dans l’ordre décroissant. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{IMS_ORG}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

Vous trouverez une liste complète des paramètres et des filtres dans la [référence de l’API Catalog](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

## Récupération d’une liste de tous les fichiers appartenant à un lot spécifique

Now that you have the ID of the batch that you want to access, you can use the [!DNL Data Access] API to get a list of files belonging to that batch.

**Format d’API**

```http
GET /batches/{BATCH_ID}/files
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot auquel vous souhaitez accéder. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| Propriété | Description |
| -------- | ----------- |
| `data._links.self.href` | L’URL d’accès à ce fichier. |

La réponse contient un tableau de données qui répertorie tous les fichiers au sein du lot spécifié. Les fichiers sont référencés par leur identifiant de fichier que vous pouvez trouver sous le champ `dataSetFileId`.

## Accès à un fichier à l’aide d’un identifiant de fichier

Once you have a unique file ID, you can use the [!DNL Data Access] API to access the specific details about the file, including its name, size in bytes, and a link to download it.

**Format d’API**

```http
GET /files/{FILE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID}` | L’identifiant du fichier auquel vous souhaitez accéder. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Selon que l’identifiant de fichier pointe vers un fichier individuel ou un répertoire, le tableau de données renvoyé peut contenir une seule entrée ou une liste de fichiers appartenant à ce répertoire. Chaque élément de fichier contiendra des détails comme le nom du fichier, sa taille en octets et un lien de téléchargement du fichier.

**Cas 1 : l’identifiant de fichier pointe vers un fichier unique**

**Réponse**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | Le nom du fichier. |
| `_links.self.href` | L’URL de téléchargement du fichier. |

**Cas 2 : l’identifiant de fichier pointe vers un répertoire.**

**Réponse**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
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

| Propriété | Description |
| -------- | ----------- | 
| `data._links.self.href` | L’URL de téléchargement du fichier associé. |

Cette réponse renvoie un répertoire contenant deux fichiers séparés portant les identifiants `{FILE_ID_2}` et `{FILE_ID_3}`. Dans ce scénario, vous devez suivre l’URL de chaque fichier pour y accéder.

## Récupération des métadonnées d’un fichier

Vous pouvez récupérer les métadonnées d’un fichier en effectuant une requête HEAD. Cette opération renvoie les en-têtes des métadonnées du fichier, y compris sa taille en octets et son format de fichier.

**Format d’API**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID}` | L’identifiant du fichier. |
| `{FILE_NAME}` | Le nom du fichier (par exemple, profiles.parquet). |

**Requête**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Les en-têtes de réponse contiennent les métadonnées du fichier interrogé, notamment :
- `Content-Length` : indique la taille du payload en octets
- `Content-Type` : indique le type de fichier.

## Accès aux contenus d’un fichier

You can also access the contents of a file using the [!DNL Data Access] API.

**Format d’API**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID}` | L’identifiant du fichier. |
| `{FILE_NAME}` | Le nom du fichier (par exemple, profiles.parquet). |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie le contenu du fichier.

## Téléchargement du contenu partiel d’un fichier

The [!DNL Data Access] API allows for downloading files in chunks. Vous pouvez indiquer un en-tête de plage pendant une requête `GET /files/{FILE_ID}` pour télécharger une plage d’octets spécifique d’un fichier. Si la plage n’est pas spécifiée, l’API téléchargera l’intégralité du fichier par défaut.

L’exemple HEAD de la [section précédente](#retrieve-the-metadata-of-a-file) donne la taille d’un fichier particulier en octets.

**Format d’API**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID} ` | L’identifiant du fichier. |
| `{FILE_NAME}` | Le nom du fichier (par exemple, profiles.parquet). |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Propriété | Description |
| -------- | ----------- | 
| `Range: bytes=0-99` | Précise la plage d’octets à télécharger. Si celle-ci n’est pas précisée, l’API téléchargera l’intégralité du fichier. Dans cet exemple, les 100 premiers octets seront téléchargés. |

**Réponse**

Le corps de la réponse inclut les 100 premiers octets du fichier (comme indiqué par l’en-tête « Plage » dans la requête) avec un état HTTP 206 (Partial Contents). La réponse inclut également les en-têtes suivants :

- Content-Length : 100 (le nombre d’octets renvoyé)
- Content-type : application/parquet (un fichier parquet a été demandé, c’est pourquoi le type de contenu de la réponse est parquet)
- Content-Range : bytes 0-99/249058 (la plage demandée (0-99) sur le nombre total d’octets (249058))

## Configuration de la pagination des réponses de l’API

Responses within the [!DNL Data Access] API are paginated. Par défaut, 100 est le nombre maximal d’entrées par page. Vous pouvez utiliser les paramètres de pagination pour modifier le comportement par défaut.

- `limit` : vous pouvez spécifier le nombre d’entrées par page en fonction de vos besoins à l’aide du paramètre « limit ».
- `start` : le décalage peut être défini par le paramètre de requête « start ».
- `&` : vous pouvez utiliser une esperluette pour combiner plusieurs paramètres en un appel unique.

**Format d’API**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot auquel vous souhaitez accéder. |
| `{OFFSET}` | L’index spécifié pour démarrer le tableau de résultat (par exemple, start=0) |
| `{LIMIT}` | Contrôle le nombre de résultats renvoyé dans le tableau de résultat (par exemple, limit=1) |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse** :

La réponse contient un tableau `"data"` contenant un seul élément comme indiqué par le paramètre de demande `limit=1`. Cet élément est un objet contenant les détails du premier fichier disponible, comme indiqué par le paramètre `start=0` dans la requête (n’oubliez pas qu’en numérotation basée sur zéro, le premier élément est « 0 »).

La valeur `_links.next.href` contient le lien vers la page de réponses suivante sur laquelle vous pouvez voir que le paramètre `start` est passé à `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```

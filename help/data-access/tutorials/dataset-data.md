---
keywords: Experience Platform;accueil;rubriques populaires;accès aux données;api d’accès aux données;accès aux données de requête
solution: Experience Platform
title: Affichage des données d’un jeu de données à l’aide de l’API Data Access
type: Tutorial
description: Découvrez comment localiser, accéder et télécharger des données stockées dans un jeu de données à l’aide de l’API Data Access de Adobe Experience Platform. Certaines des fonctionnalités uniques de l’API Data Access vous seront également présentées comme la pagination et les téléchargements partiels.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 73%

---

# Affichage des données d’un jeu de données à l’aide de [!DNL Data Access] API

Ce document fournit un tutoriel détaillé qui explique comment localiser, accéder et télécharger des données stockées dans un jeu de données à l’aide du [!DNL Data Access] API dans Adobe Experience Platform. Vous découvrirez également certaines des fonctionnalités uniques de la [!DNL Data Access] API, telles que la pagination et les téléchargements partiels.

## Prise en main

Ce tutoriel nécessite une compréhension pratique de la création et du remplissage d’un jeu de données. Pour plus d’informations, consultez le [tutoriel sur la création de jeux de données](../../catalog/datasets/create.md).

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API Platform.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Graphique de séquences

Ce tutoriel suit les étapes décrites dans le diagramme de séquence ci-dessous, mettant en évidence les fonctionnalités de base de la fonction [!DNL Data Access] API.</br>
![](../images/sequence_diagram.png)

Le [!DNL Catalog] L’API vous permet de récupérer des informations concernant les lots et les fichiers. Le [!DNL Data Access] L’API vous permet d’accéder à ces fichiers et de les télécharger via HTTP sous la forme de téléchargements complets ou partiels, selon la taille du fichier.

## Localisation des données

Avant de commencer à utiliser la variable [!DNL Data Access] API, vous devez identifier l’emplacement des données auxquelles vous souhaitez accéder. Dans le [!DNL Catalog] API, vous pouvez utiliser deux points de terminaison pour parcourir les métadonnées d’une organisation et récupérer l’identifiant d’un lot ou d’un fichier auquel vous souhaitez accéder :

- `GET /batches` : renvoie une liste de lots sous votre organisation
- `GET /dataSetFiles` : renvoie une liste de fichiers sous votre organisation

Pour obtenir une liste complète des points de fin dans la variable [!DNL Catalog] API, reportez-vous à la section [Référence d’API](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Récupération d’une liste de lots sous votre organisation

En utilisant la variable [!DNL Catalog] API, vous pouvez renvoyer une liste de lots sous votre organisation :

**Format d’API**

```http
GET /batches
```

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse comprend un objet qui répertorie tous les lots associés à l’organisation, chaque valeur de niveau supérieur représentant un lot. Les objets de lot individuels contiennent les détails pour ce lot spécifique. La réponse ci-dessous a été réduite pour gagner de l’espace.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

Vous trouverez une liste complète des paramètres et des filtres dans la [référence de l’API Catalog](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Récupération d’une liste de tous les fichiers appartenant à un lot spécifique

Maintenant que vous disposez de l’identifiant du lot auquel vous souhaitez accéder, vous pouvez utiliser la variable [!DNL Data Access] API pour obtenir une liste des fichiers appartenant à ce lot.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une fois que vous disposez d’un identifiant de fichier unique, vous pouvez utiliser la variable [!DNL Data Access] API pour accéder aux détails spécifiques sur le fichier, notamment son nom, sa taille en octets et un lien de téléchargement.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Les en-têtes de réponse contiennent les métadonnées du fichier interrogé, notamment :
- `Content-Length` : indique la taille du payload en octets
- `Content-Type` : indique le type de fichier.

## Accès aux contenus d’un fichier

Vous pouvez également accéder au contenu d’un fichier à l’aide de l’option [!DNL Data Access] API.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie le contenu du fichier.

## Téléchargement du contenu partiel d’un fichier

Le [!DNL Data Access] L’API permet de télécharger des fichiers par blocs. Vous pouvez indiquer un en-tête de plage pendant une requête `GET /files/{FILE_ID}` pour télécharger une plage d’octets spécifique d’un fichier. Si la plage n’est pas spécifiée, l’API téléchargera l’intégralité du fichier par défaut.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Propriété | Description |
| -------- | ----------- | 
| `Range: bytes=0-99` | Précise la plage d’octets à télécharger. Si celle-ci n’est pas précisée, l’API téléchargera l’intégralité du fichier. Dans cet exemple, les 100 premiers octets seront téléchargés. |

**Réponse**

Le corps de la réponse inclut les 100 premiers octets du fichier (comme indiqué par l’en-tête « Plage » dans la requête) avec un état HTTP 206 (Partial Contents). La réponse inclut également les en-têtes suivants :

- Content-Length : 100 (le nombre d’octets renvoyé)
- Content-type : application/parquet (un fichier Parquet a été demandé, par conséquent le type de contenu de la réponse est `parquet`)
- Content-Range : bytes 0-99/249058 (la plage demandée (0-99) sur le nombre total d’octets (249058))

## Configuration de la pagination des réponses de l’API

Réponses dans la variable [!DNL Data Access] Les API sont mises en page. Par défaut, 100 est le nombre maximal d’entrées par page. Vous pouvez utiliser les paramètres de pagination pour modifier le comportement par défaut.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

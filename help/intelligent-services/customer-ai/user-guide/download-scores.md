---
keywords: Experience Platform;télécharger des scores;service clientèle;rubriques les plus consultées;exportation;téléchargement de l’assistance client;scores de l’assistance client
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Scores de téléchargement dans Customer AI
description: Customer AI vous permet de télécharger des scores au format de fichier Parquet.
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 72%

---

# Téléchargement de scores dans Customer AI

Ce document sert de guide pour télécharger des scores dans Customer AI.

## Prise en main

Customer AI vous permet de télécharger des scores au format de fichier Parquet. Pour suivre ce tutoriel, vous devez avoir terminé de lire la section consacrée au téléchargement de scores Customer AI dans le [guide de prise en main](../getting-started.md).

De plus, pour accéder aux scores dans Customer AI, vous devez disposer d’une instance de service avec un état d’exécution réussi disponible. Pour créer une instance de service, consultez la page [Configuration d’une instance Customer AI](./configure.md). Si vous avez récemment créé une instance de service et qu’elle est toujours en cours de formation et de notation, comptez 24 heures pour qu’elle se termine.

Actuellement, il existe deux manières de télécharger les scores Customer AI :

1. Si vous souhaitez télécharger les scores au niveau individuel et/ou si Real-Time Customer Profile n’est pas activé, commencez par accéder à [la recherche de l’identifiant de votre jeu de données](#dataset-id).
2. Si Profile est activé et que vous souhaitez télécharger les segments que vous avez configurés à l’aide de Customer AI, [téléchargez un segment configuré avec Customer AI](#segment).

## Recherche de votre identifiant de jeu de données {#dataset-id}

Dans votre instance de service d’informations Customer AI, cliquez sur la liste déroulante *Actions supplémentaires* dans le volet de navigation en haut à droite, puis sélectionnez **[!UICONTROL Accéder aux scores]**.

![actions supplémentaires](../images/insights/more-actions.png)

Une boîte de dialogue s’affiche. Elle contient un lien vers la documentation des scores de téléchargement et l’identifiant du jeu de données de votre instance actuelle. Copiez l’identifiant du jeu de données dans votre presse-papiers et passez à l’étape suivante.

![Identifiant du jeu de données](../images/download-scores/access-scores.png)

## Récupération de votre identifiant de lot {#retrieve-your-batch-id}

À l’aide de l’identifiant de jeu de données de l’étape précédente, vous devez effectuer un appel à l’API Catalog afin de récupérer un identifiant de lot. Des paramètres de requête supplémentaires sont utilisés pour cet appel API afin de renvoyer le dernier lot réussi au lieu d’une liste de lots appartenant à votre organisation. Pour renvoyer des lots supplémentaires, augmentez le nombre du paramètre de requête limite à la valeur souhaitée que vous souhaitez voir renvoyer. Pour plus d’informations sur les types de paramètres de requête disponibles, consultez le guide sur le [filtrage des données Catalogue à l’aide des paramètres de requête](../../../catalog/api/filter-data.md).

**Format d’API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | Identifiant du jeu de données disponible dans la boîte de dialogue « Accéder aux scores ». |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant un objet d’identifiant de lot. Dans cet exemple, la valeur clé de l’objet renvoyé est l’identifiant de lot `01E5QSWCAASFQ054FNBKYV6TIQ`. Copiez l’identifiant de lot à utiliser dans l’appel API suivant.

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## Récupération de l’appel API suivant avec l’identifiant de lot {#retrieve-the-next-api-call-with-your-batch-id}

Une fois que vous disposez de l’identifiant de lot, vous pouvez adresser une nouvelle requête GET à `/batches`. La requête renvoie un lien utilisé pour la requête d’API suivante.

**Format d’API**

```http
GET batches/{BATCH_ID}/files
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant de lot récupéré à l’étape précédente, [récupération de votre identifiant de lot](#retrieve-your-batch-id). |

**Requête**

En utilisant votre propre identifiant de lot, effectuez la requête suivante.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant un objet `_links`. L’objet `_links` contient une valeur `href` ayant un nouvel appel API comme valeur. Copiez cette valeur pour passer à l’étape suivante.

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
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

## Récupération de vos fichiers {#retrieving-your-files}

À l’aide de la valeur `href` obtenue à l’étape précédente comme appel API, effectuez une nouvelle requête GET pour récupérer votre répertoire de fichiers.

**Format d’API**

```http
GET files/{DATASETFILE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L’identifiant dataSetFile est renvoyé dans la valeur `href` de l’[étape précédente](#retrieve-the-next-api-call-with-your-batch-id). Il est aussi accessible dans le tableau `data`, sous le type d’objet `dataSetFileId`. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse contient un tableau de données qui peut comporter une entrée unique ou une liste de fichiers liés à ce répertoire. L’exemple ci-dessous contient une liste de fichiers et a été condensé pour en faciliter la lecture. Dans ce scénario, vous devez suivre l’URL de chaque fichier pour y accéder.

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| Paramètre | Description |
| --------- | ----------- |
| `_links.self.href` | L’URL de la requête GET utilisée pour télécharger un fichier dans votre répertoire. |


Copiez la valeur `href` de chaque objet de fichier du tableau `data`, puis passez à l’étape suivante.

## Télécharger vos données de fichier

Pour télécharger vos données de fichier, envoyez une requête GET vers la valeur `"href"` que vous avez copiée à l’étape précédente [récupération de vos fichiers](#retrieving-your-files).

>[!NOTE]
>
>Si vous effectuez cette requête directement dans la ligne de commande, vous serez peut-être invité à ajouter une sortie après les en-têtes de la requête. L’exemple de requête suivant utilise `--output {FILENAME.FILETYPE}`.

**Format d’API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L’identifiant dataSetFile est renvoyé dans la valeur `href` d’une [étape précédente](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Nom du fichier. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Assurez-vous que vous vous trouvez dans le répertoire ou le dossier dans lequel vous souhaitez enregistrer votre fichier avant d’effectuer la demande de GET.

**Réponse**

La réponse télécharge le fichier que vous avez demandé dans votre répertoire actuel. Dans cet exemple, le nom de fichier est « filename.parquet ».

![Terminal](../images/download-scores/response.png)

## Téléchargement d’un segment configuré avec Customer AI {#segment}

Vous pouvez aussi télécharger vos données de score en exportant votre audience vers un jeu de données. Une fois la tâche de segmentation terminée (la valeur de l’attribut `status` est « SUCCEEDED »), vous pouvez exporter votre audience vers un jeu de données permettant son accès et son utilisation. Pour en savoir plus sur la segmentation, consultez la [présentation de la segmentation](../../../segmentation/home.md).

>[!IMPORTANT]
>
>Afin d’utiliser cette méthode d’exportation, Real-Time Customer Profile doit être activé pour le jeu de données.

La section [Exportation d’un segment](../../../segmentation/tutorials/evaluate-a-segment.md) du guide d’évaluation des segments décrit les étapes requises pour exporter un jeu de données d’audience. Le guide décrit les étapes suivantes et fournit des exemples de celles-ci :

- **Création d’un jeu de données cible :** créez le jeu de données pour retenir les membres de l’audience.
- **Génération de profils d’audience dans le jeu de données :** renseignez le jeu de données avec des profils individuels XDM en fonction des résultats d’une tâche de segmentation.
- **Contrôle de la progression de l’exportation :** vérifiez la progression actuelle du processus d’exportation.
- **Lecture des données d’audience :** récupérez les profils individuels XDM obtenus représentant les membres de votre audience.

## Étapes suivantes

Ce document décrit les étapes requises pour télécharger des scores Customer AI. Vous pouvez maintenant continuer à parcourir les autres [services intelligents](../../home.md) et guides proposés.

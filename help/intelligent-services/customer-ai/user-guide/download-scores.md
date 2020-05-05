---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: Téléchargement de scores dans l’API client
topic: Downloading scores
translation-type: tm+mt
source-git-commit: 7c892d92a50312fb4b733431737b796651689804

---


# Téléchargement de scores dans l’API client

Ce document sert de guide pour le téléchargement de scores pour l’IA du client.

## Prise en main

Customer AI vous permet de télécharger des partitions au format de fichier parquet. Ce didacticiel nécessite que vous ayez lu et terminé la section Téléchargement des scores d’IA client dans le guide de [prise en main](../getting-started.md) .

De plus, pour accéder aux scores de l’IA du client, vous devez disposer d’une instance de service avec un état d’exécution réussi. Pour créer une instance de service, consultez [Configuration d’une instance](./configure.md)d’API client. Si vous avez récemment créé une instance de service et qu’elle continue à s’entraîner et à marquer des points, veuillez lui accorder 24 heures pour qu’elle se termine.

Actuellement, il existe deux méthodes pour télécharger les scores d’IA client :

1. Si vous souhaitez télécharger les scores au niveau individuel et/ou si le Profil client en temps réel n’est pas activé, début en accédant à la [recherche de votre ID](#dataset-id)de jeu de données.
2. Si le Profil est activé et que vous souhaitez télécharger les segments que vous avez configurés à l’aide de l’API du client, naviguez pour [télécharger un segment configuré avec l’IA](#segment)du client.

## Find your dataset ID {#dataset-id}

Dans votre instance de service pour obtenir des informations sur l’IA du client, cliquez sur la liste déroulante *Autres actions* dans le volet de navigation supérieur droit, puis sélectionnez **[!UICONTROL Access scores]**.

![Autres actions](../images/insights/more-actions.png)

Une nouvelle boîte de dialogue s’affiche, contenant un lien vers la documentation des scores de téléchargement et l’ID du jeu de données de votre instance actuelle. Copiez l’ID du jeu de données dans le Presse-papiers et passez à l’étape suivante.

![ID de jeu de données](../images/download-scores/access-scores.png)

## Récupérer votre identifiant de lot {#retrieve-your-batch-id}

En utilisant l’ID de votre jeu de données de l’étape précédente, vous devez appeler l’API Catalog pour récupérer un identifiant de lot. D&#39;autres paramètres de requête sont utilisés pour cet appel d&#39;API afin de renvoyer le dernier lot réussi au lieu d&#39;une liste de lots appartenant à votre organisation. Pour renvoyer des lots supplémentaires, augmentez le nombre du paramètre de requête limite à la quantité souhaitée à renvoyer. Pour plus d’informations sur les types de paramètres de requête disponibles, consultez le guide sur le [filtrage des données du catalogue à l’aide de paramètres](../../../catalog/api/filter-data.md)de requête.

**Format d’API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | ID du jeu de données disponible dans la boîte de dialogue &quot;Accéder aux scores&quot;. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant un objet d’identifiant de lot. Dans cet exemple, la valeur clé de l’objet renvoyé est l’identifiant du lot `01E5QSWCAASFQ054FNBKYV6TIQ`. Copiez l’ID de lot à utiliser dans l’appel d’API suivant.

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

## Récupérez le prochain appel d’API avec votre identifiant de lot. {#retrieve-the-next-api-call-with-your-batch-id}

Une fois que vous disposez de votre identifiant de lot, vous pouvez faire une nouvelle demande GET à `/batches`. La requête renvoie un lien utilisé comme requête d’API suivante.

**Format d’API**

```http
GET batches/{BATCH_ID}/files
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID de lot récupéré à l’étape précédente [récupère votre ID](#retrieve-your-batch-id)de lot. |

**Requête**

En utilisant votre propre ID de lot, effectuez la requête suivante.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant un `_links` objet. L’ `_links` objet contient un appel `href` d’API dont la valeur est un nouvel appel d’API. Copiez cette valeur pour passer à l’étape suivante.

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

## Récupérer vos fichiers {#retrieving-your-files}

En utilisant la `href` valeur obtenue à l’étape précédente comme appel d’API, effectuez une nouvelle demande GET pour récupérer votre répertoire de fichiers.

**Format d’API**

```http
GET files/{DATASETFILE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile est renvoyé dans la `href` valeur de l&#39;étape [](#retrieve-the-next-api-call-with-your-batch-id)précédente. Il est également accessible dans le `data` tableau sous le type d&#39;objet `dataSetFileId`. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse contient un tableau de données qui peut comporter une entrée unique ou une liste de fichiers appartenant à ce répertoire. L&#39;exemple ci-dessous contient une liste de fichiers et a été condensé pour en faciliter la lecture. Dans ce scénario, vous devez suivre l’URL de chaque fichier pour accéder au fichier.

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
| `_links.self.href` | URL de demande GET utilisée pour télécharger un fichier dans votre répertoire. |


Copiez la `href` valeur de tout objet de fichier dans le `data` tableau, puis passez à l&#39;étape suivante.

## Télécharger vos données de fichier

Pour télécharger vos données de fichier, faites une requête GET à la `"href"` valeur que vous avez copiée à l’étape précédente [récupérant vos fichiers](#retrieving-your-files).

>[!NOTE] Si vous effectuez cette requête directement en ligne de commande, vous pouvez être invité à ajouter une sortie après les en-têtes de la requête. L&#39;exemple de demande suivant utilise `--output {FILENAME.FILETYPE}`.

**Format d’API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile est renvoyé dans la `href` valeur d&#39;une étape [](#retrieve-the-next-api-call-with-your-batch-id)précédente. |
| `{FILE_NAME}` | Nom du fichier. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP] Assurez-vous que vous vous trouvez dans le répertoire ou le dossier dans lequel vous souhaitez enregistrer votre fichier avant d’effectuer la demande GET.

**Réponse**

La réponse télécharge le fichier que vous avez demandé dans votre répertoire actuel. Dans cet exemple, le nom de fichier est &quot;filename.parquet&quot;.

![Terminal](../images/download-scores/response.png)

## Téléchargement d’un segment configuré avec l’API du client {#segment}

Une autre façon de télécharger vos données de score consiste à exporter votre audience dans un jeu de données. Une fois la tâche de segmentation terminée (la valeur de l’ `status` attribut est &quot;SUCCEEDED&quot;), vous pouvez exporter votre audience dans un jeu de données où elle est accessible et où vous pouvez agir. Pour en savoir plus sur la segmentation, consultez la présentation [de la](../../../segmentation/home.md)segmentation.

>[!IMPORTANT] Pour utiliser cette méthode d’exportation, le Profil client en temps réel doit être activé pour le jeu de données.

La section [Exporter un segment](../../../segmentation/tutorials/evaluate-a-segment.md) du guide d’évaluation des segments décrit les étapes requises pour exporter un jeu de données d’audience. Le guide décrit et fournit des exemples des éléments suivants :

- **Créez un jeu de données de cible :** Créez le jeu de données pour contenir les membres d&#39;audience.
- **Générer des profils d’audience dans le jeu de données :** Remplissez le jeu de données avec des Profils individuels XDM en fonction des résultats d’une tâche de segment.
- **Suivre la progression de l&#39;exportation :** Vérifier la progression actuelle du processus d&#39;exportation.
- **Lire les données d&#39;audience :** Récupérez les Profils individuels XDM résultants représentant les membres de votre audience.

## Étapes suivantes

Ce document décrit les étapes requises pour télécharger les scores d’IA client. Vous pouvez maintenant continuer à parcourir les autres services [et guides](../../home.md) intelligents qui sont proposés.

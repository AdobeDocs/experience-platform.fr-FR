---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: Téléchargement de scores dans l’API client
topic: Downloading scores
translation-type: tm+mt
source-git-commit: 387cbdebccb9ae54a2907d1afe220e9711927ca6

---


# Téléchargement de scores dans l’API client

Ce sert de guide pour le téléchargement des scores pour l’IA du client.

## Prise en main

Customer AI vous permet de télécharger des scores au format de fichier parquet. Ce didacticiel nécessite que vous ayez lu et terminé la section des scores AI client téléchargée dans le guide de [prise en main](./getting-started.md) .

De plus, pour accéder aux scores de l’API client, vous devez disposer d’une instance de service avec un état d’exécution réussi. Pour créer une nouvelle instance de service, consultez le guide [d’utilisation de l’API du](./user-guide.md)client. Si vous avez récemment créé une instance de service et qu’elle est toujours en cours d’entraînement et de notation, veuillez compter 24 heures pour qu’elle se termine.

Actuellement, il existe deux manières de télécharger les scores AI du client :

1. Si vous souhaitez télécharger les scores au niveau individuel et/ou si le Client en temps réel n’est pas activé,  en recherchant l’ID [](#dataset-id)de votre jeu de données.
2. Si  est activé et que vous souhaitez télécharger les segments que vous avez configurés à l’aide de l’API du client, naviguez pour [télécharger un segment configuré avec l’API](#segment)du client.

## Find your dataset ID {#dataset-id}

Dans votre instance de service pour obtenir des informations sur l’IA du client, cliquez sur la liste déroulante Actions ** supplémentaires dans le volet de navigation supérieur droit, puis sélectionnez des scores d’ **accès**.

![autres actions](./images/insights/more-actions.png)

Une nouvelle boîte de dialogue s’affiche, contenant un lien vers la documentation des scores de téléchargement et l’ID du jeu de données de votre instance actuelle. Copiez l’ID du jeu de données dans le Presse-papiers et passez à l’étape suivante.

![ID du jeu de données](./images/download-scores/access-scores.png)

## Récupérez votre identifiant de lot {#retrieve-your-batch-id}

En utilisant votre ID de jeu de données de l’étape précédente, vous devez appeler l’API Catalog pour récupérer un ID de lot. Des paramètres  supplémentaires sont utilisés pour cet appel d’API afin de renvoyer un seul lot au lieu d’un de lots appartenant à votre organisation. Pour plus d’informations sur les types de paramètres  de disponibles, consultez le guide sur le [filtrage des données du catalogue à l’aide de paramètres](../../catalog/api/filter-data.md)de.

**Format API**

```http
GET /batches?&dataSet={DATASET_ID}&orderBy=desc:created&limit=1
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | ID du jeu de données disponible dans la boîte de dialogue &quot;Accès aux scores&quot;. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant un objet d’ID de lot de score. In this example, the object is `5e602f67c2f39715a87f46b1`.

L’objet d’ID de lot de score contient un `relatedObjects` tableau. Ce tableau contient deux objets. Le premier objet a la `type` valeur &quot;batch&quot; et contient également un ID. Dans l’exemple de réponse ci-dessous, l’ID de lot est `035e2520-5e69-11ea-b624-51evfeba55d1`. Copiez l’ID de lot à utiliser dans l’appel d’API suivant.

```json
{   
    "5e602f67c2f39715a87f46b1": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540e14cd3d0432",
                "type": "dataSet"
            },
            {
                "id": "035e2520-5e69-11ea-b624-51evfeba55d1",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsRead": 46721830,
            "recordsWritten": 46721830,
            "avgNumExecutorsPerTask": 33,
            "startTime": 1583362385336,
            "inputSizeInKb": 10242034,
            "endTime": 1583363197517
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    }
}
```

## Récupérez le prochain appel d’API avec votre ID de lot {#retrieve-the-next-api-call-with-your-batch-id}

Une fois que vous avez votre identifiant de lot, vous pouvez effectuer une nouvelle demande GET à `/batches`. La requête renvoie un lien utilisé comme requête d’API suivante.

**Format API**

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

Une réponse réussie renvoie une charge utile contenant un `_links` objet. Dans l’ `_links` objet se trouve une valeur `href` avec un nouvel appel d’API. Copiez cette valeur pour passer à l’étape suivante.

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

**Format API**

```http
GET files/{DATASETFILE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L’ID dataSetFile est renvoyé dans la `href` valeur de l’étape [](#retrieve-the-next-api-call-with-your-batch-id)précédente. Il est également accessible dans le `data` tableau sous le type d’objet `dataSetFileId`. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse contient un tableau de données qui peut comporter une entrée unique ou un de fichiers appartenant à ce répertoire. L&#39;exemple ci-dessous contient un  de fichiers et a été condensé pour en faciliter la lecture. Dans ce scénario, vous devez suivre l’URL de chaque fichier pour accéder au fichier.

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


Copiez la `href` valeur de tout objet de fichier dans le `data` tableau, puis passez à l’étape suivante.

## Télécharger vos données de fichier

Pour télécharger vos données de fichier, faites une requête GET vers la `"href"` valeur que vous avez copiée à l’étape précédente [récupérant vos fichiers](#retrieving-your-files).

>[!NOTE] Si vous effectuez cette requête directement dans la ligne de commande, vous serez peut-être invité à ajouter une sortie après les en-têtes de votre requête. L’exemple de requête suivant utilise `--output {FILENAME.FILETYPE}`.

**Format API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L’ID dataSetFile est renvoyé dans la `href` valeur à partir d’une étape [](#retrieve-the-next-api-call-with-your-batch-id)précédente. |
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

![Terminal](./images/download-scores/response.png)

## Téléchargement d’un segment configuré avec l’API du client {#segment}

Vous pouvez également télécharger vos données de score en exportant votre   vers un jeu de données. Une fois la tâche de segmentation terminée (la valeur de l’ `status` attribut est &quot;SUCCEEDED&quot;), vous pouvez exporter votre  dans un jeu de données où vous pouvez y accéder et y donner suite. Pour en savoir plus sur la segmentation, consultez la présentation [de la](../../segmentation/home.md)segmentation.

>[!IMPORTANT] Afin d’utiliser cette méthode d’exportation, les  du client en temps réel doivent être activées pour le jeu de données.

La section [Exporter un segment](../../segmentation/tutorials/evaluate-a-segment.md) du guide d’évaluation des segments décrit les étapes requises pour exporter un jeu de données  de . Le guide décrit et fournit des exemples des éléments suivants :

- **Créez un jeu de données  de :** Créez le jeu de données pour contenir  membres .
- **Générez    dans le jeu de données :** Renseigner le jeu de données avec des  individuels XDM en fonction des résultats d’une tâche de segment.
- **Surveiller la progression de l’exportation :** Vérifiez la progression actuelle du processus d’exportation.
- **Lire  données  du :** Récupérez le XDM individuel résultant représentant les membres de votre  de.

## Étapes suivantes

Ce décrit les étapes requises pour télécharger les scores AI du client. Vous pouvez maintenant continuer à parcourir les autres services [et guides](../home.md) intelligents proposés.

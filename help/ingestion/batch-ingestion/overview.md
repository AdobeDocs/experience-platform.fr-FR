---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’administration par lots d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Présentation de l&#39;importation par lot

L’API d’assimilation par lots vous permet d’assimiler des données dans Adobe Experience Platform sous forme de fichiers de commandes. Les données en cours d’assimilation peuvent être les données  d’un fichier plat dans un système CRM (par exemple un fichier parquet) ou les données conformes à un connu  dans le registre du modèle de données d’expérience (XDM).

La référence [de l’API d’](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) administration de données fournit des informations supplémentaires sur ces appels d’API.

Le diagramme suivant décrit le processus d’assimilation par lot :

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Utilisation de l’API

L’API d’assimilation des données vous permet d’assimiler des données sous forme de lots (une unité de données composée d’un ou de plusieurs fichiers à assimiler en une seule unité) dans la plateforme d’expérience en trois étapes de base :

1. Créez un lot.
2. Téléchargez des fichiers vers un jeu de données spécifique qui correspond au  XDM des données.
3. Signale la fin du lot.


### Conditions préalables requises pour l’insertion de données

- Les données à télécharger doivent être au format Parquet ou JSON.
- Jeu de données créé dans les services [de](../../catalog/home.md)catalogue.
- Le contenu du fichier parquet doit correspondre à un sous-ensemble du  du jeu de données dans lequel il est téléchargé.
- Ayez votre unique  après l’authentification.

### Meilleures pratiques d’assimilation par lot

- La taille de lot recommandée est comprise entre 256 Mo et 100 Go.
- Chaque lot doit contenir au plus 1 500 fichiers.

Pour télécharger un fichier de plus de 512 Mo, vous devez le diviser en petits morceaux. Vous trouverez des instructions pour télécharger un fichier volumineux [ici](#large-file-upload---create-file).

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

### Création d’un lot

Avant de pouvoir ajouter des données à un jeu de données, elles doivent être liées à un lot, qui sera ensuite transféré dans un jeu de données spécifié.

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
| `datasetId` | ID du jeu de données dans lequel télécharger les fichiers. |

**Répondre**

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
| `id` | ID du lot qui vient d’être créé (utilisé dans les demandes ultérieures). |
| `relatedObjects.id` | ID du jeu de données dans lequel télécharger les fichiers. |

## Téléchargement de fichier

Après avoir créé un nouveau lot à télécharger, vous pouvez télécharger des fichiers vers un jeu de données spécifique.

Vous pouvez télécharger des fichiers à l’aide de l’API **de téléchargement de** petits fichiers. Toutefois, si vos fichiers sont trop volumineux et que la limite de la passerelle est dépassée (délais d’expiration étendus, demandes de taille de corps dépassés et autres contraintes, par exemple), vous pouvez passer à l’API **de téléchargement de fichiers** volumineux. Cette API télécharge le fichier en morceaux et assemble les données à l’aide de l’appel API **de téléchargement de fichier** volumineux.

>[!NOTE] Les exemples ci-dessous utilisent le format de fichier [parquet](https://parquet.apache.org/documentation/latest/) . Vous trouverez un exemple d’utilisation du format de fichier JSON dans le guide [du développeur d’assimilation de](./api-overview.md)lot.

### Téléchargement de petits fichiers

Une fois un lot créé, les données peuvent être transférées vers un jeu de données préexistant.  Le fichier en cours de téléchargement doit correspondre à son  XDM référencé.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot. |
| `{DATASET_ID}` | ID du jeu de données à télécharger des fichiers. |
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
| `{FILE_PATH_AND_NAME}` | Chemin et nom de fichier du fichier à télécharger dans le jeu de données. |

**Répondre**

```JSON
#Status 200 OK, with empty response body
```

### Téléchargement de fichiers volumineux - créer un fichier

Pour télécharger un fichier volumineux, le fichier doit être divisé en petits morceaux et téléchargé un par un.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot. |
| `{DATASET_ID}` | ID du jeu de données qui imbrique les fichiers. |
| `{FILE_NAME}` | Nom du fichier tel qu’il sera affiché dans le jeu de données. |

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Répondre**

```JSON
#Status 201 CREATED, with empty response body
```

### Téléchargement de fichiers volumineux - transfert des parties suivantes

Une fois le fichier créé, tous les blocs suivants peuvent être téléchargés en exécutant des requêtes PATCH répétées, une pour chaque section du fichier.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot. |
| `{DATASET_ID}` | ID du jeu de données dans lequel télécharger les fichiers. |
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
| `{FILE_PATH_AND_NAME}` | Chemin et nom de fichier du fichier à télécharger dans le jeu de données. |

**Répondre**

```JSON
#Status 200 OK, with empty response
```

## Fin du lot de signaux

Une fois que tous les fichiers ont été téléchargés dans le lot, le lot peut être signalé pour achèvement. Ce faisant, les entrées Catalog **DataSetFile** sont créées pour les fichiers terminés et associées au lot généré ci-dessus. Le lot du catalogue est ensuite marqué comme une réussite, ce qui déclenche des flux en aval pour assimiler les données disponibles.

**Requête**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot à télécharger dans le jeu de données. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Répondre**

```JSON
#Status 200 OK, with empty response
```

## Vérifier l&#39;état du lot

En attendant que les fichiers soient téléchargés dans le lot, vous pouvez vérifier l’état du lot pour voir sa progression.

**Format API**

```http
GET /batch/{BATCH_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot en cours de vérification. |

**Requête**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Répondre**

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
| `{USER_ID}` | ID de l’utilisateur qui a créé ou mis à jour le lot. |

Le `"status"` champ indique l’état actuel du lot demandé. Les lots peuvent avoir l’un des états suivants :

## Etat d&#39;assimilation par lot

| État | Description |
| ------ | ----------- |
| Abandonné | Le lot n&#39;est pas terminé dans la période prévue. |
| Abordée | Une opération d’abandon a été **explicitement** appelée (via l’API d’assimilation par lot) pour le lot spécifié. Une fois le lot **chargé** , il ne peut plus être abandonné. |
| Actif | Le lot a été promu avec succès et est disponible pour la consommation en aval. Cet état peut être utilisé de manière interchangeable avec **Success**. |
| Supprimé | Les données du lot ont été complètement supprimées. |
| En échec | État terminal résultant d’une configuration incorrecte et/ou de données incorrectes. Les données d’un lot en panne **ne s’affichent pas** . Cet état peut être utilisé de manière interchangeable avec **Échec**. |
| Inactif | La promotion du lot a réussi, mais a été annulée ou a expiré. Le lot n’est plus disponible pour la consommation en aval. |
| Chargé | Les données du lot sont terminées et le lot est prêt pour la promotion. |
| Chargement | Les données de ce lot sont en cours de transfert et le lot **n’est actuellement pas** prêt à être promu. |
| Nouvelle tentative | Les données de ce lot sont en cours de traitement. Cependant, en raison d’une erreur système ou transitoire, le lot a échoué. Par conséquent, ce lot est en cours de nouvelle tentative. |
| Mis en scène | La phase d&#39;évaluation du processus de promotion d&#39;un lot est terminée et la tâche d&#39;assimilation a été exécutée. |
| Évaluation | Les données du lot sont en cours de traitement. |
| Bloqué | Les données du lot sont en cours de traitement. Toutefois, la promotion par lot est bloquée après un certain nombre de . |
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’importation par lots d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 2%

---


# Présentation de l&#39;importation par lot

L’API d’importation par lot vous permet d’assimiler des données dans Adobe Experience Platform sous forme de fichiers par lot. Les données ingérées peuvent être les données de profil d’un fichier plat dans un système de gestion de la relation client (par exemple un fichier de parquet) ou les données conformes à un schéma connu dans le registre du modèle de données d’expérience (XDM).

La référence [de l&#39;API d&#39;](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) administration de données fournit des informations supplémentaires sur ces appels d&#39;API.

Le diagramme suivant décrit le processus d&#39;assimilation par lot :

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Utilisation de l’API

L’API d’importation de données vous permet d’assimiler des données sous forme de lots (une unité de données composée d’un ou de plusieurs fichiers à assimiler en une seule unité) dans la plate-forme d’expérience en trois étapes de base :

1. Créez un lot.
2. Téléchargez des fichiers vers un jeu de données spécifié qui correspond au schéma XDM des données.
3. Signale la fin du lot.


### Prérequis pour l&#39;importation de données

- Les données à télécharger doivent être au format Parquet ou JSON.
- Jeu de données créé dans les services [de](../../catalog/home.md)catalogue.
- Le contenu du fichier parquet doit correspondre à un sous-ensemble du schéma du jeu de données dans lequel il est chargé.
- Ayez votre Jeton d&#39;accès unique après l’authentification.

### Meilleures pratiques d’assimilation par lot

- La taille de lot recommandée est comprise entre 256 Mo et 100 Go.
- Chaque lot doit contenir au plus 1 500 fichiers.

Pour télécharger un fichier de plus de 512 Mo, le fichier doit être divisé en petits morceaux. Les instructions pour télécharger un fichier volumineux sont disponibles [ici](#large-file-upload---create-file).

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

### Création d’un lot

Avant de pouvoir ajouter des données à un jeu de données, celles-ci doivent être liées à un lot, qui sera ensuite transféré dans un jeu de données spécifié.

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

**Réponses**

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

Après avoir créé un nouveau lot pour le transfert, les fichiers peuvent être téléchargés vers un jeu de données spécifique.

Vous pouvez télécharger des fichiers à l’aide de l’API **de téléchargement de** petits fichiers. Toutefois, si vos fichiers sont trop volumineux et que la limite de passerelle est dépassée (délais d’expiration étendus, demandes de taille de corps dépassés et autres contraintes, par exemple), vous pouvez passer à l’API **de téléchargement de fichiers** volumineux. Cette API télécharge le fichier en blocs et collecte les données ensemble à l’aide de l’appel API **de téléchargement de fichier** volumineux.

>[!NOTE] Les exemples ci-dessous utilisent le format de fichier [parquet](https://parquet.apache.org/documentation/latest/) . Vous trouverez un exemple d’utilisation du format de fichier JSON dans le guide [du développeur d’](./api-overview.md)assimilation par lot.

### Téléchargement de petits fichiers

Une fois un lot créé, les données peuvent être transférées vers un jeu de données préexistant.  Le fichier en cours de téléchargement doit correspondre à son schéma XDM référencé.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot. |
| `{DATASET_ID}` | ID du jeu de données à télécharger. |
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
| `{FILE_PATH_AND_NAME}` | Chemin d’accès et nom de fichier du fichier à télécharger dans le jeu de données. |

**Réponses**

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
| `{DATASET_ID}` | ID du jeu de données qui imprime les fichiers. |
| `{FILE_NAME}` | Nom du fichier tel qu’il sera affiché dans le jeu de données. |

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponses**

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
| `{FILE_PATH_AND_NAME}` | Chemin d’accès et nom de fichier du fichier à télécharger dans le jeu de données. |

**Réponses**

```JSON
#Status 200 OK, with empty response
```

## Fin du lot de signaux

Une fois que tous les fichiers ont été téléchargés dans le lot, celui-ci peut être signalé comme étant terminé. Ce faisant, les entrées **DataSetFile** du catalogue sont créées pour les fichiers terminés et associées au lot généré ci-dessus. Le lot de catalogue est ensuite marqué comme ayant réussi, ce qui déclenche des flux en aval pour assimiler les données disponibles.

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

**Réponses**

```JSON
#Status 200 OK, with empty response
```

## Vérifier l&#39;état du lot

En attendant que les fichiers soient téléchargés dans le lot, vous pouvez vérifier l&#39;état du lot pour voir sa progression.

**Format d’API**

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

**Réponses**

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

Le `"status"` champ indique l&#39;état actuel du lot demandé. Les lots peuvent avoir l’un des états suivants :

## Etat d’assimilation par lot

| État | Description |
| ------ | ----------- |
| Abandonné | Le lot n&#39;est pas terminé dans la période prévue. |
| Abandonné | Une opération d&#39;abandon a été **explicitement** appelée (via l&#39;API de réception par lot) pour le lot spécifié. Une fois le lot **chargé** , il ne peut plus être abandonné. |
| Actif | Le lot a été promu avec succès et est disponible pour la consommation en aval. Cet état peut être utilisé de manière interchangeable avec **Success**. |
| Supprimé | Les données du lot ont été complètement supprimées. |
| En échec | Etat de terminal résultant d’une configuration incorrecte et/ou de données incorrectes. Les données d&#39;un lot en panne **ne s&#39;affichent pas** . Cet état peut être utilisé de manière interchangeable avec **Échec**. |
| Inactif | La promotion du lot a réussi, mais a été annulée ou a expiré. Le lot n&#39;est plus disponible pour la consommation en aval. |
| Chargé | Les données du lot sont terminées et le lot est prêt pour la promotion. |
| Chargement | Les données de ce lot sont en cours de transfert et le lot **n&#39;est pas** actuellement prêt à être promu. |
| Nouvelle tentative | Les données de ce lot sont en cours de traitement. Cependant, en raison d&#39;une erreur système ou transitoire, le lot a échoué. Par conséquent, ce lot est de nouveau essayé. |
| Mis en scène | La phase d&#39;évaluation du processus de promotion d&#39;un lot est terminée et la tâche d&#39;assimilation a été exécutée. |
| Évaluation | Les données du lot sont en cours de traitement. |
| Bloqué | Les données du lot sont en cours de traitement. Cependant, la promotion par lot est bloquée après un certain nombre de Reprises. |
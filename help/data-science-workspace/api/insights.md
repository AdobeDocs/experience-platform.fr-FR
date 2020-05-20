---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Statistiques
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 4%

---


# Statistiques

Les statistiques contiennent des mesures qui permettent à un chercheur en données d’évaluer et de choisir des modèles ML optimaux en affichant les mesures d’évaluation appropriées.

## Récupération d’une liste d’informations

Vous pouvez récupérer une liste d’informations en exécutant une seule requête GET sur le point de terminaison d’informations.  Pour faciliter le filtrage des résultats, vous pouvez spécifier des paramètres de requête dans le chemin d’accès à la requête. Pour une liste des requêtes disponibles, reportez-vous à la section de l&#39;annexe sur les paramètres de [requête pour la récupération](./appendix.md#query)des ressources.

**Format d’API**

```http
GET /insights
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile qui inclut une liste d’informations et chaque information possède un identifiant unique ( `id` ). De plus, vous recevrez `context` qui contient les identifiants uniques associés à cette information particulière suite aux données des événements et mesures d’statistiques.

```json
{
    "children": [
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| Propriété | Description |
| --- | --- |
| `id` | ID correspondant à l’aperçu. |
| `experimentId` | ID d’expérience valide. |
| `experimentRunId` | ID d’exécution d’expérience valide. |
| `modelId` | ID de modèle valide. |

## Récupération d’une information spécifique

Pour rechercher une information particulière, effectuez une requête GET et fournissez une requête valide `{INSIGHT_ID}` dans le chemin de la requête. Pour faciliter le filtrage des résultats, vous pouvez spécifier des paramètres de requête dans le chemin d’accès à la requête. Pour une liste des requêtes disponibles, reportez-vous à la section de l&#39;annexe sur les paramètres de [requête pour la récupération](./appendix.md#query)des ressources.

**Format d’API**

```http
GET /insights/{INSIGHT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{INSIGHT_ID}` | Identificateur unique d’une information Sensei. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/{INSIGHT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile qui inclut l’identifiant unique d’informations (`id`). De plus, vous recevrez `context` qui contient les identifiants uniques associés aux informations particulières qui suivent les données des événements et mesures d’statistiques.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Propriété | Description |
| --- | --- |
| `id` | ID correspondant à l’aperçu. |
| `experimentId` | ID d’expérience valide. |
| `experimentRunId` | ID d’exécution d’expérience valide. |
| `modelId` | ID de modèle valide. |

## Ajouter une nouvelle connaissance du modèle

Vous pouvez créer une nouvelle vue du modèle en exécutant une requête POST et une charge utile qui fournit le contexte, les événements et les mesures pour la nouvelle vue du modèle. Le champ de contexte utilisé pour créer une nouvelle information sur le modèle n&#39;est pas nécessaire pour que des services existants y soient associés, mais vous pouvez choisir de créer la nouvelle information sur le modèle avec les services existants en fournissant un ou plusieurs des ID correspondants :

```json
"context": {
    "clientId": "{CLIENT_ID}",
    "notebookId": "{NOTEBOOK_ID}",
    "experimentId": "{EXPERIMENT_ID}",
    "engineId": "{ENGINE_ID}",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "modelId": "{MODEL_ID}",
    "dataSetId": "{DATASET_ID}"
  }
```

**Format d’API**

```http
POST /insights
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**Réponse**

Une réponse positive renvoie une charge utile contenant un paramètre `{INSIGHT_ID}` et tous les paramètres fournis dans la demande initiale.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Propriété | Description |
| --- | --- |
| `insightId` | ID unique créé pour cette information particulière lorsqu’une demande POST réussie est effectuée. |

## Récupération d’une liste de mesures par défaut pour les algorithmes

Vous pouvez récupérer une liste de toutes les mesures par défaut et de l’algorithme en exécutant une seule requête GET sur le point de terminaison des mesures. Pour requête une mesure particulière, effectuez une demande GET et fournissez une valeur valide `{ALGORITHM}` dans le chemin de la demande.

**Format d’API**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Paramètre | Description |
| --- | --- |
| `{ALGORITHM}` | Identificateur du type d’algorithme. |

**Requête**

La requête suivante contient une requête et récupère une mesure spécifique à l’aide de l’identifiant d’algorithme. `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile qui inclut l’identifiant `algorithm` unique et un tableau de mesures par défaut.

```json
{
    "children": [
        {
            "algorithm": "{ALGORITHM}",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```

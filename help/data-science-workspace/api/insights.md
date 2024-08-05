---
keywords: Experience Platform;guide de développement;point de terminaison;Data Science Workspace;rubriques les plus consultées;informations;api d’apprentissage automatique sensei
solution: Experience Platform
title: Point de terminaison de l’API Insights
description: Les informations contiennent des mesures qui permettent à un scientifique de données d’évaluer et de choisir des modèles ML optimaux en affichant les mesures d’évaluation appropriées.
role: Developer
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 91%

---

# Point d’entrée Insights

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Les informations contiennent des mesures qui permettent à un scientifique de données d’évaluer et de choisir des modèles ML optimaux en affichant les mesures d’évaluation appropriées.

## Récupération d’une liste d’informations

Vous pouvez récupérer une liste d’informations en effectuant une requête GET unique sur le point de terminaison des informations.  Pour vous aider à filtrer les résultats, vous pouvez spécifier des paramètres de requête dans le chemin de requête. Pour obtenir une liste des requêtes disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload incluant une liste d’informations, et chaque information dispose d’un identifiant unique ( `id` ). De plus, vous recevrez le champ `context` incluant les identifiants uniques associés à cette information spécifique ainsi que les événements d’informations et les données de mesures.

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `id` | L’identifiant correspondant à l’information. |
| `experimentId` | Un identifiant d’expérience valide. |
| `experimentRunId` | Un identifiant d’exécution d’expérience valide. |
| `modelId` | Un identifiant de modèle valide. |

## Récupération d’une information spécifique

Pour rechercher une information spécifique, effectuez une requête GET et fournissez un `{INSIGHT_ID}` valide dans le chemin d’accès de la requête. Pour vous aider à filtrer les résultats, vous pouvez spécifier des paramètres de requête dans le chemin de requête. Pour obtenir une liste des requêtes disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).

**Format d’API**

```http
GET /insights/{INSIGHT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{INSIGHT_ID}` | L’identifiant unique d’une information Sensei. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload incluant l’identifiant unique d’information (`id`). De plus, vous recevrez le champ `context` incluant les identifiants uniques associés à cette information spécifique ainsi que les événements d’informations et les données de mesures.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `id` | L’identifiant correspondant à l’information. |
| `experimentId` | Un identifiant d’expérience valide. |
| `experimentRunId` | Un identifiant d’exécution d’expérience valide. |
| `modelId` | Un identifiant de modèle valide. |

## Ajout d’une nouvelle information de modèle

Vous pouvez créer une information de modèle en effectuant une requête POST et un payload fournissant le contexte, les événements et les mesures de la nouvelle information de modèle. Le champ de contexte utilisé pour créer une information de modèle n’est pas nécessaire pour associer les services existants à l’information, mais vous pouvez choisir de créer l’information de modèle avec les services existants en fournissant un ou plusieurs des identifiants correspondants :

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

Une réponse réussie renvoie un payload incluant un `{INSIGHT_ID}` et tous les paramètres fournis dans la requête initiale.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `insightId` | L’ID unique créé pour cette information spécifique en cas de requête POST réussie. |

## Récupération d’une liste de mesures par défaut pour les algorithmes

Vous pouvez récupérer une liste de toutes les mesures de vos algorithmes et mesures par défaut en effectuant une requête GET unique sur le point d’entrée des mesures. Pour interroger une mesure spécifique, effectuez une requête GET et fournissez un `{ALGORITHM}` valide dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Paramètre | Description |
| --- | --- |
| `{ALGORITHM}` | L’identifiant du type d’algorithme. |

**Requête**

La requête suivante contient une requête et renvoie une mesure spécifique à l’aide de l’identifiant d’algorithme `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload incluant l’identifiant unique `algorithm` et un tableau de mesures par défaut.

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
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

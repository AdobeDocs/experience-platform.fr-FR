---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: MLInstances
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 4%

---


# MLInstances

Un MLInstance est une association d&#39;un [moteur](./engines.md) existant avec un ensemble approprié de configurations qui définit tous les paramètres d&#39;entraînement, paramètres d&#39;évaluation ou configurations de ressources matérielles.

## Création d’une instance MLI {#create-an-mlinstance}

Vous pouvez créer une instance MLInstance en exécutant une requête POST tout en fournissant une charge utile de requête composée d&#39;un ID de moteur (`{ENGINE_ID}`) valide et d&#39;un ensemble approprié de configurations par défaut.

Si l’ID de moteur fait référence à un moteur PySpark ou Spark, vous pouvez configurer la quantité de ressources de calcul telles que le nombre de coeurs ou la quantité de mémoire. Si un moteur Python est référencé, vous pouvez choisir d&#39;utiliser un processeur ou une GPU à des fins de formation et de notation. Pour plus d&#39;informations, reportez-vous aux sections de l&#39;annexe sur les configurations [de ressources](./appendix.md#resource-config) PySpark et Spark et les configurations [de processeur et de GPU](./appendix.md#cpu-gpu-config) Python.

**Format d’API**

```http
POST /mlInstances
```

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom souhaité pour l’instance MLInstance. Le modèle correspondant à cette instance MLInstance héritera de cette valeur à afficher dans l&#39;interface utilisateur en tant que nom du modèle. |
| `description` | Description facultative de l&#39;instance MLInstance. Le modèle correspondant à cette instance MLInstance héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description du modèle. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `engineId` | ID d&#39;un moteur existant. |
| `tasks` | Ensemble de configurations pour la formation, la notation ou les pipelines de fonctionnalités. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de l&#39;instance MLInstance nouvellement créée, y compris son identifiant unique (`id`).

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Récupération d&#39;une liste d&#39;instances MLI

Vous pouvez récupérer une liste d’instances MLInstances en exécutant une seule requête GET. Pour faciliter le filtrage des résultats, vous pouvez spécifier des paramètres de requête dans le chemin d’accès à la requête. Pour une liste des requêtes disponibles, reportez-vous à la section de l&#39;annexe sur les paramètres de [requête pour la récupération](./appendix.md#query)des ressources.

**Format d’API**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETER}` | L&#39;un des paramètres [de requête](./appendix.md#query) disponibles utilisés pour filtrer les résultats. |
| `{VALUE}` | Valeur du paramètre de requête précédent. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d&#39;instances MLInstances et leurs détails.

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## Récupérer une instance MLI spécifique {#retrieve-specific}

Vous pouvez récupérer les détails d&#39;une instance MLInstance spécifique en exécutant une requête GET qui inclut l&#39;ID de l&#39;instance MLInstance souhaitée dans le chemin d&#39;accès à la requête.

**Format d’API**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | ID de l’instance MLInstance souhaitée. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l&#39;instance de liste.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Mettre à jour une instance MLI

Vous pouvez mettre à jour une instance MLInstance existante en remplaçant ses propriétés par une requête PUT qui inclut l&#39;ID de l&#39;instance MLInstance de cible dans le chemin de la requête et fournit une charge utile JSON contenant des propriétés mises à jour.

>[!TIP]
>
>Afin d’assurer le succès de cette requête PUT, il est conseillé d’effectuer d’abord une requête GET pour [récupérer l’instance MLInstance par ID](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié comme charge utile pour la demande PUT.

L’exemple d’appel d’API suivant met à jour les paramètres d’identification et de notation d’une instance MLInstance lors de l’utilisation initiale de ces propriétés :

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**Format d’API**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | ID d&#39;instance MLInstance valide. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails mis à jour de l&#39;instance MLInstance.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## Supprimer les instances MLInstances par ID de moteur

Vous pouvez supprimer toutes les instances MLInstances partageant le même moteur en exécutant une requête de DELETE qui inclut l&#39;ID de moteur en tant que paramètre de requête.

**Format d’API**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | ID de moteur valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstances successfully deleted"
}
```

## Suppression d’une instance MLI

Vous pouvez supprimer une seule instance en exécutant une requête de DELETE qui inclut l&#39;identifiant de l&#39;instance de la cible dans le chemin de la requête.

**Format d’API**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | ID d&#39;instance MLInstance valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstance deletion was successful"
}
```

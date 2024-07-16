---
keywords: Experience Platform;guide de développement;point de terminaison;Data Science Workspace;rubriques les plus consultées;mlinstances;api d’apprentissage automatique sensei
solution: Experience Platform
title: Point d’entrée de l’API MLInstances
description: Une instance MLInstance correspond à l’association d’un moteur existant avec un ensemble approprié de configurations qui définit tous les paramètres de formation, paramètres de notation ou configurations de ressources matérielles.
role: Developer
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 87%

---

# Point d’entrée MLInstances

Une instance MLInstance correspond à l’association d’un [moteur](./engines.md) existant avec un ensemble approprié de configurations qui définit les paramètres de formation, les paramètres de notation ou les configurations de ressources matérielles.

## Création d’une instance MLInstance {#create-an-mlinstance}

Vous pouvez créer une instance MLInstance en effectuant une requête POST tout en fournissant un payload de requête composé d’un identifiant de moteur (`{ENGINE_ID}`) valide et d’un ensemble approprié de configurations par défaut.

Si l’identifiant de moteur référence un moteur PySpark ou Spark, vous pouvez configurer la quantité de ressources de calcul, telles que le nombre de noyaux ou la quantité de mémoire. Si un moteur Python est référencé, vous pouvez choisir d’utiliser un processeur ou un processeur graphique à des fins de formation et de notation. Pour plus d’informations, consultez les sections de l’annexe sur les [configurations des ressources PySpark et Spark](./appendix.md#resource-config) et les [configurations de processeur et de processeur graphique Python](./appendix.md#cpu-gpu-config).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Le nom souhaité pour l’instance MLInstance. Le modèle correspondant à cette instance MLInstance héritera de cette valeur afin d’être affiché dans l’interface utilisateur en tant que nom du modèle. |
| `description` | Description facultative de l’instance MLInstance. Le modèle correspondant à cette instance MLInstance héritera de cette valeur afin d’être affiché dans l’interface utilisateur en tant que description du modèle. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur comme étant une chaîne vide. |
| `engineId` | L’identifiant d’un moteur existant. |
| `tasks` | Un ensemble de configurations pour la formation, la notation ou les pipelines de fonctionnalités. |

**Réponse**

Une réponse réussie renvoie un payload contenant les détails de la nouvelle instance MLInstance, y compris son identifiant unique (`id`).

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

## Récupération d’une liste d’instances MLInstances

Vous pouvez récupérer une liste d’instances MLInstances en effectuant une seule requête GET. Pour filtrer les résultats plus facilement, vous pouvez spécifier les paramètres de requête dans le chemin d’accès de la requête. Pour obtenir une liste des requêtes disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).

**Format d’API**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETER}` | L’un des [paramètres de requête disponibles](./appendix.md#query) utilisé pour filtrer les résultats. |
| `{VALUE}` | La valeur du paramètre de requête précédent. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’instances MLInstances et leurs détails.

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

## Récupération d’une instance MLInstance spécifique {#retrieve-specific}

Vous pouvez récupérer les détails d’une instance MLInstance spécifique en effectuant une requête GET comprenant l’identifiant de l’instance MLInstance de votre choix dans le chemin de requête.

**Format d’API**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | L’identifiant de l’instance MLInstance de votre choix. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’instance MLInstance.

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

## Mise à jour d’une instance MLInstance

Vous pouvez mettre à jour une instance MLInstance existante en écrasant ses propriétés par le biais d’une requête PUT comprenant l’identifiant de l’instance MLInstance cible dans le chemin de requête et en fournissant un payload JSON contenant des propriétés mises à jour.

>[!TIP]
>
>Afin de garantir le succès de cette requête de PUT, il est conseillé d’effectuer d’abord une requête de GET pour [récupérer l’instance MLInstance par l’identifiant](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié en tant que payload de la requête PUT.

L’exemple d’appel API suivant met à jour les paramètres de formation et de notation d’une instance MLInstance lorsque les propriétés initiales sont les suivantes :

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
| `{MLINSTANCE_ID}` | Un identifiant MLInstance valide. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie un payload contenant les détails mis à jour de l’instance MLInstance.

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

## Suppression des instances MLInstances par identifiant de moteur

Vous pouvez supprimer toutes les instances MLInstances partageant le même moteur en effectuant une requête DELETE comprenant l’identifiant de moteur en tant que paramètre de requête.

**Format d’API**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | Un identifiant de moteur valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Suppression d’une instance MLInstance

Vous pouvez supprimer une seule instance MLInstance en effectuant une requête DELETE comprenant l’identifiant de l’instance MLInstance cible dans le chemin de requête.

**Format d’API**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | Un identifiant MLInstance valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

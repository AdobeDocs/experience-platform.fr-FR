---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: MLInstances
topic: Developer guide
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# MLInstances

Une instance MLInstance est une association d&#39;un [moteur](./engines.md) existant avec un ensemble approprié de configurations qui définit les paramètres d&#39;entraînement, les paramètres de notation ou les configurations de ressources matérielles.

## Création d’une instance MLI {#create-an-mlinstance}

Vous pouvez créer une instance MLInstance en exécutant une requête POST tout en fournissant une charge utile de requête composée d’un ID de moteur (`{ENGINE_ID}`) valide et d’un ensemble approprié de configurations par défaut.

Si l’ID de moteur fait référence à un moteur PySpark ou Spark, vous pouvez configurer la quantité de ressources de calcul, telles que le nombre de noyaux ou la quantité de mémoire. Si un moteur Python est référencé, vous pouvez choisir d&#39;utiliser soit un CPU, soit un GPU à des fins d&#39;entraînement et de notation. Pour plus d’informations, reportez-vous aux sections de l’annexe sur les configurations [de ressources](./appendix.md#resource-config) PySpark et Spark et les configurations [de processeur et de processeur GPU](./appendix.md#cpu-gpu-config) Python.

**Format API**

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
        "engineId": "{ENGINE_ID}",
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
| `name` | Nom souhaité pour l’instance MLInstance. Le modèle correspondant à cette instance MLInstance héritera de cette valeur pour être affiché dans l&#39;interface utilisateur comme nom du modèle. |
| `description` | Description facultative de l’instance MLInstance. Le modèle correspondant à cette instance MLInstance héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description du modèle. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `engineId` | ID d’un moteur existant. |
| `tasks` | Ensemble de configurations pour la formation, la notation ou les pipelines de fonctionnalités. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de l’instance MLInstance nouvellement créée, y compris son identifiant unique (`id`).

```json
{
    "id": "{MLINSTANCE_ID}",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "{ENGINE_ID}",
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

## Récupération d’un  d’instances MLI

Vous pouvez récupérer un d’instances de liste en exécutant une seule requête GET. Pour vous aider à filtrer les résultats, vous pouvez spécifier des paramètres  dans le chemin de requête. Pour un  de  de disponible, reportez-vous à la section de l’annexe sur les paramètres de [](./appendix.md#query)pour la récupérationdes ressources.

**Format API**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETER}` | L’un des paramètres [de ](./appendix.md#query) utilisés pour filtrer les résultats. |
| `{VALUE}` | Valeur du paramètre  de précédent. |

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

Une réponse réussie renvoie un d’instances de liste d’événements (MLInstances) et leurs détails.

```json
{
    "children": [
        {
            "id": "{MLINSTANCE_ID}",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "{ENGINE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "{MLINSTANCE_ID}",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "{ENGINE_ID}",
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

Vous pouvez récupérer les détails d’une instance MLInstance spécifique en exécutant une requête GET qui inclut l’ID de l’instance MLInstance souhaitée dans le chemin d’accès à la requête.

**Format API**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | ID de l’instance MLInstance souhaitée. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’instance d’erreur.

```json
{
    "id": "{MLINSTANCE_ID}",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "{ENGINE_ID}",
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

## Mettre à jour une instance MLInstance

Vous pouvez mettre à jour une instance MLInstance existante en écrasant ses propriétés par le biais d’une requête PUT qui inclut l’ID de l’instance MLInstance du dans le chemin d’accès à la requête et fournit une charge JSON contenant des propriétés mises à jour.

>[!TIP] Afin de garantir le succès de cette requête PUT, il est conseillé d’effectuer d’abord une requête GET pour [récupérer l’instance MLInstance par ID](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié comme charge utile pour la requête PUT.

L’exemple d’appel d’API suivant met à jour les paramètres d’identification et de notation d’une instance MLInstance lors de l’utilisation initiale des propriétés suivantes :

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

**Format API**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | ID d’instance MLInstance valide. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
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

Une réponse réussie renvoie une charge utile contenant les détails mis à jour de l’instance MIC.

```json
{
    "id": "{MLINSTANCE_ID}",
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

Vous pouvez supprimer toutes les instances MLInstances partageant le même moteur en exécutant une requête DELETE qui inclut l&#39;ID de moteur en tant que paramètre de  de.

**Format API**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | ID de moteur valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId={ENGINE_ID} \
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

## Suppression d’une instance MLInstance

Vous pouvez supprimer une instance MLInstance unique en exécutant une requête DELETE qui inclut l’ID de l’instance MLInstance du dans le chemin d’accès de la requête.

**Format API**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | ID d’instance MLInstance valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
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

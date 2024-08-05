---
keywords: Experience Platform;guide de développement;point de terminaison;Data Science Workspace;rubriques les plus consultées;expériences;api d’apprentissage automatique sensei
solution: Experience Platform
title: Point de terminaison de l’API d’expériences
description: Le développement et la formation de modèle se déroulent au niveau de l’expérience qui se compose d’une instance MLInstance ainsi que d’exécutions de formation et de notation.
role: Developer
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 86%

---

# Point d’entrée des expériences

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Le développement et la formation de modèle se déroulent au niveau de l’expérience qui se compose d’une instance MLInstance ainsi que d’exécutions de formation et de notation.

## Création d’une expérience {#create-an-experiment}

Vous pouvez créer une expérience en exécutant une requête POST tout en fournissant un nom et un identifiant d’instance MLInstance valide dans le payload de la requête.

>[!NOTE]
>
>Contrairement à la formation de modèle dans l’interface utilisateur, la création d’une expérience par le biais d’un appel API explicite ne crée pas et n’exécute pas de formation automatiquement.

**Format d’API**

```http
POST /experiments
```

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Le nom de votre choix pour l’expérience. L’exécution de formation correspondant à cette expérience hérite de cette valeur qui s’affiche dans l’interface utilisateur en tant que nom de l’exécution de formation. |
| `mlInstanceId` | Un identifiant MLInstance valide. |

**Réponse**

Une réponse réussie renvoie un payload contenant les détails de l’expérience que vous venez de créer, y compris son identifiant unique (`id`).

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Création et exécution d’une exécution de formation ou de notation {#experiment-training-scoring}

Vous pouvez créer des exécutions de formation ou de notation en exécutant une requête POST ainsi qu’en fournissant un identifiant d’expérience valide et en spécifiant la tâche d’exécution. Les exécutions de notation ne peuvent être créées que si elles sont associées à une exécution de formation réussie. La création réussie d’une exécution de formation initie la procédure de formation du modèle, tandis que son achèvement réussi génère un modèle formé. La génération de modèles formés remplace les modèles qui existaient auparavant, de sorte qu’une expérience ne peut utiliser qu’un seul modèle formé à un moment donné.

**Format d’API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | Un identifiant d’expérience valide. |

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Propriété | Description |
| --- | --- |
| `{TASK}` | Spécifie la tâche de l’exécution. Définissez la valeur `train` pour la formation, `score` pour la notation ou `featurePipeline` pour le pipeline de fonctionnalités. |

**Réponse**

Une réponse réussie renvoie un payload contenant les détails de l’exécution qui vient d’être créée, y compris les paramètres de formation ou d’évaluation par défaut hérités et l’ID unique de l’exécution (`{RUN_ID}`).

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Récupération d’une liste d’expériences

Vous pouvez obtenir une liste des expériences associées à une instance MLInstance spécifique en exécutant une seule requête GET et en fournissant un identifiant MLInstance valide en tant que paramètre de la requête. Pour obtenir une liste des requêtes disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).


**Format d’API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | Fournissez un identifiant d’instance MLInstance valide pour récupérer une liste des expériences associées à cette instance MLInstance spécifique. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’expériences partageant le même identifiant d’instance MLInstance (`{MLINSTANCE_ID}`).

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## Récupération d’une expérience spécifique {#retrieve-specific}

Vous pouvez récupérer les détails d’une expérience spécifique en exécutant une requête GET incluant l’identifiant de l’expérience souhaitée dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | Un identifiant d’expérience valide. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails de l’expérience interrogée.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Récupération d’une liste d’exécutions d’expérience

Vous pouvez obtenir une liste des exécutions de formation ou de notation associées à une expérience spécifique en exécutant une seule requête GET et en fournissant un identifiant d’expérience valide. Pour filtrer les résultats plus facilement, vous pouvez spécifier les paramètres de requête dans le chemin d’accès de la requête. Pour obtenir la liste complète des paramètres de requête disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).

>[!NOTE]
>
>Lorsque vous combinez plusieurs paramètres de requête, ceux-ci doivent être séparés par des esperluettes (&amp;).

**Format d’API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | Un identifiant d’expérience valide. |
| `{QUERY_PARAMETER}` | L’un des [paramètres de requête disponibles](./appendix.md#query) utilisés pour filtrer les résultats. |
| `{VALUE}` | La valeur du paramètre de requête précédent. |

**Requête**

La requête suivante contient une requête et renvoie une liste d’exécutions de formation associées à une expérience.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant une liste d’exécutions et les détails de chacune d’elles, y compris leur identifiant d’exécution d’expérience (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Mise à jour d’une expérience

Vous pouvez mettre à jour une expérience existante en écrasant ses propriétés par le biais d’une requête PUT qui inclut l’identifiant de l’expérience cible dans le chemin d’accès de la requête et en fournissant un payload JSON contenant des propriétés mises à jour.

>[!TIP]
>
>Afin de garantir le succès de cette requête de PUT, il est conseillé d’effectuer d’abord une requête de GET pour [récupérer l’expérience par l’identifiant](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié en tant que payload de la requête PUT.

L’exemple d’appel API suivant met à jour le nom d’une expérience lorsque les propriétés initiales sont les suivantes :

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**Format d’API**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | Un identifiant d’expérience valide. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails mis à jour de l’expérience.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Suppression d’une expérience

Vous pouvez supprimer une seule expérience en exécutant une requête DELETE incluant l’identifiant de l’expérience cible dans le chemin d’accès de la requête.

**Format d’API**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | Un identifiant d’expérience valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
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
    "detail": "Experiment successfully deleted"
}
```

## Suppression d’expériences par identifiant d’instance MLInstance

Vous pouvez supprimer toutes les expériences associées à une instance MLInstance spécifique en exécutant une requête DELETE incluant l’identifiant d’instance MLInstance en tant que paramètre de la requête.

**Format d’API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | ---|
| `{MLINSTANCE_ID}` | Un identifiant MLInstance valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "Experiments successfully deleted"
}
```

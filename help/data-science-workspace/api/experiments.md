---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Expériences
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 4%

---


# Expériences

Le développement et la formation de modèles se déroulent au niveau Expérience, où une Expérience se compose d’une instance de la MLI, de sessions de formation et d’exécutions de notation.

## Création d’une expérience {#create-an-experiment}

Vous pouvez créer une expérience en exécutant une requête POST tout en fournissant un nom et un ID d&#39;instance MLInstance valide dans la charge utile de la requête.

>[!NOTE]
>
>Contrairement à la formation de modèle dans l’interface utilisateur, la création d’une expérience par le biais d’un appel d’API explicite ne crée pas et n’exécute pas automatiquement une session de formation.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de l’expérience souhaité. L&#39;exécution de formation correspondant à cette expérience hérite de cette valeur à afficher dans l&#39;interface utilisateur comme nom de l&#39;exécution de formation. |
| `mlInstanceId` | ID d&#39;instance MLInstance valide. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de l&#39;expérience nouvellement créée, y compris son identifiant unique (`id`).

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

## Créer et exécuter une formation ou une série de notation {#experiment-training-scoring}

Vous pouvez créer des exécutions de formation ou de notation en exécutant une requête POST et en fournissant un ID d’expérience valide et en spécifiant la tâche d’exécution. Les exécutions de score ne peuvent être créées que si l’expérience a une exécution de formation existante et réussie. La création réussie d&#39;un cycle de formation initialise la procédure de formation du modèle et sa réussite génère un modèle formé. La création de modèles formés remplacera ceux qui existaient déjà, de sorte qu&#39;une expérience ne peut utiliser qu&#39;un seul modèle formé à un moment donné.

**Format d’API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Propriété | Description |
| --- | --- |
| `{TASK}` | Indique la tâche de l’exécution. Définissez cette valeur comme `train` pour la formation, `score` pour la notation ou `featurePipeline` pour le pipeline de fonctionnalités. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de l&#39;exécution nouvellement créée, y compris les paramètres de formation ou d&#39;évaluation par défaut hérités et l&#39;identifiant unique de l&#39;exécution (`{RUN_ID}`).

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

## Récupérer une liste d&#39;expériences

Vous pouvez récupérer une liste d&#39;expériences appartenant à une instance MLInstance particulière en exécutant une seule requête GET et en fournissant un ID MLInstance valide en tant que paramètre de requête. Pour une liste des requêtes disponibles, reportez-vous à la section de l&#39;annexe sur les paramètres de [requête pour la récupération](./appendix.md#query)des ressources.


**Format d’API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | Fournissez un ID d&#39;instance de liste de mesure valide pour récupérer une liste d&#39;expériences appartenant à cette instance particulière. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’expériences partageant le même ID d’instance de la liste (`{MLINSTANCE_ID}`).

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

## Récupérer une expérience spécifique {#retrieve-specific}

Vous pouvez récupérer les détails d’une expérience spécifique en exécutant une requête GET qui inclut l’ID de l’expérience souhaitée dans le chemin de la requête.

**Format d’API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de l&#39;expérience demandée.

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

Vous pouvez récupérer une liste d’exécutions de formation ou de notation appartenant à une expérience particulière en exécutant une seule demande GET et en fournissant un ID d’expérience valide. Pour faciliter le filtrage des résultats, vous pouvez spécifier des paramètres de requête dans le chemin d’accès à la requête. Pour une liste complète des paramètres de requête disponibles, voir la section de l&#39;annexe sur les paramètres de [requête pour la récupération](./appendix.md#query)des ressources.

>[!NOTE]
>
>Lors de la combinaison de plusieurs paramètres de requête, ils doivent être séparés par des esperluettes (&amp;).

**Format d’API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |
| `{QUERY_PARAMETER}` | L&#39;un des paramètres [de requête](./appendix.md#query) disponibles utilisés pour filtrer les résultats. |
| `{VALUE}` | Valeur du paramètre de requête précédent. |

**Requête**

La requête suivante contient une requête et récupère une liste d&#39;exécutions de formation appartenant à une expérience.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant une liste d&#39;exécutions et chacun de leurs détails, y compris leur ID d&#39;exécution d&#39;expérience (`{RUN_ID}`).

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

## Mettre à jour une expérience

Vous pouvez mettre à jour une expérience existante en remplaçant ses propriétés par une requête PUT qui inclut l’ID de l’expérience de cible dans le chemin de la requête et fournit une charge utile JSON contenant des propriétés mises à jour.

>[!TIP]
>
>Afin d’assurer le succès de cette requête PUT, il est conseillé d’effectuer d’abord une requête GET pour [récupérer l’expérience par ID](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié comme charge utile pour la demande PUT.

L’exemple d’appel d’API suivant met à jour le nom d’une expérience alors que ces propriétés étaient au départ les suivantes :

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
| `{EXPERIMENT_ID}` | ID d’expérience valide. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Une réponse réussie renvoie une charge utile contenant les détails mis à jour de l’expérience.

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

Vous pouvez supprimer une seule expérience en exécutant une requête de DELETE qui inclut l’ID de l’expérience de cible dans le chemin de la requête.

**Format d’API**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
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
    "detail": "Experiment successfully deleted"
}
```

## Supprimer des expériences par ID d&#39;instance de liste

Vous pouvez supprimer toutes les expériences appartenant à une instance MLInstance particulière en exécutant une demande de DELETE qui inclut l&#39;ID MLInstance en tant que paramètre de requête.

**Format d’API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | ---|
| `{MLINSTANCE_ID}` | ID d&#39;instance MLInstance valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "Experiments successfully deleted"
}
```

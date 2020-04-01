---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Expériences
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Expériences

Le développement et la formation du modèle se déroulent au niveau de l’expérience, où une expérience se compose d’une instance de l’IMC, d’exécutions de formation et d’exécutions de notation.

## Création d’une expérience

Vous pouvez créer une expérience en exécutant une requête POST tout en fournissant un nom et un ID d’instance MLInstance valide dans la charge utile de la requête.

>[!NOTE] Contrairement à la formation de modèle dans l’interface utilisateur, la création d’une expérience par le biais d’un appel d’API explicite ne crée pas et n’exécute pas automatiquement une session de formation.

**Format API**

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
        "mlInstanceId": "{MLINSTANCE_ID}"
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom souhaité pour l’expérience. L’exécution de formation correspondant à cette expérience héritera de cette valeur à afficher dans l’interface utilisateur comme nom de l’exécution de formation. |
| `mlInstanceId` | ID d’instance MLInstance valide. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de l’expérience nouvellement créée, y compris son identifiant unique (`id`).

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Création et exécution d’une session de formation ou de notation

Vous pouvez créer des exécutions de formation ou de notation en exécutant une requête POST et en fournissant un ID d’expérience valide et en spécifiant le  d’exécution. Les exécutions de score ne peuvent être créées que si l’expérience a une exécution de formation existante et réussie. La création réussie d&#39;une session de formation initiera la procédure d&#39;entraînement du modèle et son achèvement réussi générera un modèle formé. La création de modèles formés remplacera ceux qui existaient auparavant, de sorte qu’une expérience ne puisse utiliser qu’un seul modèle formé à un moment donné.

**Format API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
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
| `{TASK}` | Indique le  de l’exécution. Définissez cette valeur comme `train` pour la formation, `score` pour la notation ou `fp` pour le pipeline de fonctionnalités. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de l’exécution nouvellement créée, y compris les paramètres de formation ou d’évaluation par défaut hérités et l’identifiant unique de l’exécution (`{RUN_ID}`).

```json
{
    "id": "{RUN_ID}",
    "mode": "{TASK}",
    "experimentId": "{EXPERIMENT_ID}",
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

## Récupérer un d&#39;expériences

Vous pouvez récupérer un d’expériences appartenant à une instance MLInstance particulière en exécutant une seule requête GET et en fournissant un ID d’instance MLInstance valide en tant que paramètre . Pour un  de  de disponible, reportez-vous à la section de l’annexe sur les paramètres de [](./appendix.md#query)pour la récupérationdes ressources.


**Format API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | Fournissez un ID d’instance MLInstance valide pour récupérer un d’expériences appartenant à cette instance MLInstance particulière. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId=={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une  d’expériences partageant le même ID d’instance (`{MLINSTANCE_ID}`).

```json
{
    "children": [
        {
            "id": "{EXPERIMENT_ID}",
            "name": "A name for this Experiment",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 1",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 2",
            "mlInstanceId": "{MLINSTANCE_ID}",
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

Vous pouvez récupérer les détails d’une expérience spécifique en exécutant une requête GET qui inclut l’ID de l’expérience souhaitée dans le chemin d’accès de la requête.

**Format API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```


**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de l’expérience demandée.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Récupération d’un d’exécutions d’expérience

Vous pouvez récupérer un d’exécutions de formation ou de notation appartenant à une expérience spécifique en exécutant une seule requête GET et en fournissant un ID d’expérience valide. Pour vous aider à filtrer les résultats, vous pouvez spécifier des paramètres  dans le chemin de requête. Pour un complet des paramètres de  disponibles, reportez-vous à la section de l’annexe sur les paramètres de [](./appendix.md#query)pour la récupérationdes ressources.

>[!NOTE] Lorsque vous combinez plusieurs paramètres de , ils doivent être séparés par des esperluettes (&amp;).

**Format API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |
| `{QUERY_PARAMETER}` | L’un des paramètres [de ](./appendix.md#query) utilisés pour filtrer les résultats. |
| `{VALUE}` | Valeur du paramètre  de précédent. |

**Requête**

La requête suivante contient un  et récupère un de pistes de formation appartenant à une expérience.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant un  d’exécutions et chacun de leurs détails, y compris leur ID d’exécution d’expérience (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "{RUN_ID}",
            "mode": "train",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId=={EXPERIMENT_ID},deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Mettre à jour une expérience

Vous pouvez mettre à jour une expérience existante en écrasant ses propriétés par le biais d’une requête PUT qui inclut l’ID de l’expérience de  dans le chemin d’accès à la requête et fournit une charge JSON contenant des propriétés mises à jour.

>[!TIP] Afin d’assurer le succès de cette requête PUT, il est conseillé d’effectuer d’abord une requête GET pour [récupérer l’expérience par ID](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié comme charge utile pour la requête PUT.

L’exemple d’appel d’API suivant met à jour le nom d’une expérience alors que ces propriétés étaient au départ :

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**Format API**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "{MLINSTANCE_ID}",
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
    "id": "{EXPERIMENT_ID}",
    "name": "An updated name",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Suppression d’une expérience

Vous pouvez supprimer une expérience unique en exécutant une requête DELETE qui inclut l’ID de l’expérience de  dans le chemin de la requête.

**Format API**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPERIMENT_ID}` | ID d’expérience valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
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

## Supprimer les expériences par ID d&#39;instance de liste

Vous pouvez supprimer toutes les expériences appartenant à une instance MLInstance particulière en exécutant une requête DELETE qui inclut l’ID MLInstance en tant que paramètre .

**Format API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | ---|
| `{MLINSTANCE_ID}` | ID d’instance MLInstance valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId={MLINSTANCE_ID} \
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

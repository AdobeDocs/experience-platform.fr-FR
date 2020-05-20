---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: Formation et évaluation d’un modèle (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 1%

---


# Formation et évaluation d’un modèle (API)


Ce didacticiel vous montre comment créer, former et évaluer un modèle à l&#39;aide d&#39;appels d&#39;API. Reportez-vous à [ce document](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) pour obtenir une liste détaillée de la documentation de l’API.

## Conditions préalables

Suivez la procédure [Importer une recette empaquetée à l&#39;aide de l&#39;API](./import-packaged-recipe-api.md) pour créer un moteur, qui est nécessaire pour former et évaluer un modèle à l&#39;aide de l&#39;API.

Suivez ce [didacticiel](../../tutorials/authentication.md) pour obtenir l’autorisation d’effectuer des appels d’API par début.

Dans le didacticiel, vous devez maintenant avoir les valeurs suivantes :

- `{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.
- `{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.

- Lien vers une image de Docker d&#39;un service intelligent

## Processus des API

Nous allons utiliser les API pour créer une exécution d’expérience pour la formation. Pour ce didacticiel, nous nous concentrerons sur les points de terminaison **Moteurs**, **MLInstances** et **Experiments** . Le graphique suivant présente la relation entre les trois et présente également l&#39;idée d&#39;un Run et d&#39;un Model.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE] Les termes &quot;Moteur&quot;, &quot;Instance&quot;, &quot;MLService&quot;, &quot;Expérience&quot; et &quot;Modèle&quot; sont appelés termes différents dans l’interface utilisateur. Si vous venez de l’interface utilisateur, le tableau suivant fera correspondre les différences.
> 
> | Terme de l’interface utilisateur | Terme de l’API |
> --- | ---
> | Recette | Moteur |
> | Modèle | Instance MLI |
> | Cours de formation | Expérience |
> | Service | MLService |



### Création d’une instance MLI

La création d&#39;une instance MLInstance peut être effectuée à l&#39;aide de la requête suivante. Vous utiliserez le `{ENGINE_ID}` qui a été renvoyé lors de la création d&#39;un moteur à partir du didacticiel [Importer une recette empaquetée à l&#39;aide du didacticiel API](./import-packaged-recipe-ui.md) .

**Requête**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.\
`{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}`: La configuration de notre instance MLInstance. L’exemple que nous utilisons dans notre didacticiel est illustré ci-dessous :

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE] Dans le `{JSON_PAYLOAD}`tableau, nous définissons les paramètres utilisés pour la formation et le score dans la `tasks` baie. L&#39;ID `{ENGINE_ID}` est celui du moteur que vous souhaitez utiliser et le `tag` champ est un paramètre facultatif utilisé pour identifier l&#39;instance.

La réponse contiendra le `{INSTANCE_ID}` qui représente l&#39;instance MLInstance créée. Il est possible de créer plusieurs instances MLInstances de modèles avec des configurations différentes.

**Réponse**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`: Cet identifiant représente le moteur sous lequel l&#39;instance MLInstance est créée.\
`{INSTANCE_ID}`: ID qui représente l&#39;instance MLInstance.

### Création d’une expérience

Une expérience est utilisée par un chercheur en données pour obtenir un modèle hautement performant pendant la formation. Plusieurs expériences incluent la modification de jeux de données, de fonctionnalités, de paramètres d’apprentissage et de matériel. Voici un exemple de création d’une expérience.

**Requête**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Objet d’expérience créé. L’exemple que nous utilisons dans notre didacticiel est illustré ci-dessous :

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: ID qui représente l&#39;instance MLInstance.

La réponse de la création de l’expérience ressemble à ceci.

**Réponse**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`: ID représentant l’expérience que vous venez de créer.
`{INSTANCE_ID}`: ID qui représente l&#39;instance MLInstance.

### Créer une expérience planifiée pour la formation

Les expériences planifiées sont utilisées de sorte que nous n’ayons pas à créer chaque exécution d’expérience unique au moyen d’un appel d’API. Au lieu de cela, nous fournissons tous les paramètres nécessaires lors de la création de l&#39;expérience et chaque exécution sera créée périodiquement.

Pour indiquer la création d’une expérience planifiée, nous devons ajouter une `template` section dans le corps de la requête. En `template`effet, tous les paramètres nécessaires pour la planification des exécutions sont inclus, par exemple `tasks`, qui indiquent quelle action et `schedule`, qui indiquent le timing des exécutions planifiées.

**Requête**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Données à publier. L’exemple que nous utilisons dans notre didacticiel est illustré ci-dessous :

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

Lors de la création d’une expérience, le corps, `{JSON_PAYLOAD}`doit contenir le `mlInstanceId` ou le `mlInstanceQuery` paramètre. Dans cet exemple, une expérience planifiée appelle une exécution toutes les 20 minutes, définie dans le `cron` paramètre, à partir du `startTime` jusqu’au `endTime`.

**Réponse**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`: ID représentant l’expérience.\
`{INSTANCE_ID}`: ID qui représente l&#39;instance MLInstance.


### Création d’une exécution d’expérience pour la formation

Une entité Expérience créée permet de créer et d&#39;exécuter une session de formation à l&#39;aide de l&#39;appel ci-dessous. Vous aurez besoin de la `{EXPERIMENT_ID}` et indiquez ce que `mode` vous souhaitez déclencher dans le corps de la requête.

**Requête**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: ID correspondant à l’expérience que vous souhaitez cible. Cela se trouve dans la réponse lors de la création de votre expérience.\
`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Pour créer une session de formation, vous devez inclure les éléments suivants dans le corps :

```JSON
{
    "mode":"Train"
}
```

Vous pouvez également remplacer les paramètres de configuration en incluant un `tasks` tableau :

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

Vous recevrez la réponse suivante qui vous fera connaître la configuration `{EXPERIMENT_RUN_ID}` et la configuration sous `tasks`.

**Réponse**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`:  ID représentant l’exécution de l’expérience.\
`{EXPERIMENT_ID}`: ID qui représente l&#39;expérience sous laquelle se trouve l&#39;exécution de l&#39;expérience.

### Récupérer un état d&#39;exécution d&#39;expérience

L’état de l’exécution Expérience peut être interrogé avec le `{EXPERIMENT_RUN_ID}`.

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: ID représentant l’expérience.\
`{EXPERIMENT_RUN_ID}`: ID représentant l’exécution de l’expérience.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.\
`{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.

**Réponse**

L’appel GET fournit l’état dans le `state` paramètre, comme indiqué ci-dessous :

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`:  ID représentant l’exécution de l’expérience.\
`{EXPERIMENT_ID}`: ID qui représente l&#39;expérience sous laquelle se trouve l&#39;exécution de l&#39;expérience.

Outre l&#39; `DONE` État, d&#39;autres États comprennent :
- `PENDING`
- `RUNNING`
- `FAILED`

Pour plus d&#39;informations, les journaux détaillés se trouvent sous le `tasklogs` paramètre.

### Récupérer le modèle formé

Pour obtenir le modèle de formation créé ci-dessus pendant la formation, nous faisons la demande suivante :

**Requête**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`: ID correspondant à l’exécution d’expérience que vous souhaitez cible. Cela se trouve dans la réponse lors de la création de votre exécution d’expérience.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.

La réponse représente le modèle formé qui a été créé.

**Réponse**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`: ID correspondant au modèle.\
`{EXPERIMENT_ID}`:  L&#39;ID correspondant à l&#39;expérience que l&#39;exécution d&#39;expérience est sous.\
`{EXPERIMENT_RUN_ID}`: ID correspondant à l’exécution de l’expérience.

### Arrêter et supprimer une expérience planifiée

Si vous souhaitez interrompre l&#39;exécution d&#39;une expérience planifiée avant son `endTime`exécution, vous pouvez demander une requête DELETE à la variable `{EXPERIMENT_ID}`

**Requête**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  ID correspondant à l’expérience.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.

>[!NOTE] L&#39;appel d&#39;API désactivera la création de nouvelles exécutions d&#39;expérience. Cependant, il n’arrêtera pas l’exécution des exécutions d’expériences déjà en cours d’exécution.

Voici la réponse vous informant que l&#39;expérience a bien été supprimée.

**Réponse**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Étapes suivantes

Ce didacticiel explique comment utiliser les API pour créer un moteur, une expérience, des exécutions d’expériences planifiées et des modèles formés. Au cours du [prochain exercice](./score-model-api.md), vous allez faire des prédictions en évaluant un nouveau jeu de données à l’aide du modèle de formation le plus performant.
---
keywords: Experience Platform;former et évaluer;Workspace de science des données;rubriques populaires;API Sensei Machine Learning
solution: Experience Platform
title: Entraînement et évaluation d’un modèle à l’aide de l’API Sensei Machine Learning
type: Tutorial
description: Ce tutoriel vous explique comment créer, entraîner et évaluer un modèle à l’aide d’appels API de machine learning Sensei.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 79%

---

# Entraînement et évaluation d’un modèle à l’aide de l’API [!DNL Sensei Machine Learning]

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Ce tutoriel vous explique comment créer, former et évaluer un modèle à l’aide d’appels API. Reportez-vous à [ce document](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) pour obtenir une liste détaillée de la documentation sur les API.

## Conditions préalables

Suivez la procédure [Importer une recette empaquetée à l’aide de l’API](./import-packaged-recipe-api.md) pour créer un moteur, ce qui est nécessaire pour former et évaluer un modèle à l’aide de l’API.

Suivez le tutoriel [Authentification de l’API Experience Platform &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour commencer à effectuer des appels API.

Grâce au tutoriel, vous devez maintenant disposer des valeurs suivantes :

- `{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.
- `{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.

- Lien vers une image Docker d’un service intelligent

## Workflow API

Nous utiliserons les API pour créer une exécution d’expérience pour la formation. Pour ce tutoriel, nous nous concentrerons sur les points d’entrée Moteurs, MLInstances et Expériences . Le graphique suivant décrit la relation entre les trois points et présente également la notion d’exécution et de modèle.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>Les termes « Moteur », « MLInstance », « MLService », « Expérience » et « Modèle » sont appelés différents dans l’interface utilisateur. Si vous venez de l’interface utilisateur de , le tableau suivant met en correspondance les différences.

| Terme de l’interface utilisateur | Terme de l’API |
| --- | --- |
| Recette | Engine |
| Modèle | MLInstance |
| Exécutions de formation | Experiment |
| Service | MLService |

### Création d’une instance MLInstance

Vous pouvez créer une MLInstance à l’aide de la requête suivante. Vous utiliserez le `{ENGINE_ID}` renvoyé lors de la création d’un moteur à partir du tutoriel [Importer une recette empaquetée à l’aide de l’API](./import-packaged-recipe-ui.md).

**Requête**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}` : la configuration de notre MLInstance. Voici l’exemple utilisé dans notre tutoriel :

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

>[!NOTE]
>
>Dans la `{JSON_PAYLOAD}`, nous définissons les paramètres utilisés pour l’entraînement et la notation dans le tableau de `tasks`. `{ENGINE_ID}` représente l’identifiant du moteur que vous souhaitez utiliser et le champ `tag` est un paramètre facultatif utilisé pour identifier l’instance.

La réponse contient le `{INSTANCE_ID}` qui représente l’instance MLI créée. Vous pouvez créer plusieurs MLInstances de modèle avec des configurations différentes.

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

`{ENGINE_ID}` : cet identifiant représente le moteur sous lequel l’instance MLInstance est créée.\
`{INSTANCE_ID}` : identifiant qui représente l’instance MLInstance.

### Création d’une expérience

Une expérience est utilisée par un analyste de données pour obtenir un modèle hautement performant pendant la formation. Plusieurs expériences incluent la modification des jeux de données, des fonctionnalités, des paramètres de formation et du matériel. Voici un exemple de création d’une expérience.

**Requête**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}` : objet d’expérience créé. Voici l’exemple utilisé dans notre tutoriel :

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}` : identifiant qui représente l’instance MLInstance.

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

`{EXPERIMENT_ID}` : identifiant qui représente l’expérience que vous venez de créer. `{INSTANCE_ID}` : identifiant qui représente l’instance MLInstance.

### Création d’une expérience planifiée pour la formation

Les expériences planifiées sont utilisées de sorte que nous n’ayons pas besoin de créer chaque exécution d’expérience par le biais d’un appel API. Au lieu de cela, nous fournissons tous les paramètres nécessaires lors de la création de l’expérience et chaque exécution sera créée périodiquement.

Pour indiquer la création d’une expérience planifiée, nous devons ajouter une section `template` dans le corps de la requête. Dans `template`, tous les paramètres nécessaires à la planification des exécutions sont inclus, par exemple `tasks`, qui indique les actions et `schedule`, qui indique le timing des exécutions planifiées.

**Requête**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}` : données à publier. Voici l’exemple utilisé dans notre tutoriel :

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

Lorsque nous créons une expérience, le corps, `{JSON_PAYLOAD}`, doit contenir le paramètre `mlInstanceId` ou `mlInstanceQuery`. Dans cet exemple, une expérience planifiée appelle une exécution toutes les 20 minutes, définie dans le paramètre `cron`, à partir de `startTime` jusqu’au `endTime`.

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

`{EXPERIMENT_ID}` : identifiant qui représente l’expérience.\
`{INSTANCE_ID}` : identifiant qui représente l’instance MLInstance.


### Création d’une exécution d’expérience pour la formation

Une fois une entité d’expérience créée, une exécution de formation peut être créée et exécutée en utilisant l’appel ci-dessous. Vous aurez besoin de `{EXPERIMENT_ID}` et devrez indiquer le `mode` que vous souhaitez déclencher dans le corps de la requête.

**Requête**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience que vous souhaitez cibler. Vous pouvez le trouver dans la réponse lors de la création de votre expérience.\
`{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}` : pour créer une exécution de formation, vous devez inclure les éléments suivants dans le corps :

```JSON
{
    "mode":"Train"
}
```

Vous pouvez également remplacer les paramètres de configuration en incluant un tableau `tasks` :

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

Vous obtiendrez la réponse suivante qui vous indiquera le `{EXPERIMENT_RUN_ID}` et la configuration sous `tasks`.

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

`{EXPERIMENT_RUN_ID}` : identifiant qui représente l’exécution de l’expérience.\
`{EXPERIMENT_ID}` : identifiant qui représente l’expérience sous laquelle se trouve l’exécution d’expérience.

### Récupération de l’état d’une exécution d’expérience

L’état de l’exécution d’expérience peut être interrogé avec le `{EXPERIMENT_RUN_ID}`.

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}` : identifiant qui représente l’expérience.\
`{EXPERIMENT_RUN_ID}` : identifiant qui représente l’exécution de l’expérience.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.

**Réponse**

L’appel GET fournit l’état dans le paramètre `state`, comme illustré ci-dessous :

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

`{EXPERIMENT_RUN_ID}` : identifiant qui représente l’exécution de l’expérience.\
`{EXPERIMENT_ID}` : identifiant qui représente l’expérience sous laquelle se trouve l’exécution d’expérience.

Outre l’état `DONE`, les autres états incluent :
- `PENDING`
- `RUNNING`
- `FAILED`

Pour plus d’informations, les journaux détaillés se trouvent sous le paramètre `tasklogs`.

### Récupération du modèle formé

Pour obtenir le modèle formé créé ci-dessus pendant la formation, nous faisons la demande suivante :

**Requête**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}` : identifiant qui correspond à l’exécution d’expérience que vous souhaitez cibler. Vous pouvez le trouver dans la réponse lors de la création de votre exécution d’expérience.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.

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

`{MODEL_ID}` : identifiant qui correspond au modèle.\
`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience sous laquelle se trouve l’exécution d’expérience.\
`{EXPERIMENT_RUN_ID}` : identifiant qui correspond à l’expérience d’exécution.

### Arrêt et suppression d’une expérience planifiée

Si vous souhaitez arrêter l’exécution d’une expérience planifiée avant son `endTime`, vous pouvez faire une requête DELETE à l’`{EXPERIMENT_ID}`.

**Requête**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.

>[!NOTE]
>
>L’appel API désactive la création de nouvelles exécutions d’expérience. Toutefois, il n’arrête pas les exécutions d’expériences déjà en cours.

Voici la réponse qui indique que l’expérience a bien été supprimée.

**Réponse**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Étapes suivantes

Ce tutoriel explique comment utiliser les API pour créer un moteur, une expérience, des exécutions d’expériences planifiées et des modèles formés. Au cours de l’[exercice suivant](./score-model-api.md), vous allez faire des prédictions en évaluant un nouveau jeu de données à l’aide du modèle formé le plus performant.

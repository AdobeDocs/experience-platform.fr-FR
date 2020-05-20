---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Score d’un modèle (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---


# Score d’un modèle (API)

Ce didacticiel vous montrera comment exploiter les API pour créer une expérience et une exécution d’expérience. Pour obtenir une liste détaillée de la documentation de l&#39;API, veuillez consulter [ce document](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html).

## Créer une expérience planifiée pour la notation

Comme pour les expériences planifiées pour la formation, la création d’une expérience planifiée pour la notation est également effectuée en incluant une `template` section au paramètre body. De plus, le `name` champ sous `tasks` dans le corps est défini comme `score`.

Vous trouverez ci-dessous un exemple de création d’une expérience qui s’exécutera toutes les 20 minutes à partir de `startTime` et jusqu’à `endTime`laquelle elle sera exécutée.

**Requête**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Objet d&#39;exécution d&#39;expérience à envoyer. L’exemple que nous utilisons dans notre didacticiel est illustré ci-dessous :

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`: ID qui représente l&#39;instance MLInstance.\
`{MODEL_ID}`: ID qui représente le modèle formé.

Voici la réponse après la création de l’expérience planifiée.

**Réponse**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`: ID représentant l’expérience.\
`{INSTANCE_ID}`: ID qui représente l&#39;instance MLInstance.


### Création d’une exécution d’expérience pour la notation

Maintenant, avec le modèle entraîné, nous pouvons créer une exécution d’expérience pour la notation. La valeur du `modelId` paramètre est le `id` paramètre renvoyé dans la demande de modèle GET ci-dessus.

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

`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{EXPERIMENT_ID}`: ID correspondant à l’expérience que vous souhaitez cible. Cela se trouve dans la réponse lors de la création de votre expérience.\
`{JSON_PAYLOAD}`: Données à publier. L’exemple que nous utilisons dans notre didacticiel est le suivant :

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`: ID correspondant au modèle.

La réponse issue de la création de l’exécution d’expérience est illustrée ci-dessous :

**Réponse**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`:  ID correspondant à l&#39;expérience sous laquelle l&#39;exécution est exécutée.\
`{EXPERIMENT_RUN_ID}`: ID correspondant à l’exécution d’expérience que vous venez de créer.


### Récupérer un état d&#39;exécution d&#39;expérience pour l&#39;exécution d&#39;expérience planifiée

Pour obtenir des exécutions d’expériences pour des expériences planifiées, la requête est présentée ci-dessous :

**Requête**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  ID correspondant à l&#39;expérience sous laquelle l&#39;exécution est exécutée.\
`{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.

Comme il existe plusieurs exécutions d’expériences pour une expérience spécifique, la réponse renvoyée comporte un tableau d’ID d’exécution.

**Réponse**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: ID correspondant à l’exécution de l’expérience.\
`{EXPERIMENT_ID}`:  ID correspondant à l&#39;expérience sous laquelle l&#39;exécution est exécutée.

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

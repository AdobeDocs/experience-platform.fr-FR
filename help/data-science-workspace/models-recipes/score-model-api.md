---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics;sensei machine learning api
solution: Experience Platform
title: Notation d’un modèle (API)
topic: tutorial
type: Tutorial
description: Ce didacticiel vous montrera comment tirer parti des API d'apprentissage automatique Sensei pour créer une expérience et une exécution d'expérience.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 96%

---


# Notation d’un modèle (API)

Ce tutoriel explique comment utiliser les API pour créer une expérience et une exécution d’expérience. Pour une liste détaillée de la documentation sur les API, voir [ce document](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html).

## Création d’une expérience planifiée pour la notation

Comme pour les expériences planifiées pour la formation, la création d’une expérience planifiée pour la notation est également effectuée en ajoutant une section `template` au paramètre du corps. De plus, le champ `name` sous `tasks` dans le corps est défini sur `score`.

Vous trouverez ci-dessous un exemple de création d’une expérience qui s’exécutera toutes les 20 minutes entre `startTime` et `endTime`.

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

`{IMS_ORG}` : vos informations d’identification d’organisation IMS, qui se trouvent dans votre intégration unique d’Adobe Experience Platform.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{JSON_PAYLOAD}` : objet d’exécution d’expérience à envoyer. Voici l’exemple utilisé dans notre tutoriel :

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

`{INSTANCE_ID}` : identifiant qui représente l’instance MLInstance.\
`{MODEL_ID}` : identifiant qui représente le modèle formé.

Voici la réponse après avoir créé l’expérience planifiée.

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

`{EXPERIMENT_ID}` : identifiant qui représente l’expérience.\
`{INSTANCE_ID}` : identifiant qui représente l’instance MLInstance.


### Création d’une exécution d’expérience pour la notation

Une fois le modèle formé, il est possible de créer une exécution d’expérience pour la notation. La valeur du paramètre `modelId` est le paramètre `id` renvoyé dans la requête de modèle GET ci-dessus.

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

`{IMS_ORG}` : vos informations d’identification d’organisation IMS, qui se trouvent dans votre intégration unique d’Adobe Experience Platform.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.\
`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience que vous souhaitez cibler. Vous pouvez le trouver dans la réponse lors de la création de votre expérience.\
`{JSON_PAYLOAD}` : données à publier. Voici l’exemple utilisé dans notre tutoriel :

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

`{MODEL_ID}` : identifiant qui correspond au modèle.

Voici la réponse de la création de l’exécution d’expérience :

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

`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience sous laquelle se trouve l’exécution.\
`{EXPERIMENT_RUN_ID}` : identifiant qui correspond à l’exécution d’expérience que vous venez de créer.


### Récupération d’un état d’exécution d’expérience pour une exécution d’expérience planifiée

Voici la requête qui permet d’obtenir des exécutions d’expérience pour les expériences planifiées :

**Requête**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience sous laquelle se trouve l’exécution.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{IMS_ORG}` : vos informations d’identification d’organisation IMS, qui se trouvent dans votre intégration unique d’Adobe Experience Platform.

Puisqu’il existe plusieurs exécutions d’expérience pour une expérience spécifique, la réponse renvoyée comporte un tableau d’identifiant d’exécution.

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

`{EXPERIMENT_RUN_ID}` : identifiant qui correspond à l’expérience d’exécution.\
`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience sous laquelle se trouve l’exécution.

### Arrêt et suppression d’une expérience planifiée

Si vous souhaitez arrêter l’exécution d’une expérience planifiée avant son `endTime`, vous pouvez faire une requête DELETE à l’`{EXPERIMENT_ID}`.

**Requête**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{IMS_ORG}` : vos informations d’identification d’organisation IMS, qui se trouvent dans votre intégration unique d’Adobe Experience Platform.

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

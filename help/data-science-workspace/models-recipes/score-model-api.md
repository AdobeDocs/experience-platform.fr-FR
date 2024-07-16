---
keywords: Experience Platform;Noter un modèle;Data Science Workspace;rubriques les plus consultées;API d’apprentissage automatique sensei
solution: Experience Platform
title: Notation d’un modèle à l’aide de l’API d’apprentissage automatique Sensei
type: Tutorial
description: Ce tutoriel vous explique comment tirer parti des API d’apprentissage automatique de Sensei pour créer une expérience et une exécution d’expérience.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 77%

---

# Notation d’un modèle à l’aide de [!DNL Sensei Machine Learning API]

Ce tutoriel explique comment utiliser les API pour créer une expérience et une exécution d’expérience. Pour obtenir la liste de tous les points de terminaison de l’API Sensei Machine Learning, reportez-vous à [ce document](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Création d’une expérience planifiée pour la notation

Comme pour les expériences planifiées pour la formation, la création d’une expérience planifiée pour la notation est également effectuée en ajoutant une section `template` au paramètre du corps. De plus, le champ `name` sous `tasks` dans le corps est défini sur `score`.

Vous trouverez ci-dessous un exemple de création d’une expérience qui s’exécutera toutes les 20 minutes entre `startTime` et `endTime`.

**Requête**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}` : les informations d’identification de votre organisation se trouvent dans votre intégration Adobe Experience Platform unique.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.\
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}` : les informations d’identification de votre organisation se trouvent dans votre intégration Adobe Experience Platform unique.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{API_KEY}` : votre valeur clé d’API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.\
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
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience sous laquelle se trouve l’exécution.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{ORG_ID}` : les informations d’identification de votre organisation se trouvent dans votre intégration Adobe Experience Platform unique.

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}` : identifiant qui correspond à l’expérience.\
`{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.\
`{ORG_ID}` : les informations d’identification de votre organisation se trouvent dans votre intégration Adobe Experience Platform unique.

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

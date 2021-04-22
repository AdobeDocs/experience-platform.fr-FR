---
keywords: Experience Platform ; publier un modèle ; Espace de travail des sciences de données ; sujets populaires ; api d’apprentissage automatique sensei
solution: Experience Platform
title: Publication d'un modèle en tant que service à l'aide de l'API d'apprentissage automatique Sensei
topic-legacy: tutorial
type: Tutorial
description: Ce didacticiel porte sur le processus de publication d'un modèle en tant que service à l'aide de l'API d'apprentissage automatique Sensei.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
translation-type: tm+mt
source-git-commit: a6d047d52dad085ba662bd684c896bdffe3eef2e
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 47%

---

# Publiez un modèle en tant que service en utilisant [!DNL Sensei Machine Learning API]

Ce didacticiel porte sur le processus de publication d’un modèle en tant que service à l’aide de [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Prise en main

Ce didacticiel nécessite une bonne compréhension de Adobe Experience Platform Data Science Workspace. Avant de commencer ce didacticiel, veuillez consulter la [présentation de Data Science Workspace](../home.md) pour une présentation générale du service.

Pour suivre ce didacticiel, vous devez disposer d&#39;un moteur ML, d&#39;une instance ML et d&#39;une expérience. Pour savoir comment les créer dans l&#39;API, consultez le didacticiel sur l&#39;[importation d&#39;une recette emballée](./import-packaged-recipe-api.md).

Enfin, avant de commencer ce didacticiel, consultez la section [prise en main](../api/getting-started.md) du guide du développeur pour obtenir des informations importantes que vous devez connaître pour pouvoir invoquer l&#39;API [!DNL Sensei Machine Learning], y compris les en-têtes requis utilisés dans ce didacticiel :

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

Toutes les requêtes POST, PUT et PATCH requièrent un en-tête supplémentaire :

- Content-Type: application/json

### Termes clés

Le tableau suivant décrit la terminologie utilisée dans ce tutoriel :

| Terme | Définition |
| --- | --- |
| **Instance d’apprentissage automatique (instance ML)** | Instance d&#39;un moteur [!DNL Sensei] pour un client particulier, contenant des données, des paramètres et un code [!DNL Sensei] spécifiques. |
| **Expérience** | Entité parapluie permettant d’organiser des exécutions d’expériences de formation ou de notation ou les deux. |
| **Expérience planifiée** | Terme décrivant l’automatisation des exécutions d’expériences de formation ou de notation, régies par un calendrier défini par l’utilisateur. |
| **Exécution de l’expérience** | Une instance particulière d’expériences de formation ou de notation. Les exécutions d’expériences multiples provenant d’une expérience particulière peuvent différer des valeurs de jeu de données utilisées pour la formation ou la notation. |
| **Modèle formé** | Un modèle d’apprentissage automatique créé par le processus d’expérimentation et d’ingénierie de caractéristiques avant d’arriver à un modèle validé, évalué et finalisé. |
| **Modèle publié** | Un modèle finalisé et versionné est arrivé après la formation, la validation et l’évaluation. |
| **Service d’apprentissage automatique (service ML)** | Une instance ML déployée en tant que service pour prendre en charge les demandes de formation et de notation à la demande à l’aide d’un point de terminaison API. Un service ML peut également être créé à l’aide d’exécutions d’expériences entraînées existantes. |

## Création d’un service ML avec une exécution d’expérience de formation existante et un score planifié

Lorsque vous publiez une expérience de formation Exécuter en tant que service ML, vous pouvez planifier la notation en fournissant des détails pour l’expérience de score Exécutez la charge utile d’une demande de POST. Cela entraîne la création d’une entité Expérience planifiée pour la notation.

**Format d’API**

```http
POST /mlServices
```

**Requête**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `mlInstanceId` | Identification d&#39;instance ML existante, l&#39;exécution d&#39;expérience de formation utilisée pour créer le service ML doit correspondre à cette instance ML particulière. |
| `trainingExperimentId` | Identification de l&#39;expérience correspondant à l&#39;identification de l&#39;instance ML. |
| `trainingExperimentRunId` | Exécution d&#39;une expérience de formation spécifique à utiliser pour la publication du service ML. |
| `scoringDataSetId` | Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de notation planifiées. |
| `scoringTimeframe` | Valeur entière représentant les minutes pour la filtration des données à utiliser pour les exécutions d’expérience de notation. Par exemple, une valeur de `10080` signifie que les données des dernières 10 080 minutes ou 168 heures seront utilisées pour chaque exécution des expériences de notation planifiées. Notez qu’une valeur de `0` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation. |
| `scoringSchedule` | Contient des détails sur les exécutions d’expériences de notation planifiées. |
| `scoringSchedule.startTime` | Date/heure indiquant à quel moment début le score. |
| `scoringSchedule.endTime` | Date/heure indiquant à quel moment début le score. |
| `scoringSchedule.cron` | Valeur cron indiquant l’intervalle de score des exécutions d’expérience. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau service ML, y compris son `id` unique et le `scoringExperimentId` pour son expérience de score correspondante.


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## Création d&#39;un service ML à partir d&#39;une instance ML existante

En fonction de votre cas d&#39;utilisation et de vos besoins spécifiques, la création d&#39;un service ML avec une instance ML est flexible en termes de planification de la formation et de notation des exécutions d&#39;expériences. Ce tutoriel décrit les cas spécifiques où :

- [Vous n’avez pas besoin d’une formation planifiée, mais d’une notation planifiée.](#ml-service-with-scheduled-experiment-for-scoring)
- [Vous avez besoin d’exécutions d’expériences planifiées pour la formation et la notation.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Notez qu’un service ML peut être créé à l’aide d’une instance ML sans avoir à programmer d’expériences de formation ou de notation. Ces services ML créeront des entités d&#39;expérience ordinaires et une seule exécution d&#39;expérience pour la formation et la notation.

### Service ML avec une expérience planifiée pour la notation {#ml-service-with-scheduled-experiment-for-scoring}

Vous pouvez créer un service ML en publiant une instance ML avec des exécutions d&#39;expériences planifiées pour le score, ce qui créera une entité Expérience ordinaire pour la formation. Une exécution d’expérience de formation est générée et sera utilisée pour toutes les exécutions d’expériences de score planifiées. Assurez-vous que vous disposez des valeurs `mlInstanceId`, `trainingDataSetId` et `scoringDataSetId` requises pour la création du service ML, qu’elles existent et qu’elles sont des valeurs valides.

**Format d’API**

```http
POST /mlServices
```

**Requête**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Clé JSON | Description |
| --- | --- |
| `mlInstanceId` | Identification de l’instance ML existante, représentant l’instance ML utilisée pour créer le service ML. |
| `trainingDataSetId` | Identification faisant référence au jeu de données spécifique à utiliser pour l’expérience de formation. |
| `trainingTimeframe` | Valeur entière représentant les minutes pour la filtration des données à utiliser pour les expériences de formation. Par exemple, une valeur de `"10080"` signifie que les données des dernières 10 080 minutes ou 168 heures seront utilisées pour l’exécution d’expérience de formation. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la formation. |
| `scoringDataSetId` | Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de notation planifiées. |
| `scoringTimeframe` | Valeur entière représentant les minutes pour la filtration des données à utiliser pour les exécutions d’expérience de notation. Par exemple, une valeur de `"10080"` signifie que les données des dernières 10 080 minutes ou 168 heures seront utilisées pour chaque exécution des expériences de notation planifiées. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation. |
| `scoringSchedule` | Contient des détails sur les exécutions d’expériences de notation planifiées. |
| `scoringSchedule.startTime` | Date/heure indiquant à quel moment début le score. |
| `scoringSchedule.endTime` | Date/heure indiquant à quel moment début le score. |
| `scoringSchedule.cron` | Valeur cron indiquant l’intervalle de score des exécutions d’expérience. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau service ML. Cela inclut les `id` uniques du service, ainsi que les `trainingExperimentId` et `scoringExperimentId` pour les expériences de formation et de notation correspondantes, respectivement.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### Service ML avec des expériences planifiées pour la formation et la notation {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Pour publier une instance ML existante en tant que service ML avec une formation planifiée et des exécutions d’expériences de score, vous devez fournir des calendriers de formation et de notation. Lorsqu&#39;un service ML de cette configuration est créé, des entités Expérience planifiées pour la formation et le score sont également créées. Notez que les calendriers de formation et de notation ne doivent pas nécessairement être les mêmes. Au cours de l’exécution d’une tâche de notation, le dernier modèle formé produit par les exécutions d’expériences de formation programmée est récupéré et utilisé pour l’exécution de notation planifiée.

**Format d’API**

```http
POST /mlServices
```

**Requête**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Clé JSON | Description |
| --- | --- |
| `mlInstanceId` | Identification de l’instance ML existante, représentant l’instance ML utilisée pour créer le service ML. |
| `trainingDataSetId` | Identification faisant référence au jeu de données spécifique à utiliser pour l’expérience de formation. |
| `trainingTimeframe` | Valeur entière représentant les minutes pour la filtration des données à utiliser pour les expériences de formation. Par exemple, une valeur de `"10080"` signifie que les données des dernières 10 080 minutes ou 168 heures seront utilisées pour l’exécution d’expérience de formation. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la formation. |
| `scoringDataSetId` | Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de notation planifiées. |
| `scoringTimeframe` | Valeur entière représentant les minutes pour la filtration des données à utiliser pour les exécutions d’expérience de notation. Par exemple, une valeur de `"10080"` signifie que les données des dernières 10 080 minutes ou 168 heures seront utilisées pour chaque exécution des expériences de notation planifiées. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation. |
| `trainingSchedule` | Contient des détails sur les exécutions d’expériences de formation planifiées. |
| `scoringSchedule` | Contient des détails sur les exécutions d’expériences de notation planifiées. |
| `scoringSchedule.startTime` | Date/heure indiquant à quel moment début le score. |
| `scoringSchedule.endTime` | Date/heure indiquant à quel moment début le score. |
| `scoringSchedule.cron` | Valeur cron indiquant l’intervalle de score des exécutions d’expérience. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau service ML. Cela inclut les `id` uniques du service, ainsi que les `trainingExperimentId` et `scoringExperimentId` de ses expériences de formation et de notation correspondantes, respectivement. Dans l&#39;exemple de réponse ci-dessous, la présence de `trainingSchedule` et `scoringSchedule` suggère que les entités Expérience pour la formation et la notation sont des expériences planifiées.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## Rechercher un service ML {#retrieving-ml-services}

Vous pouvez rechercher un service ML existant en adressant une requête `GET` à `/mlServices` et en fournissant l&#39;unique `id` du service ML dans le chemin d&#39;accès.

**Format d’API**

```http
GET /mlServices/{SERVICE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SERVICE_ID}` | Le `id` unique du service ML que vous recherchez. |

**Requête**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails du service ML.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>La récupération de différents services ML peut renvoyer une réponse avec plus ou moins de paires clé-valeur. La réponse ci-dessus est une représentation d’[un service ML avec des exécutions d’expériences de notation et de formation planifiées](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Planification de la formation ou de la notation

Si vous souhaitez planifier la notation et la formation sur un service ML déjà publié, vous pouvez le faire en mettant à jour le service ML existant avec une demande `PUT` le `/mlServices`.

**Format d’API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SERVICE_ID}` | `id` unique du service ML que vous mettez à jour. |

**Requête**

La requête suivante planifie la formation et le score pour un service ML existant en ajoutant les clés `trainingSchedule` et `scoringSchedule` avec leurs clés respectives `startTime`, `endTime` et `cron`.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>N&#39;essayez pas de modifier le `startTime` sur les tâches de formation et de notation planifiées existantes. Si le modèle `startTime` doit être modifié, pensez à publier le même modèle et à reprogrammer les tâches de formation et de notation.

**Réponse**

Une réponse réussie renvoie les détails du service ML mis à jour.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```

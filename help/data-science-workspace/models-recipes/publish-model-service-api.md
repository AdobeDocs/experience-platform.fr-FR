---
keywords: Experience Platform;publier un modèle;Workspace de science des données;rubriques populaires;api de machine learning sensei
solution: Experience Platform
title: Publish a Model as a Service à l’aide de l’API Sensei Machine Learning
type: Tutorial
description: Ce tutoriel décrit le processus de publication d’un modèle en tant que service à l’aide de l’API Sensei Machine Learning.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 44%

---

# Publish d’un modèle en tant que service à l’aide du [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Ce tutoriel décrit le processus de publication d’un modèle en tant que service à l’aide de l’[[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) .

## Commencer

Ce tutoriel nécessite une compréhension pratique de Adobe Experience Platform Data Science Workspace. Avant de commencer ce tutoriel, consultez la [&#x200B; Présentation du Workspace de science des données &#x200B;](../home.md) pour une présentation détaillée du service.

Pour suivre ce tutoriel, vous devez disposer d’un moteur ML, d’une instance ML et d’une expérience existants. Pour savoir comment les créer dans l’API, suivez le tutoriel sur [l’importation d’une recette empaquetée](./import-packaged-recipe-api.md).

Enfin, avant de commencer ce tutoriel, consultez la section [prise en main](../api/getting-started.md) du guide de développement pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API [!DNL Sensei Machine Learning], y compris les en-têtes requis utilisés tout au long de ce tutoriel :

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Toutes les requêtes POST, PUT et PATCH requièrent un en-tête supplémentaire :

- Content-Type: application/json

### Termes clés

Le tableau suivant présente la terminologie courante utilisée dans ce tutoriel :

| Terme | Définition |
| --- | --- |
| **Instance de machine learning (instance ML)** | Instance d’un moteur de [!DNL Sensei] pour un client spécifique, contenant des données, des paramètres et un code [!DNL Sensei] spécifiques. |
| **Expérience** | Entité parapluie permettant d’organiser des exécutions d’expériences de formation ou de notation ou les deux. |
| **Expérience planifiée** | Terme décrivant l’automatisation des exécutions d’expériences de formation ou de notation, régies par un calendrier défini par l’utilisateur. |
| **Exécution de l’expérience** | Une instance particulière d’expériences de formation ou de notation. Les exécutions d’expériences multiples provenant d’une expérience particulière peuvent différer des valeurs de jeu de données utilisées pour la formation ou la notation. |
| **Modèle formé** | Un modèle de machine learning créé par le processus d’expérimentation et d’ingénierie de caractéristiques avant d’arriver à un modèle validé, évalué et finalisé. |
| **Modèle publié** | Un modèle finalisé et versionné est arrivé après la formation, la validation et l’évaluation. |
| **Service de machine learning (service ML)** | Une instance ML déployée en tant que service pour prendre en charge les requêtes à la demande de formation et de notation à l’aide d’un point d’entrée d’API. Un service ML peut également être créé à l’aide d’exécutions d’expérience entraînées existantes. |

## Créer un service ML avec une exécution d’expérience de formation existante et une notation planifiée

Lorsque vous publiez une expérience de formation exécutée en tant que service ML, vous pouvez planifier la notation en fournissant des détails sur l’exécution de l’expérience de notation de la payload d’une requête POST. Cela entraîne la création d’une entité d’expérience planifiée pour la notation.

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
| `mlInstanceId` | L’identification de l’instance ML existante, l’exécution d’expérience de formation utilisée pour créer le service ML, doit correspondre à cette instance ML spécifique. |
| `trainingExperimentId` | Identification de l’expérience correspondant à l’identification de l’instance ML. |
| `trainingExperimentRunId` | Une expérience d’entraînement spécifique s’exécute pour être utilisée pour publier le service ML. |
| `scoringDataSetId` | Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de notation planifiées. |
| `scoringTimeframe` | Valeur entière représentant les minutes pour la filtration des données à utiliser pour les exécutions d’expérience de notation. Par exemple, une valeur de `10080` signifie que les données des dernières 10 080 minutes ou 168 heures seront utilisées pour chaque exécution des expériences de notation planifiées. Notez qu’une valeur de `0` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation. |
| `scoringSchedule` | Contient des détails sur les exécutions d’expériences de notation planifiées. |
| `scoringSchedule.startTime` | Date et heure indiquant quand commencer la notation. |
| `scoringSchedule.endTime` | Date et heure indiquant quand commencer la notation. |
| `scoringSchedule.cron` | Valeur cron indiquant l’intervalle selon lequel noter les exécutions d’expérience. |

**Réponse**

Une réponse réussie renvoie les détails du service ML nouvellement créé, y compris son `id` unique et le `scoringExperimentId` de son expérience de notation correspondante.


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

## Créer un service ML à partir d&#39;une instance ML existante

Selon votre cas d’utilisation et vos exigences spécifiques, la création d’un service ML avec une instance ML est flexible en termes de planification de la formation et de notation des exécutions d’expérience. Ce tutoriel décrit les cas spécifiques où :

- [Vous n’avez pas besoin de formation planifiée, mais vous avez besoin d’une notation planifiée.](#ml-service-with-scheduled-experiment-for-scoring)
- [Vous avez besoin d’exécutions d’expériences planifiées pour la formation et la notation.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Notez qu’un service ML peut être créé à l’aide d’une instance ML sans planifier de formation ou d’expérience de notation. Ces services ML créeront des entités d’expérience ordinaires et une seule exécution d’expérience pour la formation et la notation.

### Service ML avec une expérience planifiée pour la notation {#ml-service-with-scheduled-experiment-for-scoring}

Vous pouvez créer un service ML en publiant une instance ML avec des exécutions d’expérience planifiées pour la notation, ce qui créera une entité d’expérience ordinaire pour la formation. Une exécution d’expérience de formation est générée et sera utilisée pour toutes les exécutions d’expérience de notation planifiées. Assurez-vous que vous disposez des valeurs `mlInstanceId`, `trainingDataSetId` et `scoringDataSetId` requises pour la création du service ML, qu’elles existent et qu’elles sont des valeurs valides.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
| `scoringSchedule.startTime` | Date et heure indiquant quand commencer la notation. |
| `scoringSchedule.endTime` | Date et heure indiquant quand commencer la notation. |
| `scoringSchedule.cron` | Valeur cron indiquant l’intervalle selon lequel noter les exécutions d’expérience. |

**Réponse**

Une réponse réussie renvoie les détails du service ML nouvellement créé. Cela inclut le `id` unique du service, ainsi que les `trainingExperimentId` et `scoringExperimentId` pour ses expériences de formation et de notation correspondantes, respectivement.

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

Pour publier une instance ML existante en tant que service ML avec des exécutions d’expérience de formation et de notation planifiées, vous devez fournir des plannings de formation et de notation. Lorsqu’un service ML de cette configuration est créé, des entités d’expérience planifiées pour la formation et la notation sont également créées. Notez que les calendriers de formation et de notation ne doivent pas nécessairement être les mêmes. Au cours de l’exécution d’une tâche de notation, le dernier modèle formé produit par les exécutions d’expériences de formation programmée est récupéré et utilisé pour l’exécution de notation planifiée.

**Format d’API**

```http
POST /mlServices
```

**Requête**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
| `scoringSchedule.startTime` | Date et heure indiquant quand commencer la notation. |
| `scoringSchedule.endTime` | Date et heure indiquant quand commencer la notation. |
| `scoringSchedule.cron` | Valeur cron indiquant l’intervalle selon lequel noter les exécutions d’expérience. |

**Réponse**

Une réponse réussie renvoie les détails du service ML nouvellement créé. Cela inclut le `id` unique du service, ainsi que la `trainingExperimentId` et la `scoringExperimentId` de ses expériences de formation et de notation correspondantes, respectivement. Dans l’exemple de réponse ci-dessous, la présence de `trainingSchedule` et `scoringSchedule` suggère que les entités d’expérience pour la formation et la notation sont des expériences planifiées.

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

## Recherche d’un service ML {#retrieving-ml-services}

Vous pouvez rechercher un service ML existant en effectuant une requête `GET` à `/mlServices` et en fournissant le `id` unique du service ML dans le chemin .

**Format d’API**

```http
GET /mlServices/{SERVICE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SERVICE_ID}` | `id` unique du service ML que vous recherchez. |

**Requête**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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

Si vous souhaitez planifier la notation et la formation sur un service ML qui a déjà été publié, vous pouvez le faire en mettant à jour le service ML existant avec une requête `PUT` le `/mlServices`.

**Format d’API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SERVICE_ID}` | `id` unique du service ML que vous mettez à jour. |

**Requête**

La requête suivante planifie la formation et la notation pour un service ML existant en ajoutant les clés `trainingSchedule` et `scoringSchedule` avec leurs clés `startTime`, `endTime` et `cron` respectives.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
>N’essayez pas de modifier les `startTime` des tâches de formation et de notation planifiées existantes. Si le modèle `startTime` doit être modifié, pensez à publier le même modèle et à reprogrammer les tâches de formation et de notation.

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

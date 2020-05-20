---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publication d’un modèle en tant que service (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 1%

---


# Publication d’un modèle en tant que service (API)

## Conditions préalables

- Suivez ce [didacticiel](../../tutorials/authentication.md) pour obtenir l’autorisation d’effectuer des appels d’API par début.
Dans le didacticiel, vous devez maintenant disposer des informations suivantes :
   - `{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.
   - `{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.
   - `{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.
- Ce didacticiel nécessite les entités existantes ML Engine, ML Instance et Experiment. Reportez-vous à ce [didacticiel](./import-packaged-recipe-api.md) sur la création d&#39;entités ML Engine, ML Instance ou Experiment.
- Pour plus d&#39;informations sur les points de terminaison et les requêtes d&#39;API mentionnés dans ce didacticiel, consultez l&#39;API [d&#39;apprentissage automatique](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei complète.

## Termes clés

Voici quelques termes courants utilisés dans ce tutoriel :

| Terme | Définition |
--- | ---
| **Instance d&#39;apprentissage automatique (instance ML)** | Entité conceptuelle qui est une instance d&#39;un moteur Sensei pour un client particulier, composée de données, de paramètres et de code Sensei spécifiques. |
| **Expérience** | Entité parapluie permettant d’organiser des exécutions d’expériences de formation, des exécutions d’expériences de score ou les deux. |
| **Expérience planifiée** | Terme décrivant l’automatisation des exécutions d’expériences de formation ou de notation, régies par un calendrier défini par l’utilisateur. |
| **Exécution de l’expérience** | Un cas particulier d&#39;expériences de formation ou de notation. Les exécutions d’expériences multiples d’une expérience particulière peuvent différer des valeurs de jeu de données utilisées pour la formation ou la notation. |
| **Modèle formé** | Un modèle d&#39;apprentissage automatique créé par le processus d&#39;expérimentation et d&#39;ingénierie de caractéristiques avant d&#39;arriver à un modèle validé, évalué et finalisé. |
| **Modèle publié** | Un modèle finalisé et versionné est arrivé après la formation, la validation et l&#39;évaluation. |
| **Service d&#39;apprentissage automatique (service ML)** | Une instance ML déployée en tant que service pour prendre en charge la demande de formation et de notation via un point de terminaison. Notez qu&#39;un service ML peut également être créé à l&#39;aide d&#39;exécutions d&#39;expériences entraînées existantes. |


## Processus API

Ce didacticiel porte sur la création, la récupération et la mise à jour d&#39;un service ML.

## Création d’un service ML avec une exécution d’expérience de formation existante et un score planifié

Lorsque vous publiez une expérience de formation exécutée en tant que service ML, vous pouvez planifier la notation en fournissant des détails pour l’expérience de score exécutée dans `scoringSchedule` votre {JSON_PAYLOAD}. Cela entraîne la création d&#39;une entité Expérience planifiée pour la notation. Vérifiez que vous disposez des valeurs `mlInstanceId`, `trainingExperimentId`, `trainingExperimentRunId`, `scoringDataSetId`et qu’elles existent et qu’elles sont des valeurs valides.

Au début, faites une `POST` demande à `/mlServices`. Vous trouverez ci-dessous un exemple de commande d’exécution :

**Requête**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S d’Adobe.
- `{ACCESS_TOKEN}` : Votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{JSON_PAYLOAD}` : Vous trouverez ci-dessous un exemple de format de charge utile JSON :

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` : Identification d&#39;instance ML existante, l&#39;exécution d&#39;expérience de formation utilisée pour créer le service ML doit correspondre à cette instance ML particulière.
- `trainingExperimentId` : Identification de l&#39;expérience correspondant à l&#39;identification de l&#39;instance ML.
- `trainingExperimentRunId` : Exécution d&#39;une expérience de formation spécifique à utiliser pour la publication du service ML.
- `scoringDataSetId` : Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de score planifiées.
- `scoringTimeframe` : Valeur Entier représentant les minutes de filtrage des données à utiliser pour les exécutions d’expériences de score. Par exemple, une valeur de `"10080"` moyenne pour les données des 10 080 dernières minutes ou 168 heures sera utilisée pour chaque exécution d’expérience de score planifiée. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation.
- `scoringSchedule` : Contient des détails sur les exécutions d’expériences de score planifiées.
- `startTime` : définition.
- `endTime` : définition.
- `cron` : définition.

**Réponse**

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

À partir de la réponse JSON, la clé `scoringExperimentId` avec sa valeur correspondante suggère qu’une nouvelle expérience de score a été créée, ainsi que le calendrier de l’expérience que vous avez fourni dans la `POST` demande. La `id` clé de la réponse identifie de manière unique le service ML créé.

## Création d&#39;un service ML à partir d&#39;une instance ML existante

En fonction de votre cas d&#39;utilisation et de vos besoins spécifiques, la création d&#39;un service ML avec une instance ML est flexible en termes de planification de la formation et de notation des exécutions d&#39;expériences. Ce didacticiel porte sur les cas spécifiques où :

- [Vous n’avez pas besoin d’une formation planifiée, mais d’un score planifié.](#ml-service-with-scheduled-experiment-for-scoring)
- [Vous avez besoin d’exécutions d’expériences planifiées pour la formation et le score.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Notez qu’un service ML peut être créé à l’aide d’une instance ML sans avoir à programmer d’expériences de formation ou de notation. Ce service ML crée des entités d&#39;expérience ordinaires et une seule exécution d&#39;expérience pour la formation et la notation.

### Service ML avec expérience planifiée pour le score {#ml-service-with-scheduled-experiment-for-scoring}

La création d&#39;un service ML en publiant une instance ML avec des exécutions d&#39;expériences planifiées pour le score entraînera la création d&#39;une entité Expérience ordinaire pour la formation. L’exécution d’expérience de formation qui en résulte sera utilisée pour toutes les exécutions d’expériences de score planifiées. Assurez-vous que vous disposez des éléments `mlInstanceId`, `trainingDataSetId`et `scoringDataSetId` requis pour la création du service ML, qu’ils existent et qu’ils sont des valeurs valides.

Au début, faites une `POST` demande à `/mlServices`. Vous trouverez ci-dessous un exemple de commande d’exécution :

**Requête**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S d’Adobe.
- `{ACCESS_TOKEN}` : Votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{JSON_PAYLOAD}` : Vous trouverez ci-dessous un exemple de format de charge utile JSON :

```JSON
{
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
}
```

| Clé JSON | Description |
| --- | --- |
| **`mlInstanceId`** | Identification d&#39;instance ML existante, représentant l&#39;instance ML utilisée pour créer le service ML. |
| **`trainingDataSetId`** | Identification faisant référence au jeu de données spécifique à utiliser pour l&#39;expérience de formation. |
| **`trainingTimeframe`** | Valeur Entier représentant les minutes de filtrage des données à utiliser pour l’expérience de formation. Par exemple, une valeur de `"10080"` moyenne pour les données des 10 080 dernières minutes ou 168 heures sera utilisée pour l’exécution de l’expérience de formation. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la formation. |
| **`scoringDataSetId`** | Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de score planifiées. |
| **`scoringTimeframe`** | Valeur Entier représentant les minutes de filtrage des données à utiliser pour les exécutions d’expériences de score. Par exemple, une valeur de `"10080"` moyenne pour les données des 10 080 dernières minutes ou 168 heures sera utilisée pour chaque exécution d’expérience de score planifiée. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation. |
| **`scoringSchedule`** | Contient des détails sur les exécutions d’expériences de score planifiées. |

**Réponse**

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

À partir de la `JSON` réponse, les clés `trainingExperimentId` et `scoringExperimentId` suggèrent qu&#39;une nouvelle entité d&#39;expérience de formation et de notation a été créée pour ce service ML. La présence de l’ `scoringSchedule` objet fait référence aux détails du calendrier d’exécution de l’expérience de score. La `id` clé de la réponse fait référence au service ML que vous venez de créer.

### Service ML avec expériences planifiées pour la formation et la notation {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Pour publier une instance ML existante en tant que service ML avec une formation planifiée et des exécutions d’expériences de score, vous devez fournir des calendriers de formation et de notation. Lorsqu&#39;un service ML de cette configuration est créé, des entités Expérience planifiées pour la formation et le score sont également créées. Notez que les calendriers de formation et de notation ne doivent pas nécessairement être les mêmes. Lors de l’exécution d’un travail de score, le dernier modèle de formation produit par les exécutions d’expériences de formation programmée est récupéré et utilisé pour l’exécution de score planifiée.

Pour créer le service ML, faites une `POST` demande `/mlServices` avec le `{JSON_PAYLOAD}` représentant de l&#39;objet de service ML à ajouter. Assurez-vous que le `mlInstanceId`, `trainingDataSetId`et `scoringDataSetId` existe et sont des valeurs valides.

**Requête**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` : Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S d’Adobe.
- `{ACCESS_TOKEN}` : Votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{JSON_PAYLOAD}` : Vous trouverez ci-dessous un exemple de format de charge utile JSON :

```JSON
{
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
}
```

| Clé JSON | Description |
| --- | --- |
| **`mlInstanceId`** | Identification d&#39;instance ML existante, représentant l&#39;instance ML utilisée pour créer le service ML. |
| **`trainingDataSetId`** | Identification faisant référence au jeu de données spécifique à utiliser pour l&#39;expérience de formation. |
| **`trainingTimeframe`** | Valeur Entier représentant les minutes de filtrage des données à utiliser pour l’expérience de formation. Par exemple, une valeur de `"10080"` moyenne pour les données des 10 080 dernières minutes ou 168 heures sera utilisée pour l’exécution de l’expérience de formation. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la formation. |
| **`scoringDataSetId`** | Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de score planifiées. |
| **`scoringTimeframe`** | Valeur Entier représentant les minutes de filtrage des données à utiliser pour les exécutions d’expériences de score. Par exemple, une valeur de `"10080"` moyenne pour les données des 10 080 dernières minutes ou 168 heures sera utilisée pour chaque exécution d’expérience de score planifiée. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation. |
| **`trainingSchedule`** | Contient des détails sur les exécutions d’expériences de formation programmées. |
| **`scoringSchedule`** | Contient des détails sur les exécutions d’expériences de score planifiées. |

**Réponse**

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

L&#39;ajout de `trainingExperimentId` et `scoringExperimentId` dans le corps de la réponse suggère la création d&#39;entités Expérience pour la formation et la notation. La présence de `trainingSchedule` et `scoringSchedule` suggère que les entités d&#39;expérience mentionnées ci-dessus pour la formation et la notation sont des expériences planifiées. La `id` clé de la réponse fait référence au service ML que vous venez de créer.

## Récupération des services ML {#retrieving-ml-services}

La récupération d&#39;un service ML existant est aussi simple que l&#39;exécution d&#39;une `GET` requête au `/mlServices` point de terminaison. Assurez-vous d&#39;avoir l&#39;identification du service ML spécifique que vous essayez de récupérer.

**Requête**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` : Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S d’Adobe.
- `{ACCESS_TOKEN}` : Votre valeur de jeton porteur spécifique fournie après l’authentification.

**Réponse**

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

La réponse JSON représente l’objet Service ML. Cet objet est équivalent à la réponse lors de la création du service ML. Notez que la récupération de différents services ML peut renvoyer une réponse avec plus ou moins de paires clé-valeur. La réponse ci-dessus est une représentation d&#39;un service [ML avec une formation planifiée et des exécutions](#ml-service-with-scheduled-experiments-for-training-and-scoring)d&#39;expériences de score.


## Planification de la formation ou de la notation

Supposons que vous souhaitiez planifier la notation et la formation sur un service ML déjà publié, vous pouvez le faire en mettant à jour le service ML existant avec une `PUT` demande le `/mlServices`. Veillez à disposer de l&#39;identification du service ML que vous souhaitez mettre à jour. À titre de référence, [récupérer le service](#retrieving-ml-services) ML que vous souhaitez mettre à jour peut être une première étape utile.

**Requête**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` : Identification unique faisant référence au service ML que vous souhaitez mettre à jour.
- `{API_KEY}` : Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S d’Adobe.
- `{ACCESS_TOKEN}` : Votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{JSON_PAYLOAD}` : Vous trouverez ci-dessous un exemple de format de charge utile JSON :

```JSON
{
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
}
```

Vous pouvez planifier la formation et la notation en ajoutant la `trainingSchedule` touche et la `scoringSchedule` clé avec leurs `startTime`, `endTime`et `cron` clés respectives.

>[!NOTE] que `PUT` demandes on `mlServices` vous permet de modifier les Services avec les exécutions d&#39;expérience planifiées existantes. Veuillez **ne pas** tenter de modifier la `startTime` liste des tâches de formation et de notation planifiées existantes. Si le modèle `startTime` doit être modifié, pensez à publier le même modèle et à replanifier les tâches de formation et de notation.

**Réponse**

La réponse sera la `{JSON_PAYLOAD}` mais avec des `id`, `created`et `updated` clés supplémentaires dans l’objet.

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

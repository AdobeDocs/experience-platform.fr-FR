---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publication d’un modèle en tant que service (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Publication d’un modèle en tant que service (API)

## Conditions préalables

- Suivez ce [didacticiel](../../tutorials/authentication.md) pour obtenir l’autorisation d’ effectuer des appels d’API.
À partir du didacticiel, vous devez maintenant disposer des informations suivantes :
   - `{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.
   - `{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique d’Adobe Experience Platform.
   - `{API_KEY}`: Votre valeur de clé d’API spécifique a été trouvée dans votre intégration unique d’Adobe Experience Platform.
- Ce didacticiel nécessite les entités existantes de moteur ML, d’instance ML et d’expérience. Reportez-vous à ce [didacticiel](./import-packaged-recipe-api.md) sur la création d&#39;entités de moteur ML, d&#39;instance ML ou d&#39;expérience.
- Pour plus d’informations sur les points de fin et les requêtes d’API mentionnés dans ce didacticiel, consultez l’API [d’apprentissage automatique](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei complète.

## Termes clés

Voici quelques termes courants utilisés dans ce didacticiel :

| Terme | Définition |
--- | ---
| **Instance d’apprentissage automatique (instance ML)** | Entité conceptuelle qui est une instance d’un moteur Sensei pour un client particulier, composée de données, de paramètres et de code Sensei spécifiques. |
| **Expérience** | Entité parapluie permettant d’organiser des exécutions d’expériences de formation, des exécutions d’expériences de notation ou les deux. |
| **Expérience planifiée** | Terme décrivant l’automatisation des exécutions d’expériences de formation ou de notation, régies par un calendrier défini par l’utilisateur. |
| **Exécution de l’expérience** | Un cas particulier d’expériences de formation ou de notation. Les exécutions d’expériences multiples d’une expérience particulière peuvent différer des valeurs de jeu de données utilisées pour la formation ou la notation. |
| **Modèle formé** | Un modèle d’apprentissage automatique créé par le processus d’expérimentation et d’ingénierie de caractéristiques avant d’arriver à un modèle validé, évalué et finalisé. |
| **Modèle publié** | Un modèle finalisé et versionné est arrivé après la formation, la validation et l&#39;évaluation. |
| **Service d&#39;apprentissage automatique (service ML)** | Une instance ML déployée en tant que service pour prendre en charge, à la demande, la demande de formation et de notation via un point de fin. Notez qu’un service ML peut également être créé à l’aide d’exécutions d’expériences entraînées existantes. |


## Processus API

Ce didacticiel décrit la création, la récupération et la mise à jour d’un service ML.

## Création d’un service ML avec une exécution d’expérience de formation existante et une notation planifiée

Lorsque vous publiez une expérience de formation exécutée en tant que service ML, vous pouvez programmer la notation en fournissant des détails sur l’expérience de notation exécutée dans `scoringSchedule` votre {JSON_PAYLOAD}. Cela entraîne la création d’une entité Expérience planifiée pour la notation. Vérifiez que vous disposez des valeurs `mlInstanceId`, `trainingExperimentId`, `trainingExperimentRunId`, `scoringDataSetId`et qu’elles existent et qu’elles sont des valeurs valides.

Pour , faites une `POST` demande à `/mlServices`. Vous trouverez ci-dessous un exemple de commande d’URL :

**Requête**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Votre valeur de clé d’API spécifique a été trouvée dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S Adobe.
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
- `trainingExperimentRunId` : Exécution d’une expérience de formation spécifique à utiliser pour la publication du service ML.
- `scoringDataSetId` : Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de score planifiées.
- `scoringTimeframe` : Valeur Entier représentant les minutes permettant de filtrer les données à utiliser pour le score des exécutions d’expérience. Par exemple, une valeur de `"10080"` signifie que les données des 10 080 dernières minutes ou 168 heures seront utilisées pour chaque exécution d’expérience de score planifiée. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation.
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

À partir de la réponse JSON, la clé `scoringExperimentId` avec sa valeur correspondante suggère qu’une nouvelle expérience de score a été créée, ainsi que le calendrier de l’expérience que vous avez fourni dans la `POST` requête. La `id` clé de la réponse identifie de manière unique le service ML créé.

## Création d’un service ML à partir d’une instance ML existante

En fonction de votre cas d’utilisation spécifique et de vos besoins, la création d’un service ML avec une instance ML est flexible en termes de planification de la formation et de notation des exécutions d’expériences. Ce didacticiel décrit les cas spécifiques où :

- [Vous n’avez pas besoin d’une formation planifiée, mais d’une évaluation planifiée.](#ml-service-with-scheduled-experiment-for-scoring)
- [Vous avez besoin de lancements d’expériences planifiés pour la formation et la notation.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Notez qu’un service ML peut être créé à l’aide d’une instance ML sans avoir à programmer d’expériences de formation ou de notation. Ce service ML crée des entités d&#39;expérience ordinaires et une seule exécution d&#39;expérience pour la formation et la notation.

### Service ML avec une expérience planifiée pour le score

La création d’un service ML en publiant une instance ML avec des exécutions d’expériences planifiées pour la notation entraîne la création d’une entité Expérience ordinaire pour la formation. L’exécution d’expérience de formation générée sera utilisée pour toutes les exécutions d’expériences de score planifiées. Assurez-vous que vous disposez des valeurs `mlInstanceId`, `trainingDataSetId`et `scoringDataSetId` requises pour la création du service ML, qu’elles existent et qu’elles sont des valeurs valides.

Pour , faites une `POST` demande à `/mlServices`. Vous trouverez ci-dessous un exemple de commande d’URL :

**Requête**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Votre valeur de clé d’API spécifique a été trouvée dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S Adobe.
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
| **`mlInstanceId`** | Identification de l’instance ML existante, représentant l’instance ML utilisée pour créer le service ML. |
| **`trainingDataSetId`** | Identification faisant référence au jeu de données spécifique à utiliser pour l’expérience de formation. |
| **`trainingTimeframe`** | Valeur Entier représentant les minutes de filtrage des données à utiliser pour l’expérience de formation. Par exemple, une valeur de `"10080"` moyennes des données des 10 080 dernières minutes ou 168 heures sera utilisée pour la course d’expérience de formation. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la formation. |
| **`scoringDataSetId`** | Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de score planifiées. |
| **`scoringTimeframe`** | Valeur Entier représentant les minutes permettant de filtrer les données à utiliser pour le score des exécutions d’expérience. Par exemple, une valeur de `"10080"` signifie que les données des 10 080 dernières minutes ou 168 heures seront utilisées pour chaque exécution d’expérience de score planifiée. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation. |
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

### Service ML avec des expériences planifiées pour la formation et la notation

Pour publier une instance ML existante en tant que service ML avec une formation planifiée et des exécutions d’expériences de score, vous devez fournir des calendriers de formation et de notation. Lorsqu’un service ML de cette configuration est créé, des entités d’expérience planifiées pour la formation et la notation sont également créées. Notez que les calendriers de formation et de notation ne doivent pas nécessairement être les mêmes. Au cours de l’exécution d’une tâche de score, le dernier modèle formé produit par les exécutions d’expériences de formation programmée est récupéré et utilisé pour l’exécution de score planifiée.

Pour créer le service ML, faites une `POST` requête `/mlServices` avec le `{JSON_PAYLOAD}` représentant de l&#39;objet de service ML à ajouter. Assurez-vous que les valeurs `mlInstanceId`, `trainingDataSetId`et `scoringDataSetId` existent et sont des valeurs valides.

**Requête**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` : Votre valeur de clé d’API spécifique a été trouvée dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S Adobe.
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
| **`mlInstanceId`** | Identification de l’instance ML existante, représentant l’instance ML utilisée pour créer le service ML. |
| **`trainingDataSetId`** | Identification faisant référence au jeu de données spécifique à utiliser pour l’expérience de formation. |
| **`trainingTimeframe`** | Valeur Entier représentant les minutes de filtrage des données à utiliser pour l’expérience de formation. Par exemple, une valeur de `"10080"` moyennes des données des 10 080 dernières minutes ou 168 heures sera utilisée pour la course d’expérience de formation. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la formation. |
| **`scoringDataSetId`** | Identification faisant référence au jeu de données spécifique à utiliser pour les exécutions d’expériences de score planifiées. |
| **`scoringTimeframe`** | Valeur Entier représentant les minutes permettant de filtrer les données à utiliser pour le score des exécutions d’expérience. Par exemple, une valeur de `"10080"` signifie que les données des 10 080 dernières minutes ou 168 heures seront utilisées pour chaque exécution d’expérience de score planifiée. Notez qu’une valeur de `"0"` ne filtre pas les données, toutes les données du jeu de données sont utilisées pour la notation. |
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

L&#39;ajout de `trainingExperimentId` et `scoringExperimentId` dans l&#39;organisme de réponse suggère la création d&#39;entités d&#39;expérience pour la formation et la notation. La présence de `trainingSchedule` et `scoringSchedule` suggère que les entités d&#39;expérience mentionnées ci-dessus pour la formation et la notation sont des expériences planifiées. La `id` clé de la réponse fait référence au service ML que vous venez de créer.

## Récupération des services ML

La récupération d&#39;un service ML existant est aussi simple que l&#39;exécution d&#39;une `GET` requête vers `/mlServices` le point de fin. Assurez-vous d&#39;avoir l&#39;identification du service ML spécifique que vous essayez de récupérer.

**Requête**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` : Votre valeur de clé d’API spécifique a été trouvée dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S Adobe.
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

La réponse JSON représente l’objet Service ML. Cet objet est équivalent à la réponse lors de la création du service ML. Notez que la récupération de différents services ML peut renvoyer une réponse avec plus ou moins de paires clé-valeur. La réponse ci-dessus est une représentation d’un service [ML avec une formation planifiée et des exécutions](#ml-service-with-scheduled-experiments-for-training-and-scoring)d’expériences de score.


## Planifier la formation ou la notation

Supposons que vous souhaitiez planifier la notation et la formation sur un service ML déjà publié, vous pouvez le faire en mettant à jour le service ML existant avec une `PUT` requête le `/mlServices`. Veillez à disposer de l&#39;identification du service ML que vous souhaitez mettre à jour. À titre de référence, [récupérer le service](#retrieving-ml-services) ML que vous souhaitez mettre à jour peut être une première étape utile.

**Requête**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` : Identification unique faisant référence au service ML que vous souhaitez mettre à jour.
- `{API_KEY}` : Votre valeur de clé d’API spécifique a été trouvée dans votre intégration unique d’Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID d’organisation IMS se trouve sous les détails de l’intégration dans la console d’E/S Adobe.
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

La planification de la formation et la notation peuvent être effectuées en ajoutant la `trainingSchedule` clé et la `scoringSchedule` clé avec leurs `startTime`, `endTime`et `cron` clés respectives.

>[!NOTE] qui `PUT` demande sur `mlServices` vous permet de modifier les Services avec les exécutions d’expérience planifiées existantes. Veuillez **ne pas** tenter de modifier la `startTime` liste des tâches de formation et de notation planifiées existantes. Si le modèle `startTime` doit être modifié, pensez à publier le même modèle et à reprogrammer les tâches de formation et de notation.

**Réponse**

La réponse sera la `{JSON_PAYLOAD}` mais avec des touches supplémentaires `id`, `created`et `updated` dans l’objet.

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

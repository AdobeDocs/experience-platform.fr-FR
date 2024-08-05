---
keywords: Experience Platform;guide de développement;point de terminaison;Data Science Workspace;rubriques les plus consultées;mlservices;api d’apprentissage automatique sensei
solution: Experience Platform
title: Point d’entrée de l’API MLServices
description: Un MLService est un modèle formé publié qui permet à votre organisation d’accéder aux modèles précédemment développés et de les réutiliser. L’une des principales caractéristiques de MLServices est sa capacité d’automatiser la formation et la notation selon un calendrier précis. Les exécutions de formation planifiées peuvent contribuer à préserver l’efficacité et la précision d’un modèle, tandis que les exécutions de notation planifiées peuvent garantir que de nouvelles informations sont générées de manière cohérente.
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 92%

---

# Point d’entrée MLServices

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Un MLService est un modèle formé publié qui permet à votre organisation d’accéder aux modèles précédemment développés et de les réutiliser. L’une des principales caractéristiques de MLServices est sa capacité d’automatiser la formation et la notation selon un calendrier précis. Les exécutions de formation planifiées peuvent contribuer à préserver l’efficacité et la précision d’un modèle, tandis que les exécutions de notation planifiées peuvent garantir que de nouvelles informations sont générées de manière cohérente.

Les calendriers de formation et de notation automatisés sont définis avec un horodatage de début et de fin, ainsi qu’une fréquence représentée sous la forme d’une expression [cron](https://fr.wikipedia.org/wiki/Cron). Les planifications peuvent être définies lors de la [création d’un MLService](#create-an-mlservice) ou appliquées en [mettant à jour un MLService existant](#update-an-mlservice).

## Création d’un MLService {#create-an-mlservice}

Vous pouvez créer un MLService en exécutant un payload et une requête POST qui fournit un nom pour le service et un identifiant MLInstance valide. L’instance MLInstance utilisée pour créer un MLService n’est pas nécessaire pour avoir des expériences de formation existantes, mais vous pouvez choisir de créer un MLService avec un modèle existant en fournissant l’identifiant d’expérience et l’identifiant d’exécution de formation correspondants.

**Format d’API**

```http
POST /mlServices
```

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom souhaité pour MLService. Le service correspondant à ce MLService héritera de cette valeur à afficher dans l’interface utilisateur de la galerie de services en tant que nom du service. |
| `description` | Description facultative du MLService. Le service correspondant à ce MLService héritera de cette valeur à afficher dans l’interface utilisateur de la galerie de services en tant que description du service. |
| `mlInstanceId` | Un identifiant MLInstance valide. |
| `trainingDataSetId` | Identifiant de jeu de données de formation qui, s’il est fourni, remplacera l’identifiant de jeu de données par défaut de MLInstance. Si l’instance MLInstance utilisée pour créer le MLService ne définit pas un jeu de données de formation, vous devez fournir un identifiant de jeu de données de formation approprié. |
| `trainingExperimentId` | Identifiant d’expérience que vous pouvez éventuellement fournir. Si cette valeur n’est pas fournie, la création de MLService créera également une nouvelle expérience à l’aide des configurations par défaut de MLInstance. |
| `trainingExperimentRunId` | Identifiant d’exécution de formation que vous pouvez éventuellement fournir. Si cette valeur n’est pas fournie, la création du MLService créera et exécutera également une exécution de formation à l’aide des paramètres de formation par défaut de MLInstance. |
| `trainingSchedule` | Calendrier des exécutions de formation automatisées. Si cette propriété est définie, le MLService effectue automatiquement des exécutions de formation selon un calendrier précis. |
| `trainingSchedule.startTime` | Horodatage pour lequel les exécutions de formation planifiées commenceront. |
| `trainingSchedule.endTime` | Horodatage pour lequel les exécutions de formation planifiées se termineront. |
| `trainingSchedule.cron` | Une expression cron qui définit la fréquence des exécutions de formation automatisées. |
| `scoringSchedule` | Calendrier des exécutions de notation automatisées. Si cette propriété est définie, le MLService effectue automatiquement des exécutions de notation selon un calendrier précis. |
| `scoringSchedule.startTime` | Horodatage pour lequel les exécutions de notation planifiées commenceront. |
| `scoringSchedule.endTime` | Horodatage pour lequel les exécutions de notation planifiées se termineront. |
| `scoringSchedule.cron` | Une expression cron qui définit la fréquence des exécutions de notation automatisées. |

**Réponse**

Une réponse réussie renvoie un payload contenant les détails du MLService nouvellement créé, y compris son identifiant unique (`id`), son identifiant d’expérience pour la formation (`trainingExperimentId`), son identifiant d’expérience pour la notation (`scoringExperimentId`) et son identifiant de jeu de données de formation d’entrée (`trainingDataSetId`).

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Obtention d’une liste de MLServices {#retrieve-a-list-of-mlservices}

Vous pouvez récupérer une liste de MLServices en exécutant une requête GET unique. Pour filtrer les résultats plus facilement, vous pouvez spécifier les paramètres de requête dans le chemin d’accès de la requête. Pour obtenir une liste des requêtes disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).

**Format d’API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETER}` | L’un des [paramètres de requête disponibles](./appendix.md#query) utilisé pour filtrer les résultats. |
| `{VALUE}` | La valeur du paramètre de requête précédent. |

**Requête**

La requête suivante contient une requête et récupère une liste de MLServices partageant le même identifiant MLInstance (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de MLService et leurs informations, y compris leur identifiant MLService (`{MLSERVICE_ID}`), son identifiant d’expérience pour la formation (`{TRAINING_ID}`), son identifiant d’expérience pour la notation (`{SCORING_ID}`) et son identifiant de jeu de données de formation d’entrée (`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## Récupération d’un MLService spécifique {#retrieve-a-specific-mlservice}

Vous pouvez récupérer les détails d’une expérience spécifique en exécutant une requête GET qui inclut l’identifiant de MLService souhaité dans le chemin de la requête.

**Format d’API**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}` : un identifiant MLService valide.

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails du MLService demandé.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Mise à jour d’un MLService {#update-an-mlservice}

Vous pouvez mettre à jour un MLService existant en écrasant ses propriétés par le biais d’une requête PUT qui inclut l’identifiant du MLService cible dans le chemin d’accès à la requête et en fournissant un payload JSON contenant des propriétés mises à jour.

>[!TIP]
>
>Afin de garantir le succès de cette requête de PUT, il est conseillé d’effectuer d’abord une requête de GET pour [récupérer le MLService par l’ID](#retrieve-a-specific-mlservice). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié en tant que payload de la requête PUT.

**Format d’API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}` : un identifiant MLService valide.

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails mis à jour du MLService.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## Suppression d’un MLService

Vous pouvez supprimer un seul MLService en exécutant une requête DELETE qui inclut l’identifiant du MLService cible dans le chemin de la requête.

**Format d’API**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLSERVICE_ID}` | Un identifiant MLService valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLService deletion was successful"
}
```

## Suppression des MLServices par l’identifiant MLInstance

Vous pouvez supprimer tous les MLServices appartenant à une MLInstance particulière en exécutant une requête DELETE qui spécifie un identifiant MLInstance comme paramètre de requête.

**Format d’API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLINSTANCE_ID}` | Un identifiant MLInstance valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLServices deletion was successful"
}
```

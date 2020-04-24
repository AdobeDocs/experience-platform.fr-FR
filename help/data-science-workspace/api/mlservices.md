---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Services
topic: Developer guide
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# MLServices

Un MLService est un modèle de formation publié qui permet à votre organisation d’accéder aux modèles précédemment développés et de les réutiliser. L&#39;une des principales caractéristiques de MLServices est la capacité d&#39;automatiser la formation et la notation sur une base planifiée. Les exécutions de formation planifiées peuvent contribuer à préserver l’efficacité et la précision d’un modèle, tandis que les exécutions de score planifiées peuvent garantir que de nouvelles informations sont générées de manière cohérente.

Les calendriers de formation et de notation automatisés sont définis avec un horodatage de début, un horodatage de fin et une fréquence représentée sous la forme d’un  <a href="https://en.wikipedia.org/wiki/Cron" target="_blank">cron</a>. Les planifications peuvent être définies lors de la [création d’un service MLService](#create-an-mlservice) ou appliquées en [mettant à jour un service MLService](#update-an-mlservice)existant.

## Création d’un service MLService {#create-an-mlservice}

Vous pouvez créer un service MLService en exécutant une requête POST et une charge utile qui fournit un nom pour le service et un ID d’instance MLService valide. L’instance MLService utilisée pour créer un service MLService n’est pas nécessaire pour avoir des expériences de formation existantes, mais vous pouvez choisir de créer le service MLService avec un modèle existant en fournissant l’ID d’expérience et l’ID d’exécution de formation correspondants.

**Format API**

```http
POST /mlServices
```

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "trainingDataSetId": "{DATASET_ID}",
        "trainingExperimentId": "{TRAINING_ID}",
        "trainingExperimentRunId": "{RUN_ID}",
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
| `name` | Nom souhaité pour MLService. Le service correspondant à ce service MLService héritera de cette valeur pour être affiché dans l’interface utilisateur de la Galerie de services en tant que nom du service. |
| `description` | Description facultative du service MLService. Le service correspondant à ce MLService héritera de cette valeur pour être affiché dans l’interface utilisateur de la Galerie de services comme description du service. |
| `mlInstanceId` | ID d’instance MLInstance valide. |
| `trainingDataSetId` | ID de jeu de données d’identification qui, s’il est fourni, remplacera l’ID de jeu de données par défaut de l’instance. Si l’instance MLInstance utilisée pour créer le service MLService ne définit pas un jeu de données de formation, vous devez fournir un ID de jeu de données de formation approprié. |
| `trainingExperimentId` | Identifiant d’expérience que vous pouvez éventuellement fournir. Si cette valeur n’est pas fournie, la création de MLService créera également une nouvelle expérience à l’aide des configurations par défaut de MLInstance. |
| `trainingExperimentRunId` | ID d’exécution de formation que vous pouvez éventuellement fournir. Si cette valeur n’est pas fournie, la création du MLService créera et exécutera également une exécution de formation à l’aide des paramètres de formation par défaut de MLInstance. |
| `trainingSchedule` | Calendrier des exécutions de formation automatisées. Si cette propriété est définie, le service MLService effectue automatiquement des exécutions de formation planifiées. |
| `trainingSchedule.startTime` | Horodatage pour lequel les exécutions de formation planifiées commenceront. |
| `trainingSchedule.endTime` | Horodatage pour lequel les exécutions planifiées de la formation se termineront. |
| `trainingSchedule.cron` | cron  qui définit la fréquence des exécutions de formation automatisées. |
| `scoringSchedule` | Une planification pour l’exécution automatisée de la notation. Si cette propriété est définie, le service MLService effectue automatiquement des exécutions de notation planifiées. |
| `scoringSchedule.startTime` | Horodatage pour lequel l’exécution de la notation planifiée commence. |
| `scoringSchedule.endTime` | Horodatage pour lequel l’exécution planifiée de la notation se termine. |
| `scoringSchedule.cron` | cron  qui définit la fréquence des exécutions de score automatisées. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du MLService nouvellement créé, y compris son identifiant unique (`id`), son identifiant d’expérience pour la formation (`trainingExperimentId`), son identifiant d’expérience pour la notation (`scoringExperimentId`) et son ID de jeu de données de formation d’entrée (`trainingDataSetId`).

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
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

## Récupération d’un de MLServices {#retrieve-a-list-of-mlservices}

Vous pouvez récupérer un de MLServices en exécutant une seule requête GET. Pour vous aider à filtrer les résultats, vous pouvez spécifier des paramètres  dans le chemin de requête. Pour un  de  de disponible, reportez-vous à la section de l’annexe sur les paramètres de [](./appendix.md#query)pour la récupérationdes ressources.

**Format API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETER}` | L’un des paramètres [de ](./appendix.md#query) utilisés pour filtrer les résultats. |
| `{VALUE}` | Valeur du paramètre  de précédent. |

**Requête**

La requête suivante contient un  et récupère un de services MLServices partageant le même ID d’instance MLServices (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId=={MLINSTANCE_ID}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un  de MLServices et leurs détails, y compris leur ID MLService (`{MLSERVICE_ID}`), l’ID d’expérience pour la formation (`{TRAINING_ID}`), l’ID d’expérience pour la notation (`{SCORING_ID}`) et l’ID du jeu de données de formation d’entrée (`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "{MLSERVICE_ID}",
            "name": "A service created in UI",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "trainingExperimentId": "{TRAINING_ID}",
            "trainingDataSetId": "{DATASET_ID}",
            "scoringExperimentId": "{SCORING_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId=={MLINSTANCE_ID},deleted==false",
        "count": 1
    }
}
```

## Récupération d’un service MLService spécifique {#retrieve-a-specific-mlservice}

Vous pouvez récupérer les détails d’une expérience spécifique en exécutant une requête GET qui inclut l’ID du service MLService souhaité dans le chemin d’accès à la requête.

**Format API**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: ID MLService valide.

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du service MLService demandé.

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Mise à jour d’un service MLService {#update-an-mlservice}

Vous pouvez mettre à jour un service MLService existant en remplaçant ses propriétés par une requête PUT qui inclut l’ID du service MLService  dans le chemin d’accès à la requête et fournit une charge JSON contenant des propriétés mises à jour.

>[!TIP] Afin d’assurer le succès de cette requête PUT, il est conseillé d’effectuer d’abord une requête GET pour [récupérer le service MLService par ID](#retrieve-a-specific-mlservice). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié comme charge utile pour la requête PUT.

**Format API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: ID MLService valide.

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "trainingExperimentId": "{TRAINING_ID}",
        "trainingDataSetId": "{DATASET_ID}",
        "scoringExperimentId": "{SCORING_ID}",
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

Une réponse réussie renvoie une charge utile contenant les détails mis à jour de MLService.

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
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

## Suppression d’un service MLService

Vous pouvez supprimer un seul service MLService en exécutant une requête DELETE qui inclut l’ID du service MLService  dans le chemin d’accès de la requête.

**Format API**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLSERVICE_ID}` | ID MLService valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Suppression de MLServices par ID d’instance MLServices

Vous pouvez supprimer tous les services MLServices appartenant à une instance MLInstance particulière en exécutant une requête DELETE qui spécifie un ID d&#39;instance MLInstance comme paramètre .

**Format API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MLSERVICE_ID}` | ID MLService valide. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

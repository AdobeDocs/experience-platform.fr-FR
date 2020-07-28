---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modèles
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 66%

---


# Modèles

Un modèle est une instance d’une recette d’apprentissage automatique formée à l’aide de données historiques et de configurations dans le but de résoudre un cas d’usage commercial.

## Récupération d’une liste de modèles

Vous pouvez récupérer une liste de détails de modèle communs à tous les modèles en exécutant une seule requête GET vers /models. Par défaut, cette liste se classe à partir du modèle créé le plus ancien et limite les résultats à 25. Vous pouvez choisir de filtrer les résultats en spécifiant certains paramètres de requête. Pour obtenir une liste des requêtes disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).

**Format d’API**

```http
GET /models
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails de vos modèles, y compris chaque identifiant unique des modèles (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant correspondant au modèle. |
| `modelArtifactUri` | Un URI indiquant l’emplacement de stockage du modèle. L’URI se termine par la valeur `name` du modèle. |
| `experimentId` | Un identifiant d’expérience valide. |
| `experimentRunId` | Un identifiant d’exécution d’expérience valide. |

## Récupération d’un modèle spécifique

Vous pouvez récupérer une liste de détails de modèle appartenant à un modèle spécifique en exécutant une seule requête GET et en renseignant un identifiant de modèle valide dans le chemin de la requête. Pour vous aider à filtrer les résultats, vous pouvez spécifier des paramètres de requête dans le chemin de requête. Pour obtenir une liste des requêtes disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).

**Format d’API**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | L’identifiant du modèle formé ou publié. |
| `{EXPERIMENT_RUN_ID}` | L’identifiant de l’exécution de l’expérience. |

**Requête**

La demande suivante contient une requête et récupère une liste de modèles formés partageant le même expérienceRunID ({EXPERIMENT_RUN_ID}).

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails de votre modèle, y compris l’identifiant unique des modèles (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant correspondant au modèle. |
| `modelArtifactUri` | Un URI indiquant l’emplacement de stockage du modèle. L’URI se termine par la valeur `name` du modèle. |
| `experimentId` | Un identifiant d’expérience valide. |
| `experimentRunId` | Un identifiant d’exécution d’expérience valide. |

## Enregistrer un modèle prégénéré {#register-a-model}

You can register a pre-generated Model by making a POST request to the `/models` endpoint. Pour enregistrer votre modèle, les valeurs de fichier et de `modelArtifact` `model` propriété doivent être incluses dans le corps de la requête.

**Format d’API**

```http
POST /models
```

**Requête**

Le POST suivant contient les valeurs de `modelArtifact` fichier et de `model` propriété nécessaires. Pour plus d’informations sur ces valeurs, voir le tableau ci-dessous.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| Paramètre | Description |
| --- | --- |
| `modelArtifact` | Emplacement de l&#39;artefact de modèle complet que vous souhaitez inclure. |
| `model` | Données de formulaire de l&#39;objet Modèle qui doit être créé. |

**Réponse**

Une réponse réussie renvoie un payload contenant les détails de votre modèle, y compris l’identifiant unique des modèles (`id`).

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant correspondant au modèle. |
| `modelArtifactUri` | Un URI indiquant l’emplacement de stockage du modèle. The URI ends with the `id` value for your model. |

## Mise à jour d’un modèle par son identifiant

Vous pouvez mettre à jour un modèle existant en écrasant ses propriétés par le biais d’une requête PUT qui inclut l’identifiant du modèle cible dans le chemin d’accès à la requête et en fournissant un payload JSON contenant des propriétés mises à jour.

>[!TIP]
>
>Afin de garantir le succès de cette requête PUT, il est conseillé d’effectuer en premier lieu une requête GET pour récupérer le modèle par son identifiant. Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié en tant que payload de la requête PUT.

**Format d’API**

```http
PUT /models/{MODEL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | L’identifiant du modèle formé ou publié. |

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails mis à jour de l’expérience.

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## Suppression d’un modèle par son identifiant

Vous pouvez supprimer un seul modèle en exécutant une requête DELETE qui inclut l’identifiant du modèle cible dans le chemin de la requête.

**Format d’API**

```http
DELETE /models/{MODEL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | L’identifiant du modèle formé ou publié. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant un état 200 qui confirme la suppression du modèle.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Créer un nouveau transcodage pour un modèle {#create-transcoded-model}

Le transcodage est la conversion numérique-numérique directe d’un codage à un autre. Vous créez un nouveau transcodage pour un modèle en fournissant les données `{MODEL_ID}` et une `targetFormat` sortie dans laquelle vous souhaitez que la nouvelle sortie soit.

**Format d’API**

```http
POST /models/{MODEL_ID}/transcodings
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | L’identifiant du modèle formé ou publié. |

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant un objet JSON avec les informations de votre transcodage. Ceci inclut l&#39;identifiant unique de transcodage (`id`) utilisé pour [récupérer un modèle](#retrieve-transcoded-model)transcodé spécifique.

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## Récupérer une liste de transcodages pour un modèle {#retrieve-transcoded-model-list}

Vous pouvez récupérer une liste de transcodages qui ont été effectués sur un modèle en exécutant une demande de GET avec votre `{MODEL_ID}`.

**Format d’API**

```http
GET /models/{MODEL_ID}/transcodings
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | L’identifiant du modèle formé ou publié. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant un objet json avec une liste de chaque transcodage effectué sur le modèle. Chaque modèle transcodé reçoit un identifiant unique (`id`).

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## Retrieve a specific transcoded Model {#retrieve-transcoded-model}

Vous pouvez récupérer un modèle transcodé spécifique en exécutant une demande de GET avec votre modèle `{MODEL_ID}` et l&#39;identifiant d&#39;un modèle transcodé.

**Format d’API**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | Identificateur unique d&#39;un modèle formé ou publié. |
| `{TRANSCODING_ID}` | Identificateur unique d&#39;un modèle transcodé. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant un objet JSON avec les données du modèle transcodé.

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```



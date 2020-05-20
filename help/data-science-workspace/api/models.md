---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modèles
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 4%

---


# Modèles

Un modèle est l&#39;instance d&#39;une recette d&#39;apprentissage automatique qui est formée à l&#39;aide de données historiques et de configurations pour résoudre un cas d&#39;utilisation commerciale.

## Récupération d’une liste de modèles

Vous pouvez récupérer une liste de détails de modèle appartenant à tous les modèles en exécutant une seule requête GET sur /models. Par défaut, cette liste se classe à partir du modèle créé le plus ancien et limite les résultats à 25. Vous pouvez choisir de filtrer les résultats en spécifiant certains paramètres de requête. Pour une liste des requêtes disponibles, reportez-vous à la section de l&#39;annexe sur les paramètres de [requête pour la récupération](./appendix.md#query)des ressources.

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

Une réponse réussie renvoie une charge utile contenant les détails de vos modèles, y compris chaque identifiant unique de modèle (`id`).

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
| `id` | ID correspondant au modèle. |
| `modelArtifactUri` | URI indiquant l’emplacement de stockage du modèle. L&#39;URI se termine par la `name` valeur du modèle. |
| `experimentId` | ID d’expérience valide. |
| `experimentRunId` | ID d’exécution d’expérience valide. |

## Récupérer un modèle spécifique

Vous pouvez récupérer une liste de détails de modèle appartenant à un modèle particulier en exécutant une seule requête GET et en fournissant un ID de modèle valide dans le chemin de la requête. Pour faciliter le filtrage des résultats, vous pouvez spécifier des paramètres de requête dans le chemin d’accès à la requête. Pour une liste des requêtes disponibles, reportez-vous à la section de l&#39;annexe sur les paramètres de [requête pour la récupération](./appendix.md#query)des ressources.

**Format d’API**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | Identificateur du modèle formé ou publié. |
| `{EXPERIMENT_RUN_ID}` | Identificateur de l&#39;exécution de l&#39;expérience. |

**Requête**

La requête suivante contient une requête et récupère une liste de modèles formés partageant la même expérienceRunID ({EXPERIMENT_RUN_ID}).

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de votre modèle, y compris l&#39;identifiant unique Modèles (`id`).

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
        "count": 1
    }
}
```

| Propriété | Description |
| --- | --- |
| `id` | ID correspondant au modèle. |
| `modelArtifactUri` | URI indiquant l’emplacement de stockage du modèle. L&#39;URI se termine par la `name` valeur du modèle. |
| `experimentId` | ID d’expérience valide. |
| `experimentRunId` | ID d’exécution d’expérience valide. |

## Mettre à jour un modèle par ID

Vous pouvez mettre à jour un modèle existant en remplaçant ses propriétés par une requête PUT qui inclut l’ID du modèle de cible dans le chemin de la requête et fournit une charge utile JSON contenant des propriétés mises à jour.

>[!TIP] Afin d&#39;assurer le succès de cette requête PUT, il est conseillé d&#39;effectuer d&#39;abord une requête GET pour récupérer le modèle par ID. Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié comme charge utile pour la demande PUT.

**Format d’API**

```http
PUT /models/{MODEL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | Identificateur du modèle formé ou publié. |

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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

Une réponse réussie renvoie une charge utile contenant les détails mis à jour de l’expérience.

```json
{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## Supprimer un modèle par ID

Vous pouvez supprimer un modèle unique en exécutant une requête DELETE qui inclut l&#39;ID du modèle de cible dans le chemin d&#39;accès à la requête.

**Format d’API**

```http
DELETE /models/{MODEL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{MODEL_ID}` | Identificateur du modèle formé ou publié. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie une charge utile contenant un état 200 confirmant la suppression du modèle.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tâches de segment
topic: developer guide
translation-type: tm+mt
source-git-commit: db4cdbfb7719d94919c896162ca7875fdf7d2502

---


# Guide du développeur de tâches de segmentation

Une tâche de segmentation est un processus asynchrone qui crée un nouveau segment  . Il fait référence à une définition de segment, ainsi qu’à toute stratégie de fusion contrôlant la manière dont les du client en temps réel fusionnent des attributs qui se chevauchent sur vos  de. Lorsqu’une tâche de segmentation se termine avec succès, vous pouvez collecter diverses informations sur le segment, telles que les erreurs qui se sont produites au cours du traitement et la taille finale de votre  de .

Ce guide fournit des informations pour vous aider à mieux comprendre les tâches de segmentation et inclut des exemples d’appels d’API pour exécuter des actions de base à l’aide de l’API.

## Prise en main

Les points de fin d’API utilisés dans ce guide font partie de l’API de segmentation. Avant de poursuivre, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [de](./getting-started.md#getting-started) prise en main du guide du développeur de segmentation comprend des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le  du et des informations importantes concernant les en-têtes requis nécessaires pour effectuer des appels à une API de plateforme d’expérience.

## Récupération d’un  de tâches de segment

Vous pouvez récupérer un  de toutes les tâches de segment pour votre organisation IMS en exécutant une requête GET sur le `/segment/jobs` point de fin.

**Format API**

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facultatif*) Paramètres ajoutés au chemin de requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous.

**Paramètres**

Vous trouverez ci-dessous un  des paramètres de disponibles pour répertorier les tâches de segments. Tous ces paramètres sont facultatifs. Un appel à ce point de fin sans paramètre récupérera toutes les tâches de segment disponibles pour votre entreprise.

| Paramètre | Description |
| --------- | ----------- |
| `start` | Spécifie le décalage de début pour les tâches de segment renvoyées. |
| `limit` | Indique le nombre de tâches de segment renvoyées par page. |
| `status` |  les résultats selon l’état. Les valeurs prises en charge sont NEW, QUEUED, TRAITEMENT, SUCCEEDED, FAILED, ANNULATION, ANNULATION |
| `sort` | Commande les tâches de segment renvoyées. Est écrit au format `[attributeName]:[desc|asc]`. |
| `property` |  les tâches de segmentation et obtient des correspondances exactes pour le filtre donné. Il peut être écrit dans l’un des formats suivants : <ul><li>`[jsonObjectPath]==[value]` - filtrage sur la touche d&#39;objet</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtrage dans le tableau</li></ul> |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec un de tâches de segmentation pour l’organisation IMS spécifiée comme JSON. La réponse suivante renvoie un  de toutes les tâches de segment réussies pour l’organisation IMS.

>[!NOTE] La réponse suivante a été tronquée pour l’espace et n’affichera que la première tâche renvoyée.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 0,
                "segmentedProfileCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": 0,
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": 0
                },
                "segmentedProfileByNamespaceCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": {},
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": {}
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## Création d’une tâche de segment

Vous pouvez créer une tâche de segment en exécutant une requête POST sur le `/segment/jobs` point de fin.

**Format API**

```http
POST /segment/jobs
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]
 '
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails de la tâche de segment que vous venez de créer.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

## Récupération d’une tâche de segment spécifique

Vous pouvez récupérer des informations détaillées sur une tâche de segment spécifique en exécutant une requête GET vers le `/segment/jobs` point de fin et en indiquant la `id` valeur de la tâche de segment dans le chemin d’accès de la requête.

**Format API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriété | Description |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Valeur `id` de la tâche de segment que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur la tâche de segment spécifiée.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

## Annuler ou supprimer une tâche de segment spécifique

Vous pouvez demander de supprimer une tâche de segment spécifiée en effectuant une requête DELETE au point de `/segment/jobs` fin et en indiquant la `id` valeur de la tâche de segment dans le chemin de requête.

**Format API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriété | Description |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Valeur `id` de la tâche de segment à supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 avec les informations suivantes.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux le fonctionnement des tâches de segmentation. Pour plus d’informations sur la segmentation, consultez la présentation [de la](../home.md)segmentation.
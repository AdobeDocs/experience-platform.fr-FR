---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; tâches de segment ; tâche de segment ; API ; api ;
solution: Experience Platform
title: Point de terminaison de l’API Tâches de segment
topic-legacy: developer guide
description: Le point de terminaison des tâches de segment dans l’API Service de segmentation Adobe Experience Platform vous permet de gérer par programmation les tâches de segment pour votre entreprise.
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 32%

---

# Point de terminaison des tâches de segment

Une tâche de segmentation est un processus asynchrone qui crée un nouveau segment ciblé. Il fait référence à une [définition de segment](./segment-definitions.md), ainsi qu’à toute [stratégie de fusion](../../profile/api/merge-policies.md) contrôlant comment [!DNL Real-time Customer Profile] fusionne des attributs qui se chevauchent dans vos fragments de profil. Lorsqu’une tâche de segmentation se termine avec succès, vous pouvez collecter diverses informations sur le segment, telles que les erreurs qui se sont produites au cours du traitement et la taille finale de votre audience.

Ce guide fournit des informations pour vous aider à mieux comprendre les tâches de segmentation et inclut des exemples d’appels API pour exécuter des actions de base à l’aide de l’API.

## Prise en main

Les points de terminaison utilisés dans ce guide font partie de l&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes que vous devez connaître pour pouvoir invoquer l&#39;API, y compris les en-têtes requis et pour savoir comment lire des exemples d&#39;appels d&#39;API.

## Obtention d’une liste de tâches de segmentation {#retrieve-list}

Vous pouvez récupérer une liste de toutes les tâches de segmentation pour votre organisation IMS en exécutant une requête GET sur le point de terminaison `/segment/jobs`.

**Format d’API**

Le point de terminaison `/segment/jobs` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est fortement recommandée pour réduire les frais généraux élevés. Un appel à ce point de terminaison sans paramètre permet de récupérer toutes les tâches d’exportation disponibles pour votre organisation. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Paramètres de requête**

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `start` | Spécifie le décalage de départ pour les tâches de segmentation renvoyées. | `start=1` |
| `limit` | Spécifie le nombre de tâches de segmentation renvoyées par page. | `limit=20` |
| `status` | Filtre les résultats selon l’état. Les valeurs prises en charge sont : NEW (nouveau), QUEUED (file d’attente), PROCESSING (traitement en cours), SUCCEEDED (réussite), FAILED (échec), CANCELLING (annulation en cours), CANCELLED (annulé). | `status=NEW` |
| `sort` | Commande les tâches de segmentation renvoyées. Codé au format `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtre les tâches de segmentation et obtient des correspondances exactes pour le filtre donné. Peut être codé dans l’un des formats suivants : <ul><li>`[jsonObjectPath]==[value]` : filtrage sur la clé d’objet</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` : filtrage dans le tableau</li></ul> | `property=segments~segmentId==workInUS` |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de tâches de segmentation pour l’organisation IMS spécifiée comme JSON. La réponse suivante renvoie une liste de toutes les tâches de segmentation réussies pour l’organisation IMS.

>[!NOTE]
>
>La réponse suivante a été tronquée pour l’espace et affiche uniquement la première tâche renvoyée.

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
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "existing":10,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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

| Propriété | Description |
| -------- | ----------- |
| `id` | Identifiant généré par le système en lecture seule pour la tâche de segment. |
| `status` | Statut actuel de la tâche de segment. Les valeurs potentielles de l’état sont &quot;NOUVEAU&quot;, &quot;TRAITEMENT&quot;, &quot;ANNULATION&quot;, &quot;ANNULÉ&quot;, &quot;ÉCHEC&quot; et &quot;SUCCÈS&quot;. |
| `segments` | Objet contenant des informations sur les définitions de segment renvoyées dans la tâche de segment. |
| `segments.segment.id` | ID de la définition de segment. |
| `segments.segment.expression` | Objet contenant des informations sur l’expression de la définition de segment, écrit dans PQL. |
| `metrics` | Objet contenant des informations de diagnostic sur la tâche de segment. |
| `metrics.totalTime` | Objet contenant des informations sur les heures de début et de fin de la tâche de segmentation, ainsi que sur le temps total passé. |
| `metrics.profileSegmentationTime` | Objet contenant des informations sur les heures de début et de fin de l’évaluation de la segmentation, ainsi que sur le temps total passé. |
| `metrics.segmentProfileCounter` | Nombre de profils qualifiés par segment. |
| `metrics.segmentedProfileByNamespaceCounter` | Nombre de profils qualifiés pour chaque espace de nommage d&#39;identité par segment. |
| `metrics.segmentProfileByStatusCounter` | Nombre de profils pour chaque état. Les trois états suivants sont pris en charge : <ul><li>&quot;réalisé&quot; - Nombre de nouveaux profils entrés dans le segment.</li><li>&quot;existant&quot; - Nombre de profils qui persistent dans le segment.</li><li>&quot;exited&quot; : nombre de segments de profil qui n&#39;existent plus dans le segment.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Nombre total de profils fusionnés par stratégie de fusion. |

## Création d’une tâche de segmentation {#create}

Vous pouvez créer une tâche de segment en adressant une requête de POST au point de terminaison `/segment/jobs` et en incluant dans le corps l’identifiant de la définition de segment à partir de laquelle vous souhaitez créer une audience.

**Format d’API**

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
]'
```

| Propriété | Description |
| -------- | ----------- |
| `segmentId` | ID de la définition de segment pour laquelle vous souhaitez créer une tâche de segment. Ces définitions de segment peuvent appartenir à différentes stratégies de fusion. Vous trouverez plus d’informations sur les définitions de segment dans le [guide de point de terminaison de définition de segment](./segment-definitions.md). |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la tâche de segmentation que vous venez de créer.

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

| Propriété | Description |
| -------- | ----------- |
| `id` | Identificateur en lecture seule généré par le système pour la tâche de segment nouvellement créée. |
| `status` | Statut actuel de la tâche de segment. La tâche de segment venant d’être créée, l’état sera toujours &quot;NOUVEAU&quot;. |
| `segments` | Objet contenant des informations sur les définitions de segment pour lesquelles ce travail de segment est en cours d’exécution. |
| `segments.segment.id` | ID de la définition de segment que vous avez fournie. |
| `segments.segment.expression` | Objet contenant des informations sur l’expression de la définition de segment, écrit dans PQL. |

## Récupération d’une tâche de segmentation spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une tâche de segment spécifique en adressant une demande de GET au point de terminaison `/segment/jobs` et en indiquant l’identifiant de la tâche de segment que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriété | Description |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Valeur `id` de la tâche de segmentation que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la tâche de segmentation spécifiée.

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

| Propriété | Description |
| -------- | ----------- |
| `id` | Identifiant généré par le système en lecture seule pour la tâche de segment. |
| `status` | Statut actuel de la tâche de segment. Les valeurs potentielles de l’état sont &quot;NOUVEAU&quot;, &quot;TRAITEMENT&quot;, &quot;ANNULATION&quot;, &quot;ANNULÉ&quot;, &quot;ÉCHEC&quot; et &quot;SUCCÈS&quot;. |
| `segments` | Objet contenant des informations sur les définitions de segment renvoyées dans la tâche de segment. |
| `segments.segment.id` | ID de la définition de segment. |
| `segments.segment.expression` | Objet contenant des informations sur l’expression de la définition de segment, écrit dans PQL. |
| `metrics` | Objet contenant des informations de diagnostic sur la tâche de segment. |

## Récupération en masse des tâches de segment {#bulk-get}

Vous pouvez récupérer des informations détaillées sur plusieurs tâches de segment en envoyant une requête de POST au point de terminaison `/segment/jobs/bulk-get` et en fournissant les valeurs `id` des tâches de segment dans le corps de la requête.

**Format d’API**

```http
POST /segment/jobs/bulk-get
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 207 avec les tâches de segment demandées.

>[!NOTE]
>
>La réponse suivante a été tronquée pour l’espace, affichant uniquement des détails partiels de chaque tâche de segment. La réponse complète liste les détails complets des tâches de segmentation demandées.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
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
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
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
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Identifiant généré par le système en lecture seule pour la tâche de segment. |
| `status` | Statut actuel de la tâche de segment. Les valeurs potentielles de l’état sont &quot;NOUVEAU&quot;, &quot;TRAITEMENT&quot;, &quot;ANNULATION&quot;, &quot;ANNULÉ&quot;, &quot;ÉCHEC&quot; et &quot;SUCCÈS&quot;. |
| `segments` | Objet contenant des informations sur les définitions de segment renvoyées dans la tâche de segment. |
| `segments.segment.id` | ID de la définition de segment. |
| `segments.segment.expression` | Objet contenant des informations sur l’expression de la définition de segment, écrit dans PQL. |

## Annulation ou suppression d’une tâche de segmentation spécifique {#delete}

Vous pouvez supprimer une tâche de segment spécifique en adressant une requête de DELETE au point de terminaison `/segment/jobs` et en indiquant l’identifiant de la tâche de segment que vous souhaitez supprimer dans le chemin de requête.

>[!NOTE]
>
>La réponse de l’API à la demande de suppression est immédiate. Cependant, la suppression réelle de la tâche de segment est asynchrone. En d’autres termes, il existe une différence de temps entre le moment où la demande de suppression est effectuée pour la tâche de segment et celui où elle est appliquée.

**Format d’API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriété | Description |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Valeur `id` de la tâche de segmentation que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 avec les informations suivantes.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux le fonctionnement des tâches de segmentation.

---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;segment definition;segment definitions;api;API;
solution: Experience Platform
title: Définitions de segment
topic: developer guide
description: Ce guide fournit des informations pour vous aider à mieux comprendre les définitions de segment et inclut des exemples d’appels d’API pour exécuter des actions de base à l’aide de l’API.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 51%

---


# Point de terminaison des définitions de segment

Adobe Experience Platform vous permet de créer des segments définissant un groupe d’attributs ou de comportements spécifiques à partir d’un groupe de profils. A segment definition is an object that encapsulates a query written in [!DNL Profile Query Language] (PQL). Cet objet est également appelé prédicat PQL. PQL predicates define the rules for the segment based on conditions related to any record or time-series data you supply to [!DNL Real-time Customer Profile]. Pour plus d’informations sur l’écriture de requêtes PQL, reportez-vous au [guide de PQL](../pql/overview.md).

Ce guide fournit des informations pour vous aider à mieux comprendre les définitions de segment et inclut des exemples d’appels d’API pour exécuter des actions de base à l’aide de l’API.

## Prise en main

The endpoints used in this guide are part of the [!DNL Adobe Experience Platform Segmentation Service] API. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example API calls.

## Obtention d’une liste de définitions de segment {#list}

Vous pouvez obtenir une liste de toutes les définitions de segment de votre organisation IMS en envoyant une requête GET au point de terminaison `/segment/definitions`.

**Format d’API**

Le `/segment/definitions` point de terminaison prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est fortement recommandée pour réduire les frais généraux élevés. En passant un appel vers ce point de terminaison sans paramètres, vous récupérerez toutes les définitions de segment disponibles pour votre organisation. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Paramètres de requête**

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `start` | Spécifie le décalage de début pour les définitions de segment renvoyées. | `start=4` |
| `limit` | Indique le nombre de définitions de segment renvoyées par page. | `limit=20` |
| `page` | Indique à partir de quelle page commencent les résultats des définitions de segment. | `page=5` |
| `sort` | Indique le champ de tri des résultats. Is written in the following format: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Indique si la définition de segment est activée dans le flux. | `evaluationInfo.continuous.enabled=true` |

**Requête**

La demande suivante récupère les deux dernières définitions de segment publiées dans votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de définitions de segment pour l’organisation IMS spécifiée sous JSON.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Création d’une définition de segment {#create}

Vous pouvez créer une définition de segment en envoyant une requête POST au point de terminaison `/segment/definitions`.

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | **Obligatoire.** Un nom unique qui fait référence au segment. |
| `schema` | **Obligatoire.** Le schéma associé aux entités du segment. Se compose d’un champ `id` ou `name`. |
| `expression` | **Obligatoire.** Une entité qui contient des champs d’informations à propos de la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul « PQL » est pris en charge. |
| `expression.format` | Indique la structure de l’expression en valeur. Actuellement, le format suivant est pris en charge : <ul><li>`pql/text` : une représentation textuelle d’une définition de segment, selon la grammaire PQL publiée.  Par exemple : `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Une expression conforme au type indiqué dans `expression.format`. |
| `description` | Description lisible de la définition. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la définition de segment que vous venez de créer.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | ID généré par le système de votre nouvelle définition de segment. |
| `evaluationInfo` | Objet généré par le système qui indique le type d’évaluation auquel la définition de segment sera soumise. Il peut s’agir d’une segmentation par lot, continue (également appelée diffusion en continu) ou synchrone. |

## Récupération d’une définition de segment spécifique {#get}

You can retrieve detailed information about a specific segment definition by making a GET request to the `/segment/definitions` endpoint and providing the ID of the segment definition you wish to retrieve in the request path.

**Format d’API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_ID}` | The `id` value of the segment definition you want to retrieve. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les informations détaillées de la définition de segment spécifiée.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | ID en lecture seule généré par le système de la définition de segment. |
| `name` | Un nom unique qui fait référence au segment. |
| `schema` | Le schéma associé aux entités du segment. Se compose d’un champ `id` ou `name`. |
| `expression` | Une entité qui contient des champs d’informations à propos de la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul « PQL » est pris en charge. |
| `expression.format` | Indique la structure de l’expression en valeur. Actuellement, le format suivant est pris en charge : <ul><li>`pql/text` : une représentation textuelle d’une définition de segment, selon la grammaire PQL publiée.  Par exemple : `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Une expression conforme au type indiqué dans `expression.format`. |
| `description` | Une description lisible par l’utilisateur de la définition. |
| `evaluationInfo` | Objet généré par le système qui indique le type d’évaluation, de traitement par lot, continu (également appelé flux continu) ou synchrone, auquel la définition de segment sera associée. |

## Récupération en masse des définitions de segment {#bulk-get}

Vous pouvez récupérer des informations détaillées sur plusieurs définitions de segment spécifiées en envoyant une requête de POST au point de `/segment/definitions/bulk-get` terminaison et en fournissant les `id` valeurs des définitions de segment dans le corps de la requête.

**Format d’API**

```http
POST /segment/definitions/bulk-get
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 207 avec les définitions de segment demandées.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        }

    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | ID en lecture seule généré par le système de la définition de segment. |
| `name` | Un nom unique qui fait référence au segment. |
| `schema` | Le schéma associé aux entités du segment. Se compose d’un champ `id` ou `name`. |
| `expression` | Une entité qui contient des champs d’informations à propos de la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul « PQL » est pris en charge. |
| `expression.format` | Indique la structure de l’expression en valeur. Actuellement, le format suivant est pris en charge : <ul><li>`pql/text` : une représentation textuelle d’une définition de segment, selon la grammaire PQL publiée.  Par exemple : `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Une expression conforme au type indiqué dans `expression.format`. |
| `description` | Une description lisible par l’utilisateur de la définition. |
| `evaluationInfo` | Objet généré par le système qui indique le type d’évaluation, de traitement par lot, continu (également appelé flux continu) ou synchrone, auquel la définition de segment sera associée. |

## Suppression d’une définition de segment spécifique {#delete}

You can request to delete a specific segment definition by making a DELETE request to the `/segment/definitions` endpoint and providing the ID of the segment definition you wish to delete in the request path.

**Format d’API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_ID}` |  : valeur `id` de la définition de segment que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 sans message.

## Mise à jour d’une définition de segment spécifique

Vous pouvez mettre à jour une définition de segment spécifique en envoyant une requête de PATCH au point de `/segment/definitions` terminaison et en indiquant l’identifiant de la définition de segment que vous souhaitez mettre à jour dans le chemin de la requête.

**Format d’API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_ID}` | The `id` value of the segment definition you want to update. |

**Requête**

La demande suivante mettra à jour le pays d&#39;adresse de travail des États-Unis au Canada.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la définition de segment que vous venez de mettre à jour. Notez comment le pays de l&#39;adresse de travail a été mis à jour des États-Unis (États-Unis) vers le Canada (AC).

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment fonctionnent les définitions de segment. Pour plus d’informations sur la création d’un segment, consultez le didacticiel [Création d’un segment](../tutorials/create-a-segment.md) .
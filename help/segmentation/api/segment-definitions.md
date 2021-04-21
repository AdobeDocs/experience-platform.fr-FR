---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; définition de segment ; définitions de segment ; api ; API ;
solution: Experience Platform
title: Point de terminaison de l’API Définitions de segment
topic-legacy: developer guide
description: Le point de terminaison des définitions de segment dans l’API Adobe Experience Platform Segmentation Service vous permet de gérer par programmation les définitions de segment pour votre entreprise.
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 48%

---

# Point de terminaison des définitions de segment

Adobe Experience Platform vous permet de créer des segments définissant un groupe d’attributs ou de comportements spécifiques à partir d’un groupe de profils. Une définition de segment est un objet qui encapsule une requête écrite dans [!DNL Profile Query Language] (PQL). Cet objet est également appelé prédicat PQL. Les prédicats PQL définissent les règles du segment en fonction des conditions liées à tout enregistrement ou toute série de données chronologiques que vous fournissez à [!DNL Real-time Customer Profile]. Pour plus d’informations sur l’écriture de requêtes PQL, reportez-vous au [guide de PQL](../pql/overview.md).

Ce guide fournit des informations pour vous aider à mieux comprendre les définitions de segment et inclut des exemples d’appels d’API pour exécuter des actions de base à l’aide de l’API.

## Prise en main

Les points de terminaison utilisés dans ce guide font partie de l&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes que vous devez connaître pour pouvoir invoquer l&#39;API, y compris les en-têtes requis et pour savoir comment lire des exemples d&#39;appels d&#39;API.

## Obtention d’une liste de définitions de segment {#list}

Vous pouvez obtenir une liste de toutes les définitions de segment de votre organisation IMS en envoyant une requête GET au point de terminaison `/segment/definitions`.

**Format d’API**

Le point de terminaison `/segment/definitions` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est fortement recommandée pour réduire les frais généraux élevés. En passant un appel vers ce point de terminaison sans paramètres, vous récupérerez toutes les définitions de segment disponibles pour votre organisation. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

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
| `sort` | Indique le champ de tri des résultats. Est écrit au format suivant : `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
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

>[!NOTE]
>
>Une expression de définition de segment peut également faire référence à un attribut calculé. Pour en savoir plus, consultez le [guide du point de terminaison de l&#39;API d&#39;attributs calculés](../../profile/computed-attributes/ca-api.md).
>
>La fonctionnalité des attributs calculés est une version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent faire l’objet de modifications.

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

Vous pouvez récupérer des informations détaillées sur une définition de segment spécifique en envoyant une demande de GET au point de terminaison `/segment/definitions` et en indiquant l’identifiant de la définition de segment que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_ID}` | Valeur `id` de la définition de segment à récupérer. |

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

## Récupérer en bloc les définitions de segment {#bulk-get}

Vous pouvez récupérer des informations détaillées sur plusieurs définitions de segment spécifiées en envoyant une requête de POST au point de terminaison `/segment/definitions/bulk-get` et en fournissant les valeurs `id` des définitions de segment dans le corps de la requête.

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

Vous pouvez demander de supprimer une définition de segment spécifique en adressant une requête de DELETE au point de terminaison `/segment/definitions` et en indiquant l’identifiant de la définition de segment que vous souhaitez supprimer dans le chemin de requête.

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

Vous pouvez mettre à jour une définition de segment spécifique en envoyant une requête de PATCH au point de terminaison `/segment/definitions` et en indiquant l’identifiant de la définition de segment que vous souhaitez mettre à jour dans le chemin de requête.

**Format d’API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_ID}` | Valeur `id` de la définition de segment à mettre à jour. |

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

## Conversion de la définition de segment

Vous pouvez convertir une définition de segment entre `pql/text` et `pql/json` ou `pql/json` en `pql/text` en  en adressant une requête de POST au point de terminaison `/segment/conversion`.

**Format d’API**

```http
POST /segment/conversion
```

**Requête**

La demande suivante modifie le format de la définition de segment de `pql/text` en `pql/json`.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
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

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails de votre définition de segment nouvellement convertie.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment fonctionnent les définitions de segment. Pour plus d&#39;informations sur la création d&#39;un segment, consultez le [didacticiel de création d&#39;un segment](../tutorials/create-a-segment.md).

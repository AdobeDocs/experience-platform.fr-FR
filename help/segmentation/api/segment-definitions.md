---
solution: Experience Platform
title: Point d’entrée de l’API des définitions de segment
description: Le point d’entrée des définitions de segment de l’API Segmentation Service de Adobe Experience Platform vous permet de gérer par programmation les définitions de segment pour votre organisation.
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 424702d7d16eddabefe19d023c3829bd650c88ce
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 24%

---

# Point d’entrée des définitions de segment

>[!WARNING]
>
>La création d’audiences à l’aide d’entités B2B avec l’API Segmentation Service est obsolète. Vous ne pouvez plus créer d’audiences à l’aide des entités B2B suivantes : compte, relation compte-personne, campagne, membre de campagne, liste marketing, membre de liste marketing, opportunité et relation opportunité-personne.

Adobe Experience Platform vous permet de créer des définitions de segment qui définissent un groupe d’attributs ou de comportements spécifiques à partir d’un groupe de profils. Une définition de segment est un objet qui encapsule une requête écrite en [!DNL Profile Query Language] (PQL). Les définitions de segment sont appliquées aux profils pour créer des audiences. Cet objet (définition de segment) est également appelé prédicat PQL. Les prédicats de PQL définissent les règles de la définition de segment en fonction des conditions liées aux données d’enregistrement ou de série temporelle que vous fournissez à [!DNL Real-Time Customer Profile]. Pour plus d’informations sur l’écriture de requêtes PQL, reportez-vous au [guide de PQL](../pql/overview.md).

Ce guide fournit des informations pour vous aider à mieux comprendre les définitions de segment et comprend des exemples d’appels API pour exécuter des actions de base à l’aide de l’API .

## Commencer

Les points d’entrée utilisés dans ce guide font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et la manière de lire des exemples d’appels API.

## Obtention d’une liste de définitions de segment {#list}

Vous pouvez récupérer une liste de toutes les définitions de segment pour votre organisation en envoyant une requête GET au point d’entrée `/segment/definitions`.

**Format d’API**

Le point d’entrée `/segment/definitions` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais généraux élevés. Si vous effectuez un appel à ce point d’entrée sans paramètre, toutes les définitions de segment disponibles pour votre organisation sont récupérées. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Paramètres de requête**

+++ Liste des paramètres de requête disponibles.

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `start` | Indique le décalage de départ pour les définitions de segment renvoyées. | `start=4` |
| `limit` | Indique le nombre de définitions de segment renvoyées par page. | `limit=20` |
| `page` | Indique à partir de quelle page commencent les résultats des définitions de segment. | `page=5` |
| `sort` | Indique le champ par lequel trier les résultats. est écrit au format suivant : `[attributeName]:[desc/asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Indique si la définition de segment est activée dans le flux. | `evaluationInfo.continuous.enabled=true` |

+++

**Requête**

La requête suivante récupère les deux dernières définitions de segment publiées au sein de votre organisation.

+++ Exemple de requête pour récupérer une liste de définitions de segment.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de définitions de segment pour l’organisation spécifiée au format JSON.

+++ Exemple de réponse lors de la récupération d’une liste de définitions de segment.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

+++

## Création d’une définition de segment {#create}

Vous pouvez créer une définition de segment en envoyant une requête POST au point d’entrée `/segment/definitions`.

>[!IMPORTANT]
>
>Les définitions de segment créées à l’aide de l’API **ne peuvent pas** peuvent être modifiées dans le créateur de segments.

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

Lors de la création d’une définition de segment, vous pouvez la créer au format `pql/text` ou `pql/json`.

>[!BEGINTABS]

>[!TAB Utilisation de pql/text]

+++ Exemple de requête pour créer une définition de segment.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "schema": {
            "name": "_xdm.context.profile"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom unique par lequel faire référence à la définition de segment. |
| `description` | (Facultatif) Description de la définition de segment que vous êtes en train de créer. |
| `expression` | Une entité qui contient des informations de champs sur la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul « PQL » est pris en charge. |
| `expression.format` | Indique la structure de l’expression en valeur. Les valeurs prises en charge comprennent `pql/text` et `pql/json`. |
| `expression.value` | Une expression conforme au type indiqué dans `expression.format`. |
| `evaluationInfo` | (Facultatif) Type de définition de segment que vous êtes en train de créer. Si vous souhaitez créer un segment par lot, définissez `evaluationInfo.batch.enabled` sur true. Si vous souhaitez créer un segment en flux continu, définissez `evaluationInfo.continuous.enabled` sur « true ». Si vous souhaitez créer un segment Edge, définissez `evaluationInfo.synchronous.enabled` sur true. Si rien n’est indiqué, la définition de segment est créée sous la forme d’un segment **par lot**. |
| `schema` | Schéma associé aux entités du segment. Se compose d’un champ `id` ou `name`. |

+++

>[!TAB Utilisation de pql/json]

+++ Exemple de requête pour créer une définition de segment.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/json",
            "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"a\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}},{\"nodeType\":\"fieldLookup\",\"fieldName\":\"b\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}]}"
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
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string"
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom unique par lequel faire référence à la définition de segment. |
| `description` | (Facultatif) Description de la définition de segment que vous êtes en train de créer. |
| `evaluationInfo` | (Facultatif) Type de définition de segment que vous êtes en train de créer. Si vous souhaitez créer un segment par lot, définissez `evaluationInfo.batch.enabled` sur true. Si vous souhaitez créer un segment en flux continu, définissez `evaluationInfo.continuous.enabled` sur « true ». Si vous souhaitez créer un segment Edge, définissez `evaluationInfo.synchronous.enabled` sur true. Si rien n’est indiqué, la définition de segment est créée sous la forme d’un segment **par lot**. |
| `schema` | Schéma associé aux entités du segment. Se compose d’un champ `id` ou `name`. |
| `expression` | Une entité qui contient des informations de champs sur la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul « PQL » est pris en charge. |
| `expression.format` | Indique la structure de l’expression dans la valeur. |
| `expression.value` | Une expression conforme au type indiqué dans `expression.format`. |

+++

>[!ENDTABS]

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la définition de segment que vous venez de créer.

+++ Exemple de réponse lors de la création d’une définition de segment.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | Identifiant généré par le système de votre définition de segment nouvellement créée. |
| `evaluationInfo` | Objet indiquant le type d’évaluation auquel la définition de segment sera soumise. Il peut s’agir d’une segmentation par lots, en flux continu (également appelée continue) ou Edge (également appelée synchrone). |

+++

## Récupération d’une définition de segment spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une définition de segment spécifique en adressant une requête GET au point d’entrée `/segment/definitions` et en fournissant l’identifiant de la définition de segment que vous souhaitez récupérer dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_ID}` | Valeur `id` de la définition de segment que vous souhaitez récupérer. |

**Requête**

+++ Exemple de requête pour récupérer une définition de segment.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les informations détaillées de la définition de segment spécifiée.

+++ Exemple de réponse lors de la récupération d’une définition de segment.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | Identifiant en lecture seule généré par le système de la définition de segment. |
| `name` | Nom unique par lequel faire référence à la définition de segment. |
| `schema` | Schéma associé aux entités du segment. Se compose d’un champ `id` ou `name`. |
| `expression` | Une entité qui contient des informations de champs sur la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul « PQL » est pris en charge. |
| `expression.format` | Indique la structure de l’expression en valeur. Actuellement, le format suivant est pris en charge : <ul><li>`pql/text` : une représentation textuelle d’une définition de segment, selon la grammaire PQL publiée.  Par exemple : `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Une expression conforme au type indiqué dans `expression.format`. |
| `description` | Une description lisible par l’utilisateur de la définition. |
| `evaluationInfo` | Objet indiquant le type d’évaluation, de lot, de diffusion en continu (également appelée continue) ou d’edge (également appelée synchrone) auquel la définition de segment sera soumise. |

+++

## Récupérer en bloc des définitions de segment {#bulk-get}

Vous pouvez récupérer des informations détaillées sur plusieurs définitions de segment spécifiées en adressant une requête POST au point d’entrée `/segment/definitions/bulk-get` et en fournissant les valeurs `id` des définitions de segment dans le corps de la requête.

**Format d’API**

```http
POST /segment/definitions/bulk-get
```

**Requête**

+++ Exemple de requête lors de l’utilisation du point d’entrée d’obtention en bloc.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Propriété | Description |
| -------- | ----------- |
| `ids` | Un tableau contenant des objets qui indiquent les identifiants des définitions de segment que vous souhaitez récupérer. |

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 207 avec les définitions de segment demandées.

+++ Exemple de réponse lors de l’utilisation du point d’entrée d’obtention en bloc.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
| `id` | Identifiant en lecture seule généré par le système de la définition de segment. |
| `name` | Nom unique par lequel faire référence à la définition de segment. |
| `schema` | Schéma associé aux entités du segment. Se compose d’un champ `id` ou `name`. |
| `expression` | Une entité qui contient des informations de champs sur la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul « PQL » est pris en charge. |
| `expression.format` | Indique la structure de l’expression en valeur. Actuellement, le format suivant est pris en charge : <ul><li>`pql/text` : une représentation textuelle d’une définition de segment, selon la grammaire PQL publiée.  Par exemple : `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Une expression conforme au type indiqué dans `expression.format`. |
| `description` | Une description lisible par l’utilisateur de la définition. |
| `evaluationInfo` | Objet indiquant le type d’évaluation, de lot, de diffusion en continu (également appelée continue) ou d’edge (également appelée synchrone) auquel la définition de segment sera soumise. |

+++

## Suppression d’une définition de segment spécifique {#delete}

Vous pouvez demander la suppression d’une définition de segment spécifique en adressant une requête DELETE au point d’entrée `/segment/definitions` et en fournissant l’identifiant de la définition de segment que vous souhaitez supprimer du chemin de requête.

>[!NOTE]
>
> Une définition de segment utilisée dans une activation de destination **ne peut pas** peut être supprimée.

**Format d’API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_ID}` | Valeur `id` de la définition de segment à supprimer. |

**Requête**

+++ Exemple de requête pour supprimer une définition de segment.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 sans message.

## Mise à jour d’une définition de segment spécifique

Vous pouvez mettre à jour une définition de segment spécifique en adressant une requête PATCH au point d’entrée `/segment/definitions` et en fournissant l’identifiant de la définition de segment que vous souhaitez mettre à jour dans le chemin de requête.

**Format d’API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_ID}` | Valeur `id` de la définition de segment à mettre à jour. |

**Requête**

La requête suivante met à jour le pays de l&#39;adresse professionnelle des États-Unis vers le Canada.

>[!NOTE]
>
>Puisque cet appel API **remplace** le contenu de la définition de segment, assurez-vous **tous** les champs que vous souhaitez conserver sont inclus dans le corps de la requête.

+++ Exemple de requête pour mettre à jour une définition de segment.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la définition de segment que vous venez de mettre à jour.

+++ Exemple de réponse lors de la mise à jour d’une définition de segment.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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

+++

## Convertir la définition de segment

Vous pouvez convertir une définition de segment entre `pql/text` et `pql/json` ou `pql/json` en `pql/text` en effectuant une requête POST vers le point d’entrée `/segment/conversion`.

**Format d’API**

```http
POST /segment/conversion
```

**Requête**

La requête suivante modifie le format de la définition de segment de `pql/text` en `pql/json`.

+++ Exemple de requête pour convertir la définition de segment.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "payloadSchema": "string"
    }'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de votre définition de segment nouvellement convertie.

+++ Exemple de réponse lors de la conversion de la définition de segment.

```json
{
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

+++

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment fonctionnent les définitions de segment. Pour plus d’informations sur la création d’un segment, consultez le tutoriel [création d’un segment](../tutorials/create-a-segment.md).

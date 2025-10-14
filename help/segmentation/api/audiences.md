---
title: Point d’entrée de l’API Audiences
description: Utilisez le point d’entrée audiences dans l’API Adobe Experience Platform Segmentation Service pour créer, gérer et mettre à jour des audiences par programmation pour votre organisation.
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 63fa87ac9777b3ac66d990dd4bfbd202f07b0eba
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 6%

---

# Point d’entrée Audiences

Une audience est un ensemble de personnes qui partagent des comportements et/ou des caractéristiques similaires. Ces collections de personnes peuvent être générées à l’aide de Adobe Experience Platform ou à partir de sources externes. Vous pouvez utiliser le point d’entrée `/audiences` dans l’API Segmentation, ce qui vous permet de récupérer, créer, mettre à jour et supprimer des audiences par programmation.

## Commencer

Les points d’entrée utilisés dans ce guide font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et la manière de lire des exemples d’appels API.

## Récupération d’une liste d’audiences {#list}

Vous pouvez récupérer une liste de toutes les audiences de votre organisation en envoyant une requête GET au point d’entrée `/audiences`.

**Format d’API**

Le point d’entrée `/audiences` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais généraux élevés lors de l’énumération des ressources. Si vous effectuez un appel à ce point d’entrée sans paramètre, toutes les audiences disponibles pour votre organisation seront récupérées. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

>[!NOTE]
>
>Si vous utilisez ce point d’entrée sans paramètres de requête, les audiences inactives ne sont **pas** renvoyées. Cependant, si vous utilisez ce point d’entrée conjointement avec le paramètre de requête `property=audienceId`, les audiences inactives **seront** seront renvoyées.

Les paramètres de requête suivants peuvent être utilisés lors de la récupération d’une liste d’audiences :

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `start` | Indique le décalage de départ pour les audiences renvoyées. | `start=5` |
| `limit` | Indique le nombre maximal d’audiences renvoyées par page. | `limit=10` |
| `sort` | Indique l’ordre de tri des résultats. Il est écrit au format `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Un filtre qui vous permet de spécifier des audiences qui correspondent **exactement** à la valeur d’un attribut. Il est écrit au format `property=` | `property=audienceId==test-audience-id` |
| `name` | Un filtre qui permet de spécifier les audiences dont les noms **contiennent** la valeur fournie. Cette valeur ne respecte pas la casse. | `name=Sample` |
| `description` | Un filtre qui permet de spécifier les audiences dont les descriptions **contiennent** la valeur fournie. Cette valeur ne respecte pas la casse. | `description=Test Description` |
| `entityType` | Un filtre qui vous permet de spécifier le type d’audience que vous recherchez. | `entityType=_xdm.context.account` |

**Requête**

La requête suivante récupère les deux dernières audiences créées dans votre organisation.

+++Exemple de requête pour récupérer une liste d’audiences.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec une liste d’audiences créées dans votre organisation au format JSON.

+++Exemple de réponse contenant les deux dernières audiences créées qui appartiennent à votre organisation

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
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
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "totalPages": 21,
      "sortField": "name",
      "sort": "asc", 
      "pageSize": 5,
      "limit": 5,
      "start": "0",
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| Propriété | Type d’audience | Description |
| -------- | ------------- | ----------- | 
| `id` | Les deux | Identifiant en lecture seule généré par le système pour l’audience. |
| `audienceId` | Les deux | Si l’audience est une audience générée par Platform, il s’agit de la même valeur que la `id`. Si l’audience est générée en externe, cette valeur est fournie par le client. |
| `schema` | Les deux | Schéma du modèle de données d’expérience (XDM) de l’audience. |
| `imsOrgId` | Les deux | Identifiant de l’organisation à laquelle appartient l’audience. |
| `sandbox` | Les deux | Informations sur le sandbox auquel appartient l’audience. Vous trouverez plus d’informations sur les sandbox dans la [présentation des sandbox](../../sandboxes/home.md). |
| `name` | Les deux | Nom de l’audience. |
| `description` | Les deux | Description de l’audience. |
| `expression` | Généré par Platform | Expression Profile Query Language (PQL) de l’audience. Vous trouverez plus d’informations sur les expressions PQL dans le guide des expressions de PQL [&#128279;](../pql/overview.md). |
| `mergePolicyId` | Généré par Platform | L’identifiant de la politique de fusion à laquelle l’audience est associée. Pour plus d’informations sur les politiques de fusion, consultez le [guide des politiques de fusion](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Généré par Platform | Indique comment l’audience sera évaluée. Les méthodes d’évaluation possibles sont par lots, synchrones (diffusion en continu) ou continues (Edge). Vous trouverez plus d’informations sur les méthodes d’évaluation dans la [&#x200B; présentation de la segmentation &#x200B;](../home.md) |
| `dependents` | Les deux | Tableau d’ID d’audience qui dépendent de l’audience actuelle. Cette option est utile si vous créez une audience qui est un segment d’un segment. |
| `dependencies` | Les deux | Tableau d’identifiants d’audience dont dépend l’audience. Cette option est utile si vous créez une audience qui est un segment d’un segment. |
| `type` | Les deux | Champ généré par le système qui indique si l’audience est générée par Platform ou est une audience générée en externe. Les valeurs possibles sont `SegmentDefinition` et `ExternalSegment`. Une `SegmentDefinition` fait référence à une audience générée dans Platform, tandis qu’une `ExternalSegment` fait référence à une audience qui n’a pas été générée dans Platform. |
| `originName` | Les deux | Champ qui fait référence au nom de l’origine de l’audience. Pour les audiences générées par Platform, cette valeur sera `REAL_TIME_CUSTOMER_PROFILE`. Pour les audiences générées dans Audience Orchestration, cette valeur sera `AUDIENCE_ORCHESTRATION`. Pour les audiences générées dans Adobe Audience Manager, cette valeur sera `AUDIENCE_MANAGER`. Pour les autres audiences générées en externe, cette valeur sera `CUSTOM_UPLOAD`. |
| `createdBy` | Les deux | Identifiant de l’utilisateur qui a créé l’audience. |
| `labels` | Les deux | Utilisation des données au niveau de l’objet et libellés de contrôle d’accès basés sur les attributs pertinents pour l’audience. |
| `namespace` | Les deux | Espace de noms auquel appartient l’audience. Les valeurs possibles sont `AAM`, `AAMSegments`, `AAMTraits` et `AEPSegments`. |
| `linkedAudienceRef` | Les deux | Objet contenant des identifiants pour d’autres systèmes liés à l’audience. |

+++

## Création d’une audience {#create}

Vous pouvez créer une audience en effectuant une requête POST vers le point d’entrée `/audiences`.

**Format d’API**

```http
POST /audiences
```

**Requête**

+++ Exemple de requête pour créer une audience générée par Platform

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "AEPSegments",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| Propriété | Description |
| -------- | ----------- | 
| `name` | Nom de l’audience. |
| `description` | Description de l’audience. |
| `type` | Champ qui indique si l’audience est générée par Platform ou si elle est générée de manière externe. Les valeurs possibles sont `SegmentDefinition` et `ExternalSegment`. Une `SegmentDefinition` fait référence à une audience générée dans Platform, tandis qu’une `ExternalSegment` fait référence à une audience qui n’a pas été générée dans Platform. |
| `expression` | Expression Profile Query Language (PQL) de l’audience. Vous trouverez plus d’informations sur les expressions PQL dans le guide des expressions de PQL [&#128279;](../pql/overview.md). |
| `schema` | Schéma du modèle de données d’expérience (XDM) de l’audience. |
| `labels` | Utilisation des données au niveau de l’objet et libellés de contrôle d’accès basés sur les attributs pertinents pour l’audience. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur votre audience nouvellement créée.

+++Exemple de réponse lors de la création d’une audience générée par Platform.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Recherche d’une audience spécifiée {#get}

Vous pouvez rechercher des informations détaillées sur une audience spécifique en adressant une requête GET au point d’entrée `/audiences` et en fournissant l’identifiant de l’audience que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /audiences/{AUDIENCE_ID}
```

| Paramètre | Description |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | Identifiant de l’audience que vous essayez de récupérer. Notez qu’il s’agit du champ `id` et **’est pas** le champ `audienceId`. |

**Requête**

+++Exemple de requête pour récupérer une audience

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur l’audience spécifiée.

+++Exemple de réponse lors de la récupération d’une audience générée par Platform.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Remplacer une audience {#put}

Vous pouvez mettre à jour (remplacer) une audience spécifique en adressant une requête PUT au point d’entrée `/audiences` et en fournissant l’identifiant de l’audience que vous souhaitez mettre à jour dans le chemin de requête.

**Format d’API**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{AUDIENCE_ID}` | Identifiant de l’audience à mettre à jour. Notez qu’il s’agit du champ `id` et **’est pas** le champ `audienceId`. |

**Requête**

+++Exemple de requête pour mettre à jour une audience entière.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-platform-audience-id",
    "name": "New Platform audience",
    "namespace": "AEPSegments",
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country=\"US\""
    }
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| Propriété | Description |
| -------- | ----------- | 
| `audienceId` | Identifiant de l’audience. Pour les audiences générées en externe, cette valeur peut être fournie par l’utilisateur ou l’utilisatrice. |
| `name` | Nom de l’audience. |
| `namespace` | Espace de noms de l’audience. |
| `description` | Description de l’audience. |
| `type` | Champ généré par le système qui indique si l’audience est générée par Platform ou est une audience générée en externe. Les valeurs possibles sont `SegmentDefinition` et `ExternalSegment`. Un `SegmentDefinition` fait référence à une audience générée dans Experience Platform, tandis qu’un `ExternalSegment` fait référence à une audience qui n’a pas été générée dans Experience Platform. |
| `expression` | Objet contenant l’expression PQL de l’audience. |
| `lifecycleState` | Statut de l’audience. Les valeurs possibles sont `draft`, `published` et `inactive`. `draft` représente le moment où l’audience est créée, le moment `published` où elle est publiée et le moment `inactive` où elle n’est plus active. |
| `datasetId` | Identifiant du jeu de données dans lequel se trouvent les données de l’audience. |
| `labels` | Utilisation des données au niveau de l’objet et libellés de contrôle d’accès basés sur les attributs pertinents pour l’audience. |

+++

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec les détails de votre audience nouvellement mise à jour. Notez que les détails de votre audience seront différents selon qu’il s’agit d’une audience générée par Experience Platform ou d’une audience générée en externe.

+++Exemple de réponse lors de la mise à jour d’une audience entière.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Mettre à jour une audience {#patch}

Vous pouvez mettre à jour une audience spécifique en adressant une requête PATCH au point d’entrée `/audiences` et en fournissant l’identifiant de l’audience que vous souhaitez mettre à jour dans le chemin de requête.

**Format d’API**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{AUDIENCE_ID}` | Identifiant de l’audience à mettre à jour. Notez qu’il s’agit du champ `id` et **’est pas** le champ `audienceId`. |

**Requête**

+++ Exemple de requête pour mettre à jour une audience.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "op": "add",
        "path": "/lifecycleState",
        "value": "inactive"
    }
 ]'
```

| Propriété | Description |
| -------- | ----------- |
| `op` | Type d’opération PATCH effectuée. Pour ce point d’entrée, cette valeur est **toujours** `/add`. |
| `path` | Chemin d’accès au champ à mettre à jour. Les champs générés par le système, tels que `id`, `audienceId` et `namespace` **ne peuvent pas** être modifiés. |
| `value` | Nouvelle valeur affectée à la propriété spécifiée dans `path`. |

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec l’audience mise à jour.

+++Exemple de réponse lors de l’application d’un correctif à un champ dans une audience.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab5",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "inactive",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Suppression d’une audience {#delete}

Vous pouvez supprimer une audience spécifique en adressant une requête DELETE au point d’entrée `/audiences` et en fournissant l’identifiant de l’audience que vous souhaitez supprimer du chemin d’accès de la requête.

**Format d’API**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{AUDIENCE_ID}` | Identifiant de l’audience à supprimer. Notez qu’il s’agit du champ `id` et **’est pas** le champ `audienceId`. |

**Requête**

+++ Exemple de requête pour supprimer une audience.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 204 sans message.

## Récupération de plusieurs audiences {#bulk-get}

Vous pouvez récupérer plusieurs audiences en adressant une requête POST au point d’entrée `/audiences/bulk-get` et en fournissant les identifiants des audiences que vous souhaitez récupérer.

**Format d’API**

```http
POST /audiences/bulk-get
```

**Requête**

+++ Exemple de requête pour récupérer plusieurs audiences.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 207 avec des informations sur les audiences demandées.

+++ Exemple de réponse lors de la récupération de plusieurs audiences.

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
         "evaluationInfo": {
            "batch": {
               "enabled": false
            },
            "continuous": {
               "enabled": true
            },
            "synchronous": {
               "enabled": false
            }
         },
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
         "dependents": [],
         "definedOn": [
            {
               "meta:resourceType": "unions",
               "meta:containerId": "tenant",
               "$ref": "https://ns.adobe.com/xdm/context/profile__union"
            }
         ],
         "dependencies": [],
         "type": "SegmentDefinition",
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++


## Étapes suivantes

Vous êtes arrivé au bout de ce guide. À présent, vous comprenez mieux comment créer, gérer et supprimer des audiences à l’aide de l’API Adobe Experience Platform. Pour plus d’informations sur la gestion des audiences à l’aide de l’interface utilisateur, consultez le [&#x200B; guide de l’interface utilisateur de segmentation](../ui/overview.md).

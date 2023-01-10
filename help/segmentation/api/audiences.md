---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Segmentation Service;audiences;audience;API;api;
title: Point de terminaison de l’API Audiences
description: Le point de terminaison d’audiences dans l’API Adobe Experience Platform Segmentation Service vous permet de gérer par programmation les audiences pour votre organisation.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 9%

---

# Point de terminaison Audiences

>[!IMPORTANT]
>
>Le point de terminaison de l’audience est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Une audience est un groupe de personnes qui partagent des comportements et/ou des caractéristiques similaires. Ces collections de personnes peuvent être générées à l’aide de Adobe Experience Platform ou à partir de sources externes. Vous pouvez utiliser la variable `/audiences` point de terminaison dans l’API Segmentation, qui vous permet de récupérer, créer, mettre à jour et supprimer des audiences par programmation.

## Prise en main

Les points d’entrée d’API utilisés dans ce guide font partie de l’[!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, veuillez consulter la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels à l’API, notamment les en-têtes requis et la lecture d’exemples d’appels API.

## Récupération d’une liste d’audiences {#list}

Vous pouvez récupérer une liste de toutes les audiences de votre organisation en adressant une demande de GET à la fonction `/audiences` point de terminaison .

**Format d’API**

Le point d’entrée `/audiences` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais de gestion élevés lors de l’inscription de ressources. Si vous effectuez un appel vers ce point de terminaison sans paramètres, toutes les audiences disponibles pour votre organisation seront récupérées. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

Les paramètres de requête suivants peuvent être utilisés lors de la récupération d’une liste d’audiences :

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `start` | Indique le décalage de début pour les audiences renvoyées. | `start=5` |
| `limit` | Indique le nombre maximal d’audiences renvoyées par page. | `limit=10` |
| `sort` | Spécifie l’ordre de tri des résultats. Il est écrit au format `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Filtre permettant de spécifier des audiences qui **what** correspondent à la valeur d’un attribut. Il est écrit au format `property=` | `property=audienceId==test-audience-id` |
| `name` | Filtre permettant de spécifier des audiences dont les noms sont **contain** la valeur fournie. Cette valeur n’est pas sensible à la casse. | `name=Sample` |
| `description` | Filtre permettant de spécifier les audiences dont les descriptions **contain** la valeur fournie. Cette valeur n’est pas sensible à la casse. | `description=Test Description` |
| `withMetrics` | Filtre qui renvoie les mesures en plus des audiences. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>Pour les audiences, les mesures sont renvoyées sous la variable `metrics` et contient des informations sur le nombre de profils, la création et la mise à jour des horodatages.

**Aucune mesure**

La paire requête/réponse suivante est utilisée lorsque la variable `withMetrics` le paramètre de requête n’est pas présent.

**Requête**

La requête suivante récupère les cinq dernières audiences créées dans votre organisation.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**Réponse** {#no-metrics}

Une réponse réussie renvoie un état HTTP 200 avec une liste des audiences créées dans votre organisation au format JSON.

>[!NOTE]
>
>La réponse suivante a été tronquée pour l’espace et affiche uniquement la première audience renvoyée.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
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
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| Propriété | Type d’audience | Description |
| -------- | ------------- | ----------- | 
| `id` | Les deux | Identifiant en lecture seule généré par le système pour l’audience. |
| `audienceId` | Les deux | Si l’audience est une audience générée par Platform, il s’agit de la même valeur que la variable `id`. Si l’audience est générée en externe, cette valeur est fournie par le client. |
| `schema` | Les deux | Schéma du modèle de données d’expérience (XDM) de l’audience. |
| `imsOrgId` | Les deux | ID de l’organisation à laquelle appartient l’audience. |
| `sandbox` | Les deux | Informations sur l’environnement de test auquel l’audience appartient. Vous trouverez plus d’informations sur les environnements de test dans la section [Présentation des environnements de test](../../sandboxes/home.md). |
| `name` | Les deux | Nom de l’audience. |
| `description` | Les deux | Description de l’audience. |
| `expression` | Généré par la plateforme | L’expression PQL (Profile Query Language) de l’audience. Vous trouverez plus d’informations sur les expressions PQL dans la section [Guide des expressions PQL](../pql/overview.md). |
| `mergePolicyId` | Généré par la plateforme | Identifiant de la stratégie de fusion à laquelle l’audience est associée. Pour plus d’informations sur les stratégies de fusion, consultez le [guide des stratégies de fusion](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Généré par la plateforme | Affiche la manière dont l’audience sera évaluée. Les méthodes d’évaluation possibles sont les suivantes : lot, diffusion en continu ou périphérie. Vous trouverez plus d’informations sur les méthodes d’évaluation dans la section [présentation de la segmentation](../home.md) |
| `dependents` | Les deux | Tableau d’identifiants d’audience qui dépendent de l’audience actuelle. Cela serait utilisé si vous créez une audience qui est un segment d’un segment. |
| `dependencies` | Les deux | Tableau d’identifiants d’audience dont dépend l’audience. Cela serait utilisé si vous créez une audience qui est un segment d’un segment. |
| `type` | Les deux | Champ généré par le système qui affiche si l’audience est générée par Platform ou est générée en externe. Les valeurs possibles sont les suivantes : `SegmentDefinition` et `ExternalAudience`. A `SegmentDefinition` fait référence à une audience qui a été générée dans Platform, tandis qu’une `ExternalAudience` fait référence à une audience qui n’a pas été générée dans Platform. |
| `createdBy` | Les deux | L’identifiant de l’utilisateur qui a créé l’audience. |
| `labels` | Les deux | Utilisation des données au niveau de l’objet et libellés de contrôle d’accès basés sur des attributs pertinents pour l’audience. |
| `namespace` | Les deux | Espace de noms auquel l’audience appartient. Les valeurs possibles sont les suivantes : `AAM`, `AAMSegments`, `AAMTraits`, et `AEPSegments`. |
| `audienceMeta` | Externe | Métadonnées créées en externe à partir de l’audience créée en externe. |

**Avec des mesures**

La paire requête/réponse suivante est utilisée lorsque la variable `withMetrics` le paramètre de requête est présent.

**Requête**

La requête suivante récupère les cinq dernières audiences, avec des mesures, créées dans votre entreprise.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste d’audiences, avec des mesures, pour l’organisation spécifiée sous JSON.

>[!NOTE]
>
>La réponse suivante a été tronquée pour l’espace et affiche uniquement la première audience renvoyée.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
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
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "existing": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

Les propriétés suivantes sont répertoriées **exclusive** au `withMetrics` réponse. Si vous souhaitez connaître les propriétés de l’audience standard, veuillez lire le [section précédente](#no-metrics).

| Propriété | Description |
| -------- | ----------- |
| `metrics.imsOrgId` | ID d’organisation de l’audience. |
| `metrics.sandbox` | Informations de l’environnement de test relatives à l’audience. |
| `metrics.jobId` | Identifiant de la tâche de segmentation qui traite l’audience. |
| `metrics.type` | Type de tâche de segmentation. Cela peut être : `export` ou `batch_segmentation`. |
| `metrics.id` | Identifiant de l’audience. |
| `metrics.data` | Mesures liées à l’audience. Cela inclut des informations telles que le nombre total de profils inclus dans l’audience, le nombre total de profils par espace de noms et le nombre total de profils par état. |
| `metrics.createEpoch` | Horodatage indiquant le moment où l’audience a été créée. |
| `metrics.updateEpoch` | Horodatage indiquant le moment où l’audience a été mise à jour pour la dernière fois. |

## Création d’une audience {#create}

Vous pouvez créer une audience en adressant une requête de POST à la fonction `/audiences` point de terminaison .

**Format d’API**

```http
POST /audiences
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
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
| `type` | Champ qui affiche si l’audience est générée par Platform ou est générée de l’extérieur. Les valeurs possibles sont les suivantes : `SegmentDefinition` et `ExternalAudience`. A `SegmentDefinition` fait référence à une audience qui a été générée dans Platform, tandis qu’une `ExternalAudience` fait référence à une audience qui n’a pas été générée dans Platform. |
| `expression` | L’expression PQL (Profile Query Language) de l’audience. Vous trouverez plus d’informations sur les expressions PQL dans la section [Guide des expressions PQL](../pql/overview.md). |
| `schema` | Schéma du modèle de données d’expérience (XDM) de l’audience. |
| `labels` | Utilisation des données au niveau de l’objet et libellés de contrôle d’accès basés sur des attributs pertinents pour l’audience. |

**Réponse**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Recherche d’une audience spécifique {#get}

Vous pouvez rechercher des informations détaillées sur une audience spécifique en adressant une requête de GET à la fonction `/audiences` point de terminaison et en fournissant l’identifiant de l’audience que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| Paramètre | Description |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | L’identifiant de l’audience que vous essayez de récupérer. |
| `property=withmetrics==true` | Paramètre de requête facultatif que vous pouvez utiliser si vous souhaitez récupérer une audience spécifiée avec les mesures d’audience. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur l’audience spécifiée. La réponse varie selon que l’audience est générée avec Adobe Experience Platform ou des sources externes.

**Généré par la plateforme**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**Généré de manière externe**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Mise à jour d’un champ dans une audience {#update-field}

Vous pouvez mettre à jour les champs d’une audience spécifique en adressant une requête de PATCH au `/audiences` et en indiquant l’identifiant de l’audience que vous souhaitez mettre à jour dans le chemin d’accès de la requête.

**Format d’API**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{AUDIENCE_ID}` | L’identifiant de l’audience que vous souhaitez mettre à jour. |

**Requête**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Propriété | Description |
| -------- | ----------- |
| `op` | Pour la mise à jour des audiences, cette valeur est toujours `add`. |
| `path` | Chemin d’accès du champ que vous souhaitez mettre à jour. |
| `value` | Valeur vers laquelle vous souhaitez mettre à jour le champ. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur votre audience nouvellement mise à jour.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
        "value": "workAddress.country = \"CA\""
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
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Mettre à jour une audience {#put}

Vous pouvez mettre à jour (remplacer) une audience spécifique en adressant une requête de PUT à la variable `/audiences` et en indiquant l’identifiant de l’audience que vous souhaitez mettre à jour dans le chemin d’accès de la requête.

**Format d’API**

```http
PUT /audiences/{AUDIENCE_ID}
```

**Requête**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| Propriété | Description |
| -------- | ----------- | 
| `audienceId` | ID de l’audience. Utilisé par des audiences externes |
| `name` | Nom de l’audience. |
| `namespace` |  |
| `description` | Description de l’audience. |
| `type` | Champ généré par le système qui affiche si l’audience est générée par Platform ou est générée en externe. Les valeurs possibles sont les suivantes : `SegmentDefinition` et `ExternalAudience`. A `SegmentDefinition` fait référence à une audience qui a été générée dans Platform, tandis qu’une `ExternalAudience` fait référence à une audience qui n’a pas été générée dans Platform. |
| `lifecycle` | État de l’audience. Les valeurs possibles sont les suivantes : `draft`, `published`, `inactive`, et `archived`. `draft` représente le moment où l’audience est créée, `published` lorsque l’audience est publiée, `inactive` lorsque l’audience n’est plus principale, et `archived` si l’audience est supprimée. |
| `datasetId` | L’identifiant du jeu de données que les données d’audience peuvent être trouvées. |
| `labels` | Utilisation des données au niveau de l’objet et libellés de contrôle d’accès basés sur des attributs pertinents pour l’audience. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de l’audience que vous venez de mettre à jour. Notez que les détails de votre audience diffèrent selon qu’il s’agit d’une audience générée par Platform ou d’une audience générée de l’extérieur.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Suppression d’une audience {#delete}

Vous pouvez supprimer une audience spécifique en adressant une requête de DELETE à la fonction `/audiences` et en indiquant l’identifiant de l’audience que vous souhaitez supprimer dans le chemin d’accès de la requête.

**Format d’API**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{AUDIENCE_ID}` | L’identifiant de l’audience que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 sans message.

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Appliquer les stratégies d’utilisation des données à l’aide de l’API de service de stratégie
topic: enforcement
translation-type: tm+mt
source-git-commit: 3e5245a718295cc5318c277a5cf9ee71da2a911b

---


# Appliquer les stratégies d’utilisation des données à l’aide de l’API de service de stratégie

Une fois que vous avez créé des libellés d’utilisation des données pour vos données et que vous avez créé des stratégies d’utilisation pour les actions marketing à l’égard de ces libellés, vous pouvez utiliser l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service pour évaluer si une action marketing effectuée sur un jeu de données ou un groupe arbitraire de libellés constitue une violation de la stratégie. Vous pouvez ensuite configurer vos propres protocoles internes pour gérer les violations de stratégie en fonction de la réponse de l’API.

>[!NOTE] Par défaut, seules les stratégies dont l’état est défini sur `ENABLED` peuvent participer à l’évaluation. Pour autoriser `DRAFT` les stratégies à participer à l’évaluation, vous devez inclure le paramètre  `includeDraft=true` dans le chemin de requête.

Ce décrit la procédure à suivre pour utiliser l’API Service de stratégie afin de rechercher les violations de stratégie dans différents scénarios.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des concepts clés suivants, qui sont impliqués dans l’application des politiques DULE :

* [Gouvernance](../home.md)des données : Cadre selon lequel la plateforme applique la conformité à l’utilisation des données.
   * [Libellés](../labels/overview.md)d’utilisation des données : Les étiquettes d’utilisation des données sont appliquées aux jeux de données (et/ou aux champs individuels de ces jeux de données), en spécifiant les restrictions d’utilisation de ces données.
   * [Stratégies](../policies/overview.md)d’utilisation des données : Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing autorisées ou restreintes pour certains ensembles de libellés DULE.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Avant de commencer ce didacticiel, veuillez consulter le guide [du](../api/getting-started.md) développeur pour obtenir des informations importantes que vous devez connaître afin d’effectuer des appels à l’API du service de stratégie DULE, y compris les en-têtes requis et pour savoir comment lire des exemples d’appels d’API.

## Evaluer à l’aide des libellés DULE et d’une action marketing

Vous pouvez évaluer une stratégie en testant une action marketing par rapport à un ensemble de libellés DULE qui seraient éventuellement présents dans un jeu de données. Pour ce faire, utilisez le paramètre `duleLabels` , où les étiquettes DOLE sont fournies sous forme de de valeurs séparées par des virgules, comme illustré dans l’exemple ci-dessous.

**Format API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing associée à la stratégie DULE que vous évaluez. |
| `{LABEL_1}` | Libellé d’utilisation des données pour tester l’action marketing. Au moins une étiquette doit être fournie. Lorsque vous fournissez plusieurs étiquettes, elles doivent être séparées par des virgules. |

**Requête**

La requête suivante teste l’action `exportToThirdParty` marketing par rapport aux libellés `C1` et `C3`. Puisque la stratégie d’utilisation des données que vous avez créée précédemment dans ce didacticiel définit le `C1` libellé comme l’une des `deny` conditions de sa stratégie  , l’action marketing doit déclencher une violation de la stratégie.

>[!NOTE] Les libellés d’utilisation des données sont sensibles à la casse. Les violations de stratégie ne se produisent que lorsque les libellés définis dans leur  de stratégie sont mis en correspondance exacte avec les . Dans cet exemple, une `C1` étiquette déclencherait une violation, contrairement à une `c1` étiquette.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’URL de l’action marketing, les étiquettes DULE sur lesquelles elle a été testée et un de toute stratégie DULE violée suite au test de l’action par rapport à ces étiquettes. Dans cet exemple, la stratégie &quot;Exporter les données vers un tiers&quot; s’affiche dans le `violatedPolicies` tableau, indiquant que l’action marketing a déclenché la violation de stratégie attendue.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `violatedPolicies` | Tableau répertoriant toutes les stratégies DULE violées en testant l&#39;action marketing (spécifiée dans `marketingActionRef`) par rapport aux stratégies fournies `duleLabels`. |

## Évaluer à l’aide de jeux de données

Vous pouvez évaluer une stratégie DULE en testant une action marketing par rapport à un ou plusieurs jeux de données à partir desquels les étiquettes DULE peuvent être collectées. Pour ce faire, il effectue une requête POST auprès `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` et fournit des ID de jeu de données au sein du corps de la requête, comme illustré dans l’exemple ci-dessous.

**Format API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing associée à la stratégie DULE que vous évaluez. |

**Requête**

La requête suivante teste l’action `exportToThirdParty` marketing par rapport à trois jeux de données différents. Les jeux de données sont référencés par type et ID dans un tableau fourni dans la charge utile.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5c423dc25f2f2e00005e2319"
    },
    {
      "entityType": "dataSet",
      "entityId": "5cc323e15410ef14b749481e"
    },
    {
      "entityType": "dataSet",
      "entityId": "5cc1fb685410ef14b748c55f"
    }
  ]'
```

| Propriété | Description |
| --- | --- |
| `entityType` | Chaque élément du tableau de charge utile doit indiquer le type d&#39;entité en cours de définition. Dans ce cas d’utilisation, la valeur sera toujours &quot;dataSet&quot;. |
| `entityId` | Chaque élément du tableau de charge doit fournir l’identifiant unique d’un jeu de données. |

**Réponse**

Une réponse réussie renvoie l’URL de l’action marketing, les étiquettes DULE collectées à partir des jeux de données fournis et un de toute stratégie DULE violée suite au test de l’action par rapport à ces étiquettes. Dans cet exemple, la stratégie &quot;Exporter les données vers un tiers&quot; s’affiche dans le `violatedPolicies` tableau, indiquant que l’action marketing a déclenché la violation de stratégie attendue.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `duleLabels` | de libellés DULE extraits des jeux de données fournis dans la charge utile de requête. |
| `discoveredLabels` |  des jeux de données fournis dans la charge utile de la demande, affichant les étiquettes de niveau jeu de données et de niveau champ DULE trouvées dans chacun d’eux. |
| `violatedPolicies` | Tableau répertoriant toutes les stratégies DULE violées en testant l&#39;action marketing (spécifiée dans `marketingActionRef`) par rapport aux stratégies fournies `duleLabels`. |

## Étapes suivantes

En lisant ce , vous avez réussi à rechercher des violations de stratégie lors de l’exécution d’une action marketing sur un jeu de données ou un ensemble de libellés DULE. En utilisant les données renvoyées dans les réponses de l’API, vous pouvez configurer des protocoles dans votre application d’expérience afin d’appliquer correctement les violations de stratégie lorsqu’elles se produisent.

Pour savoir comment appliquer des stratégies d’utilisation des données pour  segments  en temps réel dans le de clients, reportez-vous au [didacticiel](../../segmentation/tutorials/governance.md)suivant.
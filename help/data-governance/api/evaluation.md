---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Stratégies
topic: developer guide
description: Une fois les actions marketing créées et les stratégies définies, vous pouvez utiliser l’API Policy Service pour déterminer si certaines actions ne respectent pas les stratégies. Les contraintes renvoyées prennent la forme d’un ensemble de stratégies qui seraient enfreintes si l’action marketing était appliquée aux données spécifiées contenant les libellés d’utilisation des données.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 17%

---


# Points de terminaison de l&#39;évaluation des politiques

Once marketing actions have been created and policies have been defined, you can use the [!DNL Policy Service] API to evaluate if any policies are violated by certain actions. Les contraintes renvoyées prennent la forme d’un ensemble de stratégies qui seraient enfreintes si l’action marketing était appliquée aux données spécifiées contenant les libellés d’utilisation des données.

By default, only policies whose status is set to `ENABLED` participate in evaluation. Cependant, vous pouvez utiliser le paramètre de requête `?includeDraft=true` pour inclure `DRAFT` des stratégies dans l’évaluation.

Les requêtes d’évaluation peuvent être effectuées de trois façons :

1. Compte tenu d’une action marketing et d’un ensemble d’étiquettes d’utilisation des données, l’action enfreint-elle des stratégies ?
1. Compte tenu d’une action marketing et d’un ou de plusieurs jeux de données, l’action enfreint-elle des stratégies ?
1. Compte tenu d’une action marketing, d’un ou de plusieurs jeux de données et d’un sous-ensemble d’un ou de plusieurs champs de chacun de ces jeux de données, l’action est-elle contraire à des stratégies ?

## Prise en main

The API endpoints used in this guide is part of the [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Avant de continuer, consultez le guide [de](./getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute [!DNL Experience Platform] API.

## Evaluer les violations de stratégie à l’aide de libellés d’utilisation des données {#labels}

Vous pouvez évaluer les violations de stratégie en fonction de la présence d’un ensemble spécifique d’étiquettes d’utilisation des données à l’aide du paramètre `duleLabels` requête dans une demande de GET.

**Format d’API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à tester par rapport à un ensemble d’étiquettes d’utilisation des données. Vous pouvez récupérer une liste d’actions marketing disponibles en envoyant une demande de [GET au point de terminaison](./marketing-actions.md#list)des actions marketing. |
| `{LABELS_LIST}` | Liste de noms d’utilisation des données séparés par des virgules pour tester l’action marketing. Par exemple : `duleLabels=C1,C2,C3`<br><br>Notez que les noms d’étiquette sont sensibles à la casse. Assurez-vous d’utiliser la bonne casse lorsque vous les répertoriez dans le `duleLabels` paramètre. |

**Requête**

L’exemple de requête ci-dessous évalue une action marketing en fonction des libellés C1 et C3.

>[!IMPORTANT]
>
>Tenez compte des opérateurs `AND` et `OR` dans l’expression des stratégies. In the example below, if either label (`C1` or `C3`) had appeared alone in the request, the marketing action would not have violated this policy. It takes both labels (`C1` and `C3`) to return the violated policy. Assurez-vous d’évaluer soigneusement les stratégies et de bien définir l’expression des stratégies.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive comprend un `violatedPolicies` tableau, qui contient les détails des stratégies violées suite à l&#39;exécution de l&#39;action marketing par rapport aux étiquettes fournies. If no policies are violated, the `violatedPolicies` array will be empty.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
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
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## Evaluer les violations de stratégie à l’aide de jeux de données {#datasets}

Vous pouvez évaluer les violations de stratégie en fonction d’un ensemble de jeux de données à partir desquels des étiquettes d’utilisation de données peuvent être collectées. Pour ce faire, il exécute une requête de POST sur le point de `/constraints` terminaison pour une action marketing spécifique et fournit une liste d’ID de jeu de données dans le corps de la requête.

**Format d’API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à tester par rapport à un ou plusieurs jeux de données. Vous pouvez récupérer une liste d’actions marketing disponibles en envoyant une demande de [GET au point de terminaison](./marketing-actions.md#list)des actions marketing. |

**Requête**

La requête suivante exécute l’action `crossSiteTargeting` marketing sur un ensemble de trois jeux de données afin d’évaluer les violations de stratégie.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
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
| `entityType` | Type d’entité dont l’ID est indiqué dans la propriété `entityId` frère. Actuellement, la seule valeur acceptée est `dataSet`. |
| `entityId` | ID d’un jeu de données par rapport auquel tester l’action marketing. Une liste de jeux de données et de leurs identifiants correspondants peut être obtenue en adressant une demande de GET au point de `/dataSets` terminaison dans l’ [!DNL Catalog Service] API. Pour plus d’informations, consultez le guide sur la [ [!DNL Catalog] liste des objets](../../catalog/api/list-objects.md) . |

**Réponse**

Une réponse réussie comprend un `violatedPolicies` tableau, qui contient les détails des stratégies violées suite à l&#39;exécution de l&#39;action marketing par rapport aux jeux de données fournis. If no policies are violated, the `violatedPolicies` array will be empty.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
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
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `duleLabels` | L’objet de la réponse comprend un tableau `duleLabels` qui contient une liste consolidée de tous les libellés trouvés dans les jeux de données spécifiés. Cette liste inclut des libellés de jeu de données et de champ pour tous les champs du jeu de données. |
| `discoveredLabels` | La réponse comprend également un tableau `discoveredLabels` contenant des objets pour chaque jeu de données, divisant les `datasetLabels` entre les libellés de jeu de données et les libellés de champ. Chaque libellé de champ indique le chemin d’accès au champ spécifique portant ce libellé. |

## Evaluer les violations de stratégie à l’aide de champs de jeux de données spécifiques {#fields}

Vous pouvez évaluer les violations de stratégie en fonction d’un sous-ensemble de champs d’un ou de plusieurs jeux de données, de sorte que seuls les libellés d’utilisation des données appliqués à ces champs soient évalués.

Lors de l’évaluation des stratégies à l’aide de champs de jeu de données, considérez les points suivants :

* **Les noms de champ respectent** la casse : Lorsque vous fournissez des champs, ils doivent être écrits exactement comme ils apparaissent dans le jeu de données (par exemple, `firstName` vs `firstname`).
* **Héritage** d&#39;étiquette du jeu de données : Les champs individuels d’un jeu de données héritent des étiquettes qui ont été appliquées au niveau du jeu de données. Si vos évaluations de stratégie ne reviennent pas comme prévu, veillez à rechercher les étiquettes qui ont pu être héritées du niveau des jeux de données vers les champs, en plus de celles appliquées au niveau des champs.

**Format d’API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à tester par rapport à un sous-ensemble de champs de jeux de données. Vous pouvez récupérer une liste d’actions marketing disponibles en envoyant une demande de [GET au point de terminaison](./marketing-actions.md#list)des actions marketing. |

**Requête**

La requête suivante teste l’action marketing `crossSiteTargeting` sur un ensemble spécifique de champs appartenant à trois jeux de données. La charge utile est similaire à une demande d’ [évaluation impliquant uniquement des jeux de données](#datasets), ajoutant des champs spécifiques pour chaque jeu de données à partir desquels collecter des étiquettes.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| Propriété | Description |
| --- | --- |
| `entityType` | Type d’entité dont l’ID est indiqué dans la propriété `entityId` frère. Actuellement, la seule valeur acceptée est `dataSet`. |
| `entityId` | ID d’un jeu de données dont les champs doivent être évalués par rapport à l’action marketing. Une liste de jeux de données et de leurs identifiants correspondants peut être obtenue en adressant une demande de GET au point de `/dataSets` terminaison dans l’ [!DNL Catalog Service] API. Pour plus d’informations, consultez le guide sur la [ [!DNL Catalog] liste des objets](../../catalog/api/list-objects.md) . |
| `entityMeta.fields` | Tableau de chemins d’accès à des champs spécifiques dans le schéma du jeu de données, fourni sous la forme de chaînes de pointeur JSON. Consultez la section sur le pointeur [](../../landing/api-fundamentals.md#json-pointer) JSON du guide des fondamentaux de l’API pour plus d’informations sur la syntaxe acceptée pour ces chaînes. |

**Réponse**

Une réponse réussie comprend un `violatedPolicies` tableau, qui contient les détails des stratégies qui ont été violées suite à l&#39;exécution de l&#39;action marketing par rapport aux champs du jeu de données fournis. If no policies are violated, the `violatedPolicies` array will be empty.

En comparant l&#39;exemple de réponse ci-dessous à la [réponse impliquant uniquement des jeux de données](#datasets), notez que la liste des étiquettes collectées est plus courte. Les données `discoveredLabels` de chaque jeu ont également été réduites, car elles incluent uniquement les champs spécifiés dans le corps de la demande. En outre, la stratégie précédemment violée `Targeting Ads or Content` exige que les deux `C4 AND C6` étiquettes soient présentées et n&#39;est donc plus violée, comme indiqué par le tableau vide `violatedPolicies` .

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
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
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
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
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## Évaluer les stratégies en bloc {#bulk}

Le `/bulk-eval` point de terminaison vous permet d’exécuter plusieurs tâches d’évaluation dans un seul appel d’API.

**Format d’API**

```http
POST /bulk-eval
```

**Requête**

La charge utile d&#39;une demande d&#39;évaluation en masse doit être un tableau d&#39;objets ; un pour chaque tâche d&#39;évaluation à exécuter. Pour les tâches qui sont évaluées en fonction de jeux de données et de champs, un `entityList` tableau doit être fourni. Pour les tâches qui sont évaluées en fonction des étiquettes d’utilisation des données, un `labels` tableau doit être fourni.

>[!WARNING]
>
>Si une tâche d’évaluation répertoriée contient à la fois un tableau `entityList` et un `labels` tableau, une erreur se produit. Si vous souhaitez évaluer la même action marketing en fonction des jeux de données et des étiquettes, vous devez inclure des tâches d’évaluation distinctes pour cette action marketing.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| Propriété | Description |
| --- | --- |
| `evalRef` | URI de l’action marketing à tester par rapport aux étiquettes ou aux jeux de données en cas de violation de stratégie. |
| `includeDraft` | Par défaut, seules les stratégies activées participent à l’évaluation. Si `includeDraft` est défini sur `true`, les stratégies qui sont en `DRAFT` état y participent également. |
| `labels` | Tableau d’étiquettes d’utilisation des données pour tester l’action marketing.<br><br>**IMPORTANT**: Lors de l’utilisation de cette propriété, une `entityList` propriété ne doit PAS être incluse dans le même objet. Pour évaluer la même action marketing à l’aide de jeux de données et/ou de champs, vous devez inclure un objet distinct dans la charge utile de requête qui contient un `entityList` tableau. |
| `entityList` | Tableau de jeux de données et de champs (facultatifs) spécifiques à ces jeux de données pour tester l’action marketing.<br><br>**IMPORTANT**: Lors de l’utilisation de cette propriété, une `labels` propriété ne doit PAS être incluse dans le même objet. Pour évaluer la même action marketing à l’aide de libellés d’utilisation de données spécifiques, vous devez inclure un objet distinct dans la charge utile de requête qui contient un `labels` tableau. |
| `entityType` | Type d&#39;entité par lequel tester l&#39;action marketing. Actuellement, seul `dataSet` est pris en charge. |
| `entityId` | ID d’un jeu de données par rapport auquel tester l’action marketing. |
| `entityMeta.fields` | (Facultatif) liste de champs spécifiques dans le jeu de données pour tester l’action marketing. |

**Réponse**

Une réponse positive renvoie un ensemble de résultats d&#39;évaluation ; une pour chaque tâche d’évaluation de stratégie envoyée dans la demande.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{IMS_ORG}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## Évaluation des politiques [!DNL Real-time Customer Profile]

The [!DNL Policy Service] API can also be used to check for policy violations involving the use of [!DNL Real-time Customer Profile] segments. Pour plus d’informations, consultez le tutoriel sur l’[application de la conformité à l’utilisation des données pour les segments d’audience](../../segmentation/tutorials/governance.md).
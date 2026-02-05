---
keywords: Experience Platform;accueil;rubriques populaires;Application des politiques;Application automatique;Application basée sur les API;gouvernance des données
solution: Experience Platform
title: Points d’entrée de l’API Policy Evaluation
description: Une fois les actions marketing créées et les politiques définies, vous pouvez utiliser l’API Policy Service pour déterminer si certaines actions ne respectent pas les politiques. Les contraintes renvoyées prennent la forme d’un ensemble de politiques qui seraient enfreintes si l’action marketing était appliquée aux données spécifiées contenant les libellés d’utilisation des données.
role: Developer
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: f8995ff1e460038b0e254cb500a6d23badeaa991
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 98%

---

# Points d’entrée de l’évaluation des politiques

Une fois les actions marketing créées et les politiques d’utilisation des données définies, vous pouvez utiliser l’API [!DNL Policy Service] pour déterminer si certaines actions sont en violation des politiques. Les contraintes renvoyées prennent la forme d’un ensemble de politiques qui seraient enfreintes si l’action marketing était appliquée aux données spécifiées contenant les libellés d’utilisation des données.

Par défaut, seules les politiques dont l’état est défini sur `ENABLED` participent à l’évaluation. Vous pouvez cependant utiliser le paramètre de requête `?includeDraft=true` pour inclure des politiques `DRAFT` dans l’évaluation.

Les requêtes d’évaluation peuvent être effectuées de trois façons :

1. Étant donné une action marketing et un ensemble de libellés d’utilisation des données, l’action enfreint-elle des politiques ?
1. Étant donné une action marketing et un ou plusieurs jeux de données, l’action enfreint-elle des politiques ?
1. Étant donné une action marketing, un ou plusieurs jeux de données et un sous-ensemble comprenant un ou plusieurs champs dans chaque jeu de données, l’action enfreint-elle des politiques ?

## Prise en main

Les points d’entrée d’API utilisés dans ce guide font partie de l’[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Évaluation des violations de politique à l’aide de libellés d’utilisation des données {#labels}

Vous pouvez évaluer les violations de politique en fonction de la présence d’un ensemble spécifique de libellés d’utilisation des données à l’aide du paramètre de requête `duleLabels` dans une requête GET.

**Format d’API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à tester en fonction d’un ensemble de libellés d’utilisation des données. Vous pouvez récupérer une liste d’actions marketing disponibles en effectuant une [requête GET au point d’entrée des actions marketing](./marketing-actions.md#list). |
| `{LABELS_LIST}` | Liste de noms de libellés d’utilisation des données séparés par des virgules en fonction desquels tester l’action marketing. Par exemple : `duleLabels=C1,C2,C3`<br><br>Notez que les noms de libellés sont sensibles à la casse. Assurez-vous d’utiliser la casse appropriée lorsque vous les répertoriez dans le paramètre `duleLabels`. |

**Requête**

L’exemple de requête ci-dessous évalue une action marketing en fonction des libellés C1 et C3.

>[!IMPORTANT]
>
>Tenez compte des opérateurs `AND` et `OR` dans l’expression des politiques. Dans l’exemple ci-dessous, si l’un des libellés (`C1` ou `C3`) était apparu seul dans la requête, l’action marketing n’aurait pas enfreint cette politique. Les deux libellés (`C1` et `C3`) sont nécessaires pour renvoyer la politique enfreinte. Assurez-vous d’évaluer soigneusement les politiques et de bien définir l’expression des politiques.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie comprend un tableau `violatedPolicies`, qui contient les détails des politiques enfreintes suite à l’exécution de l’action marketing par rapport aux libellés fournis. Si aucune politique n’est enfreinte, le tableau `violatedPolicies` apparaît vide.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## Évaluation des violations de politique à l’aide de jeux de données {#datasets}

>[!WARNING]
>
>Le point d’entrée `/constraints` pour l’évaluation basée sur un jeu de données est obsolète. Pour évaluer une violation de politique ou effectuer plusieurs tâches d’évaluation, utilisez plutôt l’API [bulk evaluation API (`/bulk-eval`)](#bulk).

Vous pouvez évaluer les violations de politique en fonction d’un ensemble constitué d’un ou de plusieurs jeux de données à partir desquels collecter les libellés d’utilisation des données. Pour ce faire, une requête POST est exécutée au point d’entrée `/constraints` pour une action marketing spécifique et une liste d’ID de jeu de données est fournie dans le corps de la requête.

**Format d’API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing en fonction de laquelle tester un ou plusieurs jeux de données. Vous pouvez récupérer une liste d’actions marketing disponibles en effectuant une [requête GET au point d’entrée des actions marketing](./marketing-actions.md#list). |

**Requête**

La requête suivante exécute l’action marketing `crossSiteTargeting` par rapport à un ensemble de trois jeux de données. Cela permet d’évaluer les violations de politique.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | Type d’entité dont l’ID est indiqué dans la propriété `entityId` voisine. Actuellement, la seule valeur acceptée est `dataSet`. |
| `entityId` | ID d’un jeu de données en fonction duquel tester l’action marketing. Une liste de jeux de données et de leurs ID correspondants peut être obtenue en effectuant une requête GET au point d’entrée `/dataSets` de l’API [!DNL Catalog Service]. Pour plus d’informations, consultez le guide sur la façon de [répertorier les objets du  [!DNL Catalog] ](../../catalog/api/list-objects.md). |

**Réponse**

Une réponse réussie comprend un tableau `violatedPolicies`, qui contient les détails des politiques enfreintes suite à l’exécution de l’action marketing par rapport aux jeux de données fournis. Si aucune politique n’est enfreinte, le tableau `violatedPolicies` apparaît vide.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## Évaluation des violations de politique à l’aide de champs de jeux de données spécifiques {#fields}

Vous pouvez évaluer les violations de politique en fonction d’un sous-ensemble de champs d’un ou de plusieurs jeux de données, de sorte que seuls les libellés d’utilisation des données appliqués à ces champs soient évalués.

Lors de l’évaluation des politiques à l’aide de champs de jeu de données, considérez les points suivants :

* **Les noms des champs sont sensibles à la casse** : lorsque vous spécifiez des champs, ils doivent être écrits exactement comme ils apparaissent dans le jeu de données (par exemple, `firstName` contre `firstname`).
* **Héritage des libellés des jeux de données** : les champs individuels d’un jeu de données héritent des libellés qui ont été appliqués au niveau du jeu de données. Si le retour de vos évaluations de politique ne s’effectue pas comme prévu, recherchez les libellés qui ont pu être hérités depuis le niveau des jeux de données vers les champs, en plus de ceux appliqués au niveau des champs.

**Format d’API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à tester par rapport à un sous-ensemble de champs de jeux de données. Vous pouvez récupérer une liste d’actions marketing disponibles en effectuant une [requête GET au point d’entrée des actions marketing](./marketing-actions.md#list). |

**Requête**

La requête suivante teste l’action marketing `crossSiteTargeting` sur un ensemble spécifique de champs appartenant à trois jeux de données. La payload est similaire à une [demande d’évaluation impliquant uniquement des jeux de données](#datasets), ajoutant des champs spécifiques pour chaque jeu de données où collecter les libellés.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | Type d’entité dont l’ID est indiqué dans la propriété `entityId` voisine. Actuellement, la seule valeur acceptée est `dataSet`. |
| `entityId` | ID d’un jeu de données dont les champs doivent être évalués par rapport à l’action marketing. Une liste de jeux de données et de leurs ID correspondants peut être obtenue en effectuant une requête GET au point d’entrée `/dataSets` de l’API [!DNL Catalog Service]. Pour plus d’informations, consultez le guide sur la façon de [répertorier les objets du  [!DNL Catalog] ](../../catalog/api/list-objects.md). |
| `entityMeta.fields` | Tableau de chemins d’accès à des champs spécifiques dans le schéma du jeu de données, fourni sous la forme de chaînes de pointeurs JSON. Consultez la section sur les [pointeurs JSON](../../landing/api-fundamentals.md#json-pointer) dans le guide des principes de base de l’API pour obtenir plus d’informations sur la syntaxe acceptée pour ces chaînes. |

**Réponse**

Une réponse réussie comprend un tableau `violatedPolicies`, qui contient les détails des politiques qui ont été enfreintes suite à l’exécution de l’action marketing par rapport aux champs du jeu de données fournis. Si aucune politique n’est enfreinte, le tableau `violatedPolicies` apparaît vide.

En comparant l’exemple de réponse ci-dessous à la [réponse impliquant uniquement des jeux de données](#datasets), notez que la liste des libellés collectés est plus courte. La valeur `discoveredLabels` pour chaque jeu de données a également été réduite, car elle inclut uniquement les champs spécifiés dans le corps de la requête. En outre, la politique `Targeting Ads or Content` précédemment enfreinte nécessite la présentation des deux libellés `C4 AND C6`. Elle n’est donc plus enfreinte, comme indiqué par le tableau `violatedPolicies` vide.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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

## Évaluation des politiques en bloc {#bulk}

Le point d’entrée `/bulk-eval` vous permet d’exécuter plusieurs traitements d’évaluation dans un seul appel API.

**Format d’API**

```http
POST /bulk-eval
```

**Requête**

La payload d’une demande d’évaluation en bloc doit être un tableau d’objets, où chacun représente un traitement d’évaluation à exécuter. Pour les traitements d’évaluation basés sur les jeux de données et les champs, un tableau `entityList` doit être fourni. Pour les traitements d’évaluation basés sur les libellés d’utilisation des données, un tableau `labels` doit être fourni.

>[!WARNING]
>
>Si un traitement d’évaluation répertorié contient à la fois un tableau `entityList` et un tableau `labels`, une erreur se produit. Si vous souhaitez évaluer la même action marketing en fonction des jeux de données et des libellés, vous devez inclure des traitements d’évaluation distincts pour cette action marketing.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `evalRef` | URI de l’action marketing à tester par rapport aux libellés ou aux jeux de données en cas de violations de politique. |
| `includeDraft` | Par défaut, seules les politiques activées participent à l’évaluation. Si la valeur `includeDraft` est définie sur `true`, les politiques dont l’état est défini sur `DRAFT` participent également. |
| `labels` | Tableau de libellés d’utilisation des données en fonction desquels tester l’action marketing.<br><br>**IMPORTANT** : lors de l’utilisation de cette propriété, une propriété `entityList` ne doit PAS être incluse dans le même objet. Pour évaluer la même action marketing à l’aide de jeux de données et/ou de champs, vous devez inclure un objet distinct dans la payload de requête qui contient un tableau `entityList`. |
| `entityList` | Tableau de jeux de données et de champs spécifiques (facultatifs) à ces jeux de données en fonction desquels tester l’action marketing.<br><br>**IMPORTANT** : lors de l’utilisation de cette propriété, une propriété `labels` ne doit PAS être incluse dans le même objet. Pour évaluer la même action marketing à l’aide de libellés d’utilisation de données spécifiques, vous devez inclure un objet distinct dans la payload de requête qui contient un tableau `labels`. |
| `entityType` | Type d’entité en fonction de laquelle tester l’action marketing. Actuellement, seul `dataSet` est pris en charge. |
| `entityId` | ID d’un jeu de données en fonction duquel tester l’action marketing. |
| `entityMeta.fields` | (Facultatif) Liste de champs spécifiques dans le jeu de données en fonction desquels tester l’action marketing. |

**Réponse**

Une réponse réussie renvoie un tableau reprenant les résultats de l’évaluation, où chaque résultat représente un traitement d’évaluation de politique envoyé dans la requête.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
          "imsOrg": "{ORG_ID}",
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

## Évaluation des politiques pour [!DNL Real-Time Customer Profile]

L’API [!DNL Policy Service] peut également servir à vérifier les violations de politique impliquant l’utilisation de segments de [!DNL Real-Time Customer Profile]. Pour plus d’informations, consultez le tutoriel sur l’[application de la conformité à l’utilisation des données pour les segments d’audience](../../segmentation/tutorials/governance.md).

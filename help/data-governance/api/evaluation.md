---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Stratégies
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 95%

---


# Évaluation des stratégies

Once marketing actions have been created and policies have been defined, you can use the [!DNL Policy Service] API to evaluate if any policies are violated by certain actions. Les contraintes renvoyées prennent la forme d’un ensemble de stratégies qui seraient enfreintes si l’action marketing était appliquée aux données spécifiées contenant les libellés d’utilisation des données.

Par défaut, **seules les stratégies dont l’état est défini sur « ENABLED » participent à l’évaluation**. Toutefois, vous pouvez utiliser le paramètre de requête `?includeDraft=true` pour inclure dans l’évaluation les stratégies dont l’état est défini sur « DRAFT ».

Les requêtes d’évaluation peuvent être effectuées de trois façons :

1. Compte tenu d’un ensemble de libellés d’utilisation des données et d’une action marketing, l’action enfreint-elle des stratégies ?
1. Compte tenu d’un ou plusieurs jeux de données et d’une action marketing, l’action enfreint-elle des stratégies ?
1. Compte tenu d’un ou plusieurs jeux de données et d’un sous-ensemble comprenant un ou plusieurs champs dans chaque jeu de données, l’action enfreint-elle des stratégies ?

## Évaluation des stratégies à l’aide de libellés d’utilisation des données et d’une action marketing

Pour évaluer les violations de stratégie en fonction de la présence de libellés d’utilisation des données, vous devez spécifier l’ensemble de libellés présents sur les données pendant la requête. Pour cela, vous devez utiliser des paramètres de requête où les libellés d’utilisation des données sont fournis sous la forme d’une liste de valeurs séparées par des virgules, comme illustré dans l’exemple suivant.

**Format d’API**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Requête**

L’exemple de requête ci-dessous évalue une action marketing en fonction des libellés C1 et C3. Lors de l’évaluation des stratégies à l’aide de libellés d’utilisation des données, considérez les points suivants :
* **Les libellés d’utilisation des données sont sensibles à la casse.** La requête illustrée ci-dessus renvoie une stratégie enfreinte, contrairement à une même requête utilisant des libellés en minuscules (par exemple, `"c1,c3"`, `"C1,c3"` ou `"c1,C3"`).
* **Tenez compte des opérateurs`AND`et`OR`dans l’expression des stratégies.** Dans cet exemple, si un des libellés (`C1` ou `C3`) était apparu seul dans la requête, l’action marketing n’aurait pas enfreint cette stratégie. Les deux libellés (`C1 AND C3`) sont nécessaires pour renvoyer la stratégie enfreinte. Assurez-vous d’évaluer soigneusement les stratégies et de bien définir l’expression des stratégies.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet de la réponse comprend un tableau `duleLabels` qui doit correspondre aux libellés envoyés dans la requête. Si l’exécution de l’action marketing spécifiée enfreint une stratégie à cause des libellés d’utilisation des données, le tableau `violatedPolicies` contient les détails des stratégies concernées. Si aucune stratégie n’est enfreinte, le tableau `violatedPolicies` apparaît vide (`[]`).

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

## Évaluation des stratégies à l’aide de jeux de données et d’une action marketing

Vous pouvez également évaluer les violations de stratégie en spécifiant l’identifiant d’un ou plusieurs jeux de données où collecter les libellés d’utilisation des données. Pour cela, vous devez effectuer une requête POST au point de terminaison `/constraints` principal ou personnalisé pour une action marketing, et spécifier les identifiants des jeux de données dans le corps de la requête, comme illustré ci-dessous.

**Format d’API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Requête**

Le corps de la requête contient un tableau avec un objet pour chaque identifiant de jeu de données. Puisque vous envoyez un corps de requête, l’en-tête de requête « Content-Type: application/json » est obligatoire, comme illustré dans l’exemple suivant.

```SHELL
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

**Réponse**

L’objet de la réponse comprend un tableau `duleLabels` qui contient une liste consolidée de tous les libellés trouvés dans les jeux de données spécifiés. Cette liste inclut des libellés de jeu de données et de champ pour tous les champs du jeu de données.

La réponse comprend également un tableau `discoveredLabels` contenant des objets pour chaque jeu de données, divisant les `datasetLabels` entre les libellés de jeu de données et les libellés de champ. Chaque libellé de champ indique le chemin d’accès au champ spécifique portant ce libellé.

Si l’action marketing spécifiée enfreint une stratégie impliquant les `duleLabels` des jeux de données, le tableau `violatedPolicies` contient les détails des stratégies concernées. Si aucune stratégie n’est enfreinte, le tableau `violatedPolicies` apparaît vide (`[]`).

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

## Évaluation des stratégies à l’aide de jeux de données, de champs et d’une action marketing

Outre l’utilisation d’un ou plusieurs identifiants de jeu de données, vous pouvez également spécifier un sous-ensemble de champs issus de chaque jeu de données en indiquant que seuls les libellés d’utilisation des données de ces champs doivent être évalués. Tout comme la requête POST impliquant uniquement les jeux de données, cette requête ajoute au corps de la requête des champs spécifiques pour chaque jeu de données.

Lors de l’évaluation des stratégies à l’aide de champs de jeu de données, considérez les points suivants :

* **Les noms de champ sont sensibles à la casse.** Lorsque vous spécifiez des champs, ils doivent être écrits exactement comme ils apparaissent dans le jeu de données (par exemple, `firstName` vs `firstname`).
* **Les libellés de jeu de données sont hérités.** Les libellés d’utilisation des données peuvent être appliqués à plusieurs niveaux et font l’objet d’un héritage descendant. Si vos évaluations de stratégie ne renvoient pas les résultats attendus, vérifiez les libellés des jeux de données hérités par les champs en plus de ceux appliqués au niveau des champs.

**Format d’API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Requête**

Le corps de la requête contient un tableau avec un objet pour chaque identifiant de jeu de données et le sous-ensemble de champs issu du jeu de données à utiliser pour l’évaluation. Puisque vous envoyez un corps de requête, l’en-tête de requête « Content-Type: application/json » est obligatoire, comme illustré dans l’exemple suivant.

```SHELL
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

**Réponse**

L’objet de la réponse comprend un tableau `duleLabels` qui contient la liste consolidée des libellés figurant dans les champs spécifiés. N’oubliez pas que cela inclut également les libellés des jeux de données, car ils sont hérités par les champs.

Si une stratégie est enfreinte par l’exécution de l’action marketing spécifiée sur les données des champs fournis, le tableau `violatedPolicies` contient les détails des stratégies concernées. Si aucune stratégie n’est enfreinte, le tableau `violatedPolicies` apparaît vide (`[]`).

Dans la réponse ci-dessous, vous pouvez constater que la liste de `duleLabels` est désormais plus courte, tout comme les `discoveredLabels` de chaque jeu de données, car ils ne comprennent que les champs spécifiés dans le corps de la requête. Vous remarquerez également que la stratégie précédemment enfreinte, « Targeting Ads or Content », exigeait les deux libellés `C4 AND C6`. Elle n’est donc plus enfreinte et le tableau `violatedPolicies` apparaît vide.

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

## Évaluation des politiques [!DNL Real-time Customer Profile]

The [!DNL Policy Service] API can also be used to check for policy violations involving the use of [!DNL Real-time Customer Profile] segments. Pour plus d’informations, consultez le tutoriel sur l’[application de la conformité à l’utilisation des données pour les segments d’audience](../../segmentation/tutorials/governance.md).
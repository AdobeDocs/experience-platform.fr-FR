---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Stratégies
topic: developer guide
translation-type: tm+mt
source-git-commit: 2997243622a7483ae23e21487128cea6badecb80
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 2%

---


# Évaluation des politiques

Une fois les actions marketing créées et les stratégies définies, vous pouvez utiliser l’API Service de stratégie pour déterminer si des stratégies sont violées par certaines actions. Les contraintes renvoyées prennent la forme d’un ensemble de stratégies qui seraient violées en tentant l’action marketing sur les données spécifiées contenant des étiquettes d’utilisation des données.

Par défaut, **seules les stratégies dont l’état est défini sur &quot;ACTIVÉ&quot; participent à l’évaluation**, mais vous pouvez utiliser le paramètre de requête `?includeDraft=true` pour inclure des stratégies &quot;BROUILLON&quot; dans l’évaluation.

Les demandes d&#39;évaluation peuvent être présentées de trois façons :

1. Compte tenu d’un ensemble d’étiquettes d’utilisation des données et d’une action marketing, l’action enfreint-elle des stratégies ?
1. Compte tenu d’un ou de plusieurs jeux de données et d’une action marketing, l’action enfreint-elle des stratégies ?
1. Compte tenu d’un ou de plusieurs jeux de données et d’un ou de plusieurs champs de chacun de ces jeux de données, l’action enfreint-elle des stratégies ?

## Evaluer les stratégies à l’aide de libellés d’utilisation des données et d’une action marketing

Pour évaluer les violations de stratégie en fonction de la présence d’étiquettes d’utilisation de données, vous devez spécifier l’ensemble d’étiquettes qui seront présentes sur les données pendant la demande. Pour ce faire, vous utilisez des paramètres de requête, où les étiquettes d’utilisation des données sont fournies sous la forme d’une liste de valeurs séparées par des virgules, comme indiqué dans l’exemple suivant.

**Format d’API**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Requête**

L’exemple de demande ci-dessous évalue une action marketing par rapport aux étiquettes C1 et C3. Lors de l’évaluation des stratégies à l’aide de libellés d’utilisation des données, gardez à l’esprit les points suivants :
* **Les libellés d’utilisation des données respectent la casse.** La requête illustrée ci-dessus renvoie une stratégie violée, alors qu&#39;elle utilise des libellés minuscules (ex. `"c1,c3"`, `"C1,c3"`, `"c1,C3"`) ne le fait pas.
* **Tenez compte des opérateurs`AND`et`OR`dans vos expressions de stratégie.** Dans cet exemple, si l’étiquette (`C1` ou `C3`) s’était présentée seule dans la demande, l’action marketing n’aurait pas enfreint cette stratégie. Il faut les deux étiquettes (`C1 AND C3`) pour renvoyer la stratégie violée. Assurez-vous que vous évaluez soigneusement les politiques et que vous définissez les expressions de politiques avec la même attention.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet response comprend un `duleLabels` tableau qui doit correspondre aux étiquettes envoyées dans la requête. Si l&#39;exécution de l&#39;action marketing spécifiée par rapport aux étiquettes d&#39;utilisation des données enfreint une stratégie, la `violatedPolicies` baie contiendra les détails de la (ou des stratégies) stratégie(s) concernée(s). Si aucune stratégie n&#39;est violée, le tableau `violatedPolicies` s&#39;affiche vide (`[]`).

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

## Evaluer les stratégies à l’aide de jeux de données et d’une action marketing

Vous pouvez également évaluer les violations de stratégie en spécifiant l’ID d’un ou de plusieurs jeux de données à partir desquels les étiquettes d’utilisation des données peuvent être collectées. Pour ce faire, vous devez exécuter une requête POST sur le point de terminaison principal ou personnalisé d’une action marketing et spécifier les ID des jeux de données dans le corps de la requête, comme illustré ci-dessous. `/constraints`

**Format d’API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Requête**

Le corps de la requête contient un tableau avec un objet pour chaque ID de jeu de données. Puisque vous envoyez un corps de requête, le message &quot;Content-Type: l’en-tête de requête application/json&quot; est obligatoire, comme illustré dans l’exemple suivant.

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

L&#39;objet response comprend un `duleLabels` tableau qui contient une liste consolidée de toutes les étiquettes trouvées dans les jeux de données spécifiés. Cette liste comprend des étiquettes au niveau des jeux de données et des champs sur tous les champs du jeu de données.

La réponse comprend également un `discoveredLabels` tableau contenant des objets pour chaque jeu de données, qui indique `datasetLabels` les étiquettes de niveau jeu de données et champ. Chaque étiquette de niveau champ affiche le chemin d’accès au champ spécifique avec cette étiquette.

Si l&#39;action marketing spécifiée enfreint une stratégie impliquant les `duleLabels` jeux de données, la `violatedPolicies` baie contient les détails de la (ou des stratégies) stratégie(s) concernée(s). Si aucune stratégie n&#39;est violée, le tableau `violatedPolicies` s&#39;affiche vide (`[]`).

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

## Evaluer des stratégies à l’aide de jeux de données, de champs et d’une action marketing

Outre la fourniture d’un ou de plusieurs ID de jeu de données, un sous-ensemble de champs de chaque jeu de données peut également être spécifié, ce qui indique que seuls les libellés d’utilisation des données de ces champs doivent être évalués. Comme pour la requête POST impliquant uniquement des jeux de données, cette requête ajoute des champs spécifiques pour chaque jeu de données au corps de la requête.

Lors de l’évaluation des stratégies à l’aide des champs de jeu de données, gardez à l’esprit les points suivants :

* **Les noms de champ respectent la casse.** Lorsque vous fournissez des champs, ils doivent être écrits exactement comme ils apparaissent dans le jeu de données (par exemple, `firstName` vs `firstname`).
* **Héritage de l’étiquette du jeu de données.** les étiquettes d’utilisation des données peuvent être appliquées à plusieurs niveaux et sont héritées vers le bas. Si vos évaluations de stratégie ne retournent pas la manière dont vous le pensiez, veillez à vérifier les étiquettes héritées des jeux de données dans les champs en plus de celles appliquées au niveau du champ.

**Format d’API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Requête**

Le corps de la requête contient un tableau avec un objet pour chaque ID de jeu de données et le sous-ensemble de champs dans ce jeu de données qui doit être utilisé pour l&#39;évaluation. Puisque vous envoyez un corps de requête, le message &quot;Content-Type: l’en-tête de requête application/json&quot; est obligatoire, comme illustré dans l’exemple suivant.

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

L’objet response comprend un `duleLabels` tableau qui contient la liste consolidée des libellés trouvés dans les champs spécifiés. N’oubliez pas que cela inclut également des étiquettes de jeux de données, car elles sont héritées jusqu’aux champs.

Si une stratégie est violée en exécutant l&#39;action marketing spécifiée sur les données des champs fournis, la `violatedPolicies` baie contient les détails de la (ou des stratégies) stratégie(s) concernée(s). Si aucune stratégie n&#39;est violée, le tableau `violatedPolicies` s&#39;affiche vide (`[]`).

Dans la réponse ci-dessous, vous pouvez voir que la liste de `duleLabels` données est désormais plus courte, tout comme celle `discoveredLabels` de chaque jeu de données, car elle inclut uniquement les champs spécifiés dans le corps de la requête. Vous remarquerez également que la stratégie précédemment violée, &quot;Ciblage des publicités ou du contenu&quot;, exigeait les deux `C4 AND C6` étiquettes. Elle n’est donc plus violée et la `violatedPolicies` baie apparaît vide.

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

## Évaluation des stratégies pour le Profil client en temps réel

L’API Service de stratégie peut également être utilisée pour vérifier les violations de stratégie impliquant l’utilisation de segments de Profil client en temps réel. Pour plus d’informations, consultez le tutoriel sur l’[application des stratégies d’utilisation des données pour les segments d’audience](../../segmentation/tutorials/governance.md).
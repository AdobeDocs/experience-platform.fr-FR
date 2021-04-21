---
keywords: Experience Platform ; accueil ; rubriques populaires ; Application des stratégies ; Application automatique ; Application basée sur les API ; gouvernance des données ; test
solution: Experience Platform
title: Appliquer les stratégies d’utilisation des données à l’aide de l’API Policy Service
topic-legacy: guide
type: Tutorial
description: Une fois que vous avez créé des libellés d’utilisation pour vos données et des stratégies d’utilisation pour les actions marketing en fonction de ces libellés, vous pouvez utiliser l’API Policy Service pour évaluer si une action marketing effectuée sur un jeu de données ou sur un groupe arbitraire de libellés constitue une violation de la stratégie. Vous pouvez ensuite configurer vos propres protocoles internes pour gérer les violations de stratégie en fonction de la réponse de l’API.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 58%

---

# Appliquer les stratégies d&#39;utilisation des données à l&#39;aide de l&#39;API [!DNL Policy Service]

Une fois que vous avez créé des étiquettes d&#39;utilisation des données pour vos données et créé des stratégies d&#39;utilisation pour les actions marketing à l&#39;égard de ces étiquettes, vous pouvez utiliser [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) pour évaluer si une action marketing effectuée sur un jeu de données ou un groupe arbitraire d&#39;étiquettes constitue une violation de stratégie. Vous pouvez ensuite configurer vos propres protocoles internes pour gérer les violations de stratégie en fonction de la réponse de l’API.

>[!NOTE]
>
>Par défaut, seules les stratégies dont l’état est défini sur `ENABLED` peuvent participer à l’évaluation. Pour autoriser les stratégies `DRAFT` à participer à l’évaluation, vous devez inclure le paramètre de requête `includeDraft=true` au chemin d’accès de la requête.

Ce document décrit la procédure à suivre pour utiliser l&#39;API [!DNL Policy Service] afin de rechercher les violations de stratégie dans différents scénarios.

## Prise en main

Ce didacticiel nécessite une bonne compréhension des concepts clés suivants liés à l’application des stratégies d’utilisation des données :

* [Gouvernance des données](../home.md)[!DNL Platform] : cadre selon lequel applique la conformité d’utilisation des données.
   * [Libellés d’utilisation des données](../labels/overview.md) : les libellés d’utilisation des données sont appliqués aux jeux de données (et/ou aux champs individuels de ces jeux de données), spécifiant les restrictions d’utilisation de ces données.
   * [Stratégies](../policies/overview.md) d’utilisation des données : Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing qui sont autorisées ou restreintes pour certains jeux d’étiquettes d’utilisation des données.
* [Sandbox](../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Avant de commencer ce tutoriel, consultez le [guide de développement](../api/getting-started.md) pour obtenir les informations importantes à connaître afin d’effectuer avec succès des appels vers l’API , y compris les en-têtes requis et la méthode de lecture d’exemples d’appels API.[!DNL Policy Service]

## Évaluation à l’aide de libellés et d’une action marketing

Vous pouvez évaluer une stratégie en testant une action marketing par rapport à un ensemble d’étiquettes d’utilisation de données qui seraient éventuellement présentes dans un jeu de données. Pour cela, vous devez utiliser des paramètres de requête `duleLabels` où les libellés sont fournis sous la forme d’une liste de valeurs séparées par des virgules, comme indiqué dans l’exemple ci-dessous.

**Format d’API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing associée à la stratégie d’utilisation des données que vous évaluez. |
| `{LABEL_1}` | Libellé d’utilisation des données permettant de tester l’action marketing. Au moins un libellé doit être fourni. Lorsque vous fournissez plusieurs libellés, ceux-ci doivent être séparés par des virgules. |

**Requête**

La requête suivante teste l’action marketing `exportToThirdParty` par rapport aux libellés `C1` et `C3`. Puisque la stratégie d’utilisation des données que vous avez créée précédemment dans ce tutoriel définit le libellé `C1` comme l’une des conditions `deny` de sa stratégie, l’action marketing doit signaler une violation de la stratégie.

>[!NOTE]
>
>Les libellés d’utilisation des données sont sensibles à la casse. Les violations de stratégie ne surviennent qu’en cas de correspondance exacte avec les libellés définis dans leurs expressions de stratégie. Dans cet exemple, un libellé `C1` déclenche une violation, mais pas un libellé `c1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie l’URL de l’action marketing, les étiquettes d’utilisation sur lesquelles elle a été testée et une liste de toute stratégie violée suite au test de l’action par rapport à ces étiquettes. Dans cet exemple, la stratégie « Export Data to Third Party » s’affiche dans le tableau `violatedPolicies`, indiquant que l’action marketing a déclenché la violation de stratégie attendue.

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
| `violatedPolicies` | Un tableau répertoriant toutes les stratégies violées lors du test de l’action marketing (spécifiée dans `marketingActionRef`) en fonction des `duleLabels` fournies. |

## Évaluation à l’aide de jeux de données

Vous pouvez évaluer une stratégie d’utilisation des données en testant une action marketing par rapport à un ou plusieurs jeux de données à partir desquels des étiquettes peuvent être collectées. Pour ce faire, vous devez envoyer une requête POST à `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` et fournir des identifiants de jeux de données dans le corps de la requête, comme indiqué dans l’exemple ci-dessous.

**Format d’API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing associée à la stratégie que vous évaluez. |

**Requête**

La requête suivante teste l’action marketing `exportToThirdParty` en fonction de trois jeux de données différents. Les jeux de données sont référencés par type et par identifiant dans un tableau fourni dans le payload.

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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| Propriété | Description |
| --- | --- |
| `entityType` | Chaque élément du tableau de payload doit indiquer le type d’entité en cours de définition. Dans ce cas d’utilisation, la valeur sera toujours « dataSet ». |
| `entityId` | Chaque élément du tableau de payload doit fournir l’ID unique d’un jeu de données. |
| `entityMeta.fields` | (Facultatif) Tableau de chaînes [JSON Pointer](../../landing/api-fundamentals.md#json-pointer), référençant des champs spécifiques dans le schéma du jeu de données. Si ce tableau est inclus, seuls les champs contenus dans le tableau participent à l&#39;évaluation. Les champs de schéma qui ne sont pas inclus dans la baie ne participent pas à l&#39;évaluation.<br><br>Si ce champ n&#39;est pas inclus, tous les champs du schéma de jeux de données seront inclus dans l&#39;évaluation. |

**Réponse**

Une réponse positive renvoie l’URL de l’action marketing, les étiquettes d’utilisation collectées à partir des jeux de données fournis et une liste de toute stratégie violée suite au test de l’action par rapport à ces étiquettes. Dans cet exemple, la stratégie « Export Data to Third Party » s’affiche dans le tableau `violatedPolicies`, indiquant que l’action marketing a déclenché la violation de stratégie attendue.

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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
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
| `duleLabels` | Liste d’étiquettes d’utilisation des données extraites des jeux de données fournis dans la charge utile de la demande. |
| `discoveredLabels` | Liste des jeux de données fournis dans le payload de la requête affichant les libellés au niveau du jeu de données et au niveau du champ trouvées dans chaque jeu. |
| `violatedPolicies` | Un tableau répertoriant toutes les stratégies violées lors du test de l’action marketing (spécifiée dans `marketingActionRef`) en fonction des `duleLabels` fournies. |

## Étapes suivantes

En lisant ce document, vous avez réussi à rechercher des violations de stratégie lors de l’exécution d’une action marketing sur un jeu de données ou un ensemble d’étiquettes d’utilisation des données. En utilisant les données renvoyées dans les réponses de l’API, vous pouvez configurer des protocoles dans votre application d’expérience de façon à appliquer les violations de stratégie lorsque celles-ci se produisent.

Pour plus d&#39;informations sur la façon dont Platform fournit automatiquement l&#39;application de stratégies pour les segments activés, consultez le guide sur [l&#39;application automatique](./auto-enforcement.md).

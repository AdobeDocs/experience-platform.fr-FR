---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Stratégies
topic: developer guide
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 92%

---


# Stratégies

Data usage policies are rules your organization adopts that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform].

Le point de terminaison `/policies` est utilisé pour tous les appels API liés à l’affichage, la création, la mise à jour ou la suppression des stratégies d’utilisation des données.

## Liste de toutes les stratégies

Pour afficher une liste des stratégies, vous pouvez envoyer une requête GET à `/policies/core` ou `/policies/custom`, qui renvoie toutes les stratégies pour le conteneur spécifié.

**Format d’API**

```http
GET /policies/core
GET /policies/custom
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse comprend un « count » indiquant le nombre total de stratégies au sein du conteneur spécifié, ainsi que les détails de chaque stratégie, y compris son `id`. Le champ `id` permet d’effectuer des requêtes de recherche afin de consulter des stratégies spécifiques, mais aussi d’effectuer des opérations de mise à jour et de suppression.

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
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
            "created": 1550691551888,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
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

## Rechercher une stratégie

Chaque stratégie contient un champ `id` qui peut être utilisé pour demander les détails d’une stratégie spécifique. Si vous ne connaissez pas l’`id` d’une stratégie, vous pouvez le trouver à l’aide de la requête de liste GET, qui permet de répertorier toutes les stratégies d’un conteneur spécifique (`core` ou `custom`), comme indiqué à l’étape précédente.

**Format d’API**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse contient les détails de la stratégie, y compris des champs clés comme `id` (ce champ doit correspondre au champ `id` envoyé dans la requête), `name`, `status` et `description`, ainsi qu’un lien de référence vers l’action marketing sur laquelle la stratégie est basée (`marketingActionRefs`).

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Création d’une stratégie {#create-policy}

La création d’une stratégie nécessite l’inclusion d’une action marketing avec l’expression des étiquettes DULE qui interdisent cette action marketing. Les définitions de stratégie doivent inclure une propriété `deny`, à savoir une expression booléenne concernant la présence d’étiquettes DULE.

Appelée `PolicyExpression`, cette expression est un objet contenant _soit_ une étiquette, _soit_ un opérateur et des opérandes, mais pas les deux. De même, chaque opérande forme également un objet `PolicyExpression`. Par exemple, une stratégie relative à l’exportation de données vers un tiers peut être interdite en présence d’étiquettes `C1 OR (C3 AND C7)`. Cette expression serait spécifiée comme suit :

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

**Format d’API**

```http
POST /policies/custom
```

**Requête**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Réponse**

Si la création est réussie, vous recevez un état HTTP 201 (Created) et le corps de la réponse contient les détails de la nouvelle stratégie, y compris son `id`. Cette valeur est en lecture seule et s’affiche automatiquement lors de la création de la stratégie.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Mise à jour d’une stratégie

Vous devrez peut-être mettre à jour une stratégie d’utilisation des données après sa création. Pour ce faire, vous devez envoyer une requête PUT à l’`id` de la stratégie avec un payload incluant la forme mise à jour de la stratégie dans son intégralité. En d’autres termes, la requête PUT procède essentiellement à une _réécriture_ de la stratégie. Par conséquent, le corps doit inclure toutes les informations requises, comme indiqué dans l’exemple ci-dessous.

**Format d’API**

```http
PUT /policies/custom/{id}
```

**Requête**

Dans cet exemple, les conditions d’exportation des données vers un tiers ont été modifiées. Vous devez définir la stratégie créée de sorte qu’elle rejette cette action marketing en présence d’étiquettes de données `C1 AND (C3 OR C7)`. Utilisez l’appel suivant pour mettre à jour la stratégie existante.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Réponse**

Une requête de mise à jour réussie renvoie un état HTTP 200 (OK) et le corps de la réponse affiche la stratégie mise à jour. L’`id` doit correspondre à l’`id` envoyé dans la requête.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Mise à jour d’une partie d’une stratégie

Vous pouvez mettre à jour une partie spécifique d’une stratégie à l’aide d’une requête PATCH. Contrairement aux requêtes PUT qui _réécrivent_ la stratégie, les requêtes PATCH ne mettent à jour que le chemin spécifié dans le corps de la requête. Cela s’avère particulièrement utile lorsque vous souhaitez activer ou désactiver une stratégie, car il vous suffit d’envoyer le chemin spécifique à mettre à jour (`/status`) et sa valeur (`ENABLE` ou `DISABLE`).

The [!DNL Policy Service] API currently supports &quot;add&quot;, &quot;replace&quot;, and &quot;remove&quot; PATCH operations, and allows you to combine several updates together into a single call by adding each as an object within the array, as shown in the following examples.

**Format d’API**

```http
PATCH /policies/custom/{id}
```

**Requête**

Dans cet exemple, nous utilisons l’opération « replace » pour modifier l’état de la stratégie « DRAFT » en « ENABLED » et pour mettre à jour le champ de description. Nous aurions également pu mettre à jour le champ de description à l’aide de l’opération « delete » pour supprimer la description de la stratégie, puis à l’aide de l’opération « add » pour en ajouter une, comme dans l’exemple qui suit :

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

Lorsque vous envoyez plusieurs opérations PATCH dans une seule requête, n’oubliez pas qu’elles sont traitées dans l’ordre dans lequel elles apparaissent dans le tableau. Veillez donc à envoyer les requêtes dans l’ordre approprié, le cas échéant.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**Réponse**

Une requête de mise à jour réussie renvoie un état HTTP 200 (OK) et le corps de la réponse affiche la stratégie mise à jour (« status » est désormais « ENABLED » et « description » a été modifié). L’`id` de la stratégie doit correspondre à l’`id` envoyé dans la requête.


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Suppression d’une stratégie

Si vous devez supprimer une stratégie que vous avez créée, vous pouvez envoyer une requête DELETE à l’`id` de la stratégie à supprimer. Il est recommandé d’effectuer d’abord une requête de recherche GET afin d’afficher la stratégie et de confirmer qu’il s’agit bien de la stratégie à supprimer. **Les stratégies supprimées ne peuvent pas être récupérées.**

**Format d’API**

```http
DELETE /policies/custom/{id}
```

**Requête**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Si la stratégie a bien été supprimée, le corps de la réponse sera vide avec un état HTTP 200 (OK).

Vous pouvez confirmer la suppression de la stratégie en la recherchant à l’aide de GET. Vous devriez recevoir un état HTTP 404 (Not Found), ainsi qu’un message d’erreur indiquant que la stratégie est introuvable, puisqu’elle a été supprimée.

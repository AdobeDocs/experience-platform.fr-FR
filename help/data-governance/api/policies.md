---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Stratégies
topic: developer guide
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---


# Stratégies

Data usage policies are rules your organization adopts that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform].

Le `/policies` point de terminaison est utilisé pour tous les appels d’API liés à l’affichage, la création, la mise à jour ou la suppression des stratégies d’utilisation des données.

## Liste de toutes les stratégies

Pour vue d’une liste de stratégies, une requête GET peut être envoyée à `/policies/core` ou `/policies/custom` qui renvoie toutes les stratégies pour le conteneur spécifié.

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

La réponse comprend un &quot;décompte&quot; indiquant le nombre total de stratégies dans le conteneur spécifié, ainsi que les détails de chaque stratégie, y compris sa `id`valeur. Ce `id` champ est utilisé pour exécuter des requêtes de recherche sur des stratégies spécifiques à la vue, ainsi que pour effectuer des opérations de mise à jour et de suppression.

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

Chaque stratégie contient un `id` champ qui peut être utilisé pour demander les détails d’une stratégie spécifique. Si l’ `id` une stratégie est inconnue, elle peut être trouvée à l’aide de la demande d’énumération (GET) pour liste toutes les stratégies dans un conteneur spécifique (`core` ou `custom`), comme indiqué à l’étape précédente.

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

La réponse contient les détails de la stratégie, y compris les champs clés tels que `id` (ce champ doit correspondre à celui `id` envoyé dans la demande), `name`, `status`et `description`, ainsi qu’un lien de référence vers l’action marketing sur laquelle la stratégie est basée (`marketingActionRefs`).

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

La création d’une stratégie nécessite l’inclusion d’une action marketing avec une expression des étiquettes DULE qui interdisent cette action marketing. Les définitions de stratégie doivent inclure une `deny` propriété, qui est une expression booléenne concernant la présence d&#39;étiquettes DULE.

Cette expression est appelée un `PolicyExpression` et est un objet contenant _soit_ une étiquette __ soit un opérateur et des opérandes, mais pas les deux. Chaque opérande est à son tour un `PolicyExpression` objet. Par exemple, une politique relative à l’exportation de données vers un tiers peut être interdite si `C1 OR (C3 AND C7)` des étiquettes sont présentes. Cette expression serait spécifiée comme suit :

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

Si la création est réussie, vous recevrez un état HTTP 201 (créé) et le corps de la réponse contiendra les détails de la nouvelle stratégie, y compris son `id`état. Cette valeur est en lecture seule et est affectée automatiquement lors de la création de la stratégie.

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

## Mettre à jour une stratégie

Vous devrez peut-être mettre à jour une stratégie d&#39;utilisation des données après sa création. Pour ce faire, une requête PUT est envoyée à la stratégie `id` avec une charge utile qui inclut la forme mise à jour de la stratégie, dans son intégralité. En d&#39;autres termes, la demande de PUT consiste essentiellement à _réécrire_ la stratégie, de sorte que l&#39;organisme doit inclure toutes les informations requises, comme indiqué dans l&#39;exemple ci-dessous.

**Format d’API**

```http
PUT /policies/custom/{id}
```

**Requête**

Dans cet exemple, les conditions d’exportation des données vers un tiers ont changé. Désormais, vous avez besoin de la stratégie que vous avez créée pour refuser cette action marketing si `C1 AND (C3 OR C7)` des étiquettes de données sont présentes. Utilisez l’appel suivant pour mettre à jour la stratégie existante.

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

Une demande de mise à jour réussie renvoie un état HTTP 200 (OK) et le corps de la réponse affiche la stratégie mise à jour. Le `id` doit correspondre à celui `id` envoyé dans la demande.

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

Une partie spécifique d’une stratégie peut être mise à jour à l’aide d’une demande PATCH. Contrairement aux requêtes PUT qui _réécrivent_ la stratégie, les requêtes PATCH ne mettent à jour que le chemin spécifié dans le corps de la requête. Cela s’avère particulièrement utile lorsque vous souhaitez activer ou désactiver une stratégie, car vous devez uniquement envoyer le chemin d’accès spécifique que vous souhaitez mettre à jour (`/status`) et sa valeur (`ENABLE` ou `DISABLE`).

L&#39; [!DNL Policy Service] API prend actuellement en charge les opérations &quot;add&quot;, &quot;replace&quot; et &quot;remove&quot; PATCH et vous permet de combiner plusieurs mises à jour en un seul appel en les ajoutant comme un objet dans la baie, comme le montrent les exemples suivants.

**Format d’API**

```http
PATCH /policies/custom/{id}
```

**Requête**

Dans cet exemple, nous utilisons l’opération &quot;remplacer&quot; pour changer l’état de la stratégie de &quot;BROUILLON&quot; en &quot;ACTIVÉ&quot; et pour mettre à jour le champ de description avec une nouvelle description. Nous aurions également pu mettre à jour le champ de description en utilisant l’opération &quot;supprimer&quot; pour supprimer la description de la stratégie, puis en utilisant l’opération &quot;ajouter&quot; pour ajouter une nouvelle fois, comme par exemple :

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

Lors de l&#39;envoi de plusieurs opérations PATCH dans une seule requête, n&#39;oubliez pas qu&#39;elles seront traitées dans l&#39;ordre dans lequel elles apparaissent dans la baie. Assurez-vous donc que vous envoyez les requêtes dans l&#39;ordre approprié si nécessaire.

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

Une demande de mise à jour réussie renverra un état HTTP 200 (OK) et le corps de la réponse affichera la stratégie mise à jour (&quot;status&quot; est maintenant &quot;ENABLED&quot; et &quot;description&quot; a été modifié). La stratégie `id` doit correspondre à celle `id` envoyée dans la demande.


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

Si vous devez supprimer une stratégie que vous avez créée, vous pouvez le faire en envoyant une demande de DELETE à la stratégie que vous souhaitez supprimer. `id` Il est recommandé d’effectuer d’abord une demande de recherche (GET) pour vue à la stratégie et vérifier que celle-ci est la bonne stratégie que vous souhaitez supprimer. **Une fois supprimées, les stratégies ne peuvent plus être récupérées.**

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

Si la stratégie a été correctement supprimée, le corps de la réponse sera vide avec un état HTTP 200 (OK).

Vous pouvez confirmer la suppression en tentant de rechercher à nouveau (GET) la stratégie. Vous devez recevoir un état HTTP 404 (introuvable) accompagné d’un message d’erreur &quot;Non trouvé&quot; car la stratégie a été supprimée.

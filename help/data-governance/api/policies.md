---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Stratégies
topic: developer guide
translation-type: tm+mt
source-git-commit: 08d02e7323f75c450e7a250835f26a569685cdd1

---


# Stratégies

Les stratégies d’utilisation des données sont des règles adoptées par votre entreprise qui décrivent les types d’actions marketing que vous êtes autorisé à exécuter ou dont vous êtes limité à l’exécution sur les données dans la plateforme d’expérience.

Le `/policies` point de fin est utilisé pour tous les appels d’API liés à l’affichage, la création, la mise à jour ou la suppression de stratégies d’utilisation des données.

##  toutes les stratégies

Pour  un de stratégies, une requête GET peut être envoyée à `/policies/core` ou `/policies/custom` qui renvoie toutes les stratégies pour le  spécifié.

**Format API**

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

La réponse comprend un &quot;nombre&quot; indiquant le nombre total de stratégies au sein du spécifié, ainsi que les détails de chaque stratégie, y compris sa `id`valeur. Le `id` champ permet d’effectuer des requêtes de recherche pour de stratégies spécifiques, ainsi que d’effectuer des opérations de mise à jour et de suppression.

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

## Rechercher une stratégie spécifique

Chaque stratégie contient un `id` champ qui peut être utilisé pour demander les détails d’une stratégie spécifique. Si l’ `id` une stratégie est inconnue, vous pouvez la trouver à l’aide de la demande d’énumération (GET) pour toutes les stratégies dans un spécifique (`core` ou `custom`), comme indiqué à l’étape précédente.

**Format API**

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

La réponse contient les détails de la stratégie, y compris des champs clés tels que `id` (ce champ doit correspondre au `id` champ envoyé dans la requête), `name`, `status`et `description`, ainsi qu’un lien de référence vers l’action marketing sur laquelle la stratégie est basée (`marketingActionRefs`).

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

La création d’une stratégie nécessite l’inclusion d’une action marketing avec un   des étiquettes DULE qui interdit cette action marketing. Les définitions de stratégie doivent inclure une `deny` propriété, qui est un booléen   concernant la présence d’étiquettes DULE.

Ce   est appelé un `PolicyExpression` et est un objet contenant _soit_ une étiquette _soit_ un opérateur et des opérandes, mais pas les deux. En retour, chaque opérande est aussi un `PolicyExpression` objet. Par exemple, une stratégie relative à l’exportation de données vers un tiers peut être interdite si `C1 OR (C3 AND C7)` des étiquettes sont présentes. Ce   de serait spécifié comme suit :

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

**Format API**

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

Si la création est réussie, vous recevrez un état HTTP 201 (créé) et le corps de la réponse contiendra les détails de la nouvelle stratégie, y compris sa `id`version. Cette valeur est en lecture seule et est affectée automatiquement lors de la création de la stratégie.

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

Vous devrez peut-être mettre à jour une stratégie d’utilisation des données après sa création. Pour ce faire, une requête PUT est envoyée à la stratégie `id` avec une charge utile qui inclut la forme mise à jour de la stratégie, dans son intégralité. En d’autres termes, la requête PUT est essentiellement en train de _réécrire_ la stratégie. Par conséquent, l’organisme doit inclure toutes les informations requises, comme indiqué dans l’exemple ci-dessous.

**Format API**

```http
PUT /policies/custom/{id}
```

**Requête**

Dans cet exemple, les conditions d’exportation des données vers un tiers ont changé. Vous devez désormais définir la stratégie que vous avez créée pour refuser cette action marketing si `C1 AND (C3 OR C7)` des étiquettes de données sont présentes. Utilisez l’appel suivant pour mettre à jour la stratégie existante.

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

Une requête de mise à jour réussie renvoie un état HTTP 200 (OK) et le corps de la réponse affiche la stratégie mise à jour. La `id` valeur doit correspondre à la valeur `id` envoyée dans la requête.

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

Une partie spécifique d’une stratégie peut être mise à jour à l’aide d’une requête PATCH. Contrairement aux requêtes PUT qui _réécrivent_ la stratégie, les requêtes PATCH ne mettent à jour que le chemin spécifié dans le corps de la requête. Cela s’avère particulièrement utile lorsque vous souhaitez activer ou désactiver une stratégie, car vous devez uniquement envoyer le chemin spécifique que vous souhaitez mettre à jour (`/status`) et sa valeur (`ENABLE` ou `DISABLE`).

L’API Policy Service prend actuellement en charge les opérations &quot;add&quot;, &quot;replace&quot; et &quot;remove&quot; PATCH et vous permet de combiner plusieurs mises à jour en un seul appel en les ajoutant comme un objet dans le tableau, comme illustré dans les exemples suivants.

**Format API**

```http
PATCH /policies/custom/{id}
```

**Requête**

Dans cet exemple, nous utilisons l’opération &quot;Remplacer&quot; pour changer l’état de la stratégie de &quot;BROUILLON&quot; en &quot;ACTIVÉ&quot; et pour mettre à jour le champ de description avec une nouvelle description. Nous aurions également pu mettre à jour le champ de description en utilisant l’opération &quot;supprimer&quot; pour supprimer la description de la stratégie, puis en utilisant l’opération &quot;ajouter&quot; pour ajouter une nouvelle fois, comme suit :

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

Lors de l’envoi de plusieurs opérations PATCH dans une seule requête, n’oubliez pas qu’elles seront traitées dans l’ordre dans lequel elles apparaissent dans le tableau. Veillez donc à envoyer les requêtes dans l’ordre approprié, le cas échéant.

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

Une demande de mise à jour réussie renvoie un état HTTP 200 (OK) et le corps de la réponse affiche la stratégie mise à jour (&quot;status&quot; est désormais &quot;ENABLED&quot; et &quot;description&quot; a été modifié). La stratégie `id` doit correspondre à celle `id` envoyée dans la requête.


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

Si vous devez supprimer une stratégie que vous avez créée, vous pouvez le faire en envoyant une requête DELETE à la stratégie `id` que vous souhaitez supprimer. Il est recommandé d’effectuer d’abord une requête GET (recherche) afin de de la stratégie et de confirmer qu’il s’agit de la stratégie appropriée que vous souhaitez supprimer. **Une fois supprimées, les stratégies ne peuvent plus être récupérées.**

**Format API**

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

Si la stratégie a bien été supprimée, le corps de la réponse sera vide avec un état HTTP 200 (OK).

Vous pouvez confirmer la suppression en tentant de rechercher (GET) à nouveau la stratégie. Vous devez recevoir un message d’erreur HTTP Status 404 (Introuvable) ainsi qu’un message d’erreur &quot;Not Found&quot; (Non trouvé), car la stratégie a été supprimée.

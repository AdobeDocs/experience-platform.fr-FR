---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Stratégies
topic: developer guide
translation-type: tm+mt
source-git-commit: 7bc7050d64727f09d3a13d803d532a9a3ba5d1a7
workflow-type: tm+mt
source-wordcount: '1756'
ht-degree: 8%

---


# Stratégies point de terminaison

Data usage policies are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform]. Le `/policies` point de terminaison de la [!DNL Policy Service API] permet de gérer par programmation les stratégies d’utilisation des données pour votre entreprise.

## Prise en main

The API endpoint used in this guide is part of the [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Avant de continuer, consultez le guide [de](getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute [!DNL Experience Platform] API.

## Retrieve a list of policies {#list}

Vous pouvez liste toutes les `core` stratégies ou `custom` les stratégies en adressant une demande de GET `/policies/core` ou `/policies/custom`, respectivement.

**Format d’API**

```http
GET /policies/core
GET /policies/custom
```

**Requête**

La requête suivante récupère une liste de stratégies personnalisées définies par votre organisation.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie comprend un `children` tableau qui liste les détails de chaque stratégie récupérée, y compris leurs `id` valeurs. Vous pouvez utiliser le `id` champ d’une stratégie spécifique pour effectuer une [recherche](#lookup), [mettre à jour](#update)et [supprimer](#delete) des requêtes pour cette stratégie.

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
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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

| Propriété | Description |
| --- | --- |
| `_page.count` | Nombre total de stratégies récupérées. |
| `name` | Nom d’affichage d’une stratégie. |
| `status` | Statut actuel d’une stratégie. Il existe trois états possibles : `DRAFT`, `ENABLED`ou `DISABLED`. By default, only `ENABLED` policies participate in evaluation. Pour plus d’informations, consultez l’aperçu de l’évaluation [des](../enforcement/overview.md) politiques. |
| `marketingActionRefs` | Tableau qui liste les URI de toutes les actions marketing applicables pour une stratégie. |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas d’utilisation de la stratégie. |
| `deny` | Objet qui décrit les étiquettes d’utilisation de données spécifiques sur lesquelles l’action marketing associée à une stratégie ne peut pas être exécutée. Voir la section sur la [création d’une stratégie](#create-policy) pour plus d’informations sur cette propriété. |

## Rechercher une stratégie {#look-up}

Vous pouvez rechercher une stratégie spécifique en incluant la `id` propriété de cette stratégie dans le chemin d’une demande de GET.

**Format d’API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | The `id` of the policy you want to look up. |

**Requête**

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la stratégie.

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
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| Propriété | Description |
| --- | --- |
| `name` | Nom d’affichage de la stratégie. |
| `status` | Statut actuel de la stratégie. Il existe trois états possibles : `DRAFT`, `ENABLED`ou `DISABLED`. By default, only `ENABLED` policies participate in evaluation. Pour plus d’informations, consultez l’aperçu de l’évaluation [des](../enforcement/overview.md) politiques. |
| `marketingActionRefs` | Tableau qui liste les URI de toutes les actions marketing applicables pour la stratégie. |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas d’utilisation de la stratégie. |
| `deny` | Objet qui décrit les étiquettes d’utilisation de données spécifiques sur lesquelles l’action marketing associée à la stratégie ne peut pas être exécutée. Voir la section sur la [création d’une stratégie](#create-policy) pour plus d’informations sur cette propriété. |

## Create a custom policy {#create-policy}

Dans l’ [!DNL Policy Service] API, une stratégie est définie par les éléments suivants :

* Référence à une action marketing spécifique
* Expression décrivant les étiquettes d’utilisation des données pour lesquelles l’action marketing ne peut pas être exécutée par rapport à

Pour satisfaire à cette dernière exigence, les définitions de stratégie doivent inclure une expression booléenne concernant la présence d’étiquettes d’utilisation des données. Cette expression s&#39;appelle une expression **de** politique.

Les expressions de stratégie sont fournies sous la forme d’une `deny` propriété au sein de chaque définition de stratégie. Voici un exemple d’objet simple `deny` qui ne vérifie la présence que d’une seule étiquette :

```json
"deny": {
    "label": "C1"
}
```

Cependant, de nombreuses stratégies spécifient des conditions plus complexes concernant la présence d’étiquettes d’utilisation des données. Pour prendre en charge ces cas d’utilisation, vous pouvez également inclure des opérations booléennes pour décrire vos expressions de stratégie. L&#39;objet d&#39;expression de stratégie doit contenir _soit_ une étiquette _soit_ un opérateur et des opérandes, mais pas les deux. De même, chaque opérande est également un objet d’expression de stratégie.

Par exemple, afin de définir une stratégie qui interdit l’exécution d’une action marketing sur des données où `C1 OR (C3 AND C7)` `deny` des étiquettes sont présentes, la propriété de la stratégie est spécifiée comme suit :

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

| Propriété | Description |
| --- | --- |
| `operator` | Indique la relation conditionnelle entre les étiquettes fournies dans le tableau `operands` frère. Les valeurs acceptées sont les suivantes : <ul><li>`OR`: L&#39;expression est résolue sur true si l&#39;un des libellés du `operands` tableau est présent.</li><li>`AND`: L&#39;expression ne se résout à true que si tous les libellés du `operands` tableau sont présents.</li></ul> |
| `operands` | Tableau d’objets, chaque objet représentant soit une seule étiquette, soit une paire supplémentaire de `operator` propriétés et de propriétés `operands` . La présence des libellés et/ou des opérations dans un `operands` tableau est résolue sur true ou false en fonction de la valeur de sa `operator` propriété frère. |
| `label` | Nom d’une étiquette d’utilisation de données unique qui s’applique à la stratégie. |

You can create a new custom policy by making a POST request to the `/policies/custom` endpoint.

**Format d’API**

```http
POST /policies/custom
```

**Requête**

La requête suivante crée une nouvelle stratégie qui limite l’exécution de l’action marketing `exportToThirdParty` aux données contenant des étiquettes `C1 OR (C3 AND C7)`.

```sh
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
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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

| Propriété | Description |
| --- | --- |
| `name` | Nom d’affichage de la stratégie. |
| `status` | Statut actuel de la stratégie. Il existe trois états possibles : `DRAFT`, `ENABLED`ou `DISABLED`. By default, only `ENABLED` policies participate in evaluation. Pour plus d’informations, consultez l’aperçu de l’évaluation [des](../enforcement/overview.md) politiques. |
| `marketingActionRefs` | Tableau qui liste les URI de toutes les actions marketing applicables pour la stratégie. L’URI d’une action marketing est fourni sous `_links.self.href` la réponse pour la [recherche d’une action](./marketing-actions.md#look-up)marketing. |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas d’utilisation de la stratégie. |
| `deny` | L’expression de stratégie qui décrit l’utilisation spécifique des données ne peut pas être exécutée sur laquelle l’action marketing associée à la stratégie est limitée. |

**Réponse**

A successful response returns the details of the newly created policy, including its `id`. Cette valeur est en lecture seule et s’affiche automatiquement lors de la création de la stratégie.

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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Mettre à jour une stratégie personnalisée {#update}

>[!IMPORTANT]
>
>Vous pouvez uniquement mettre à jour des stratégies personnalisées. Si vous souhaitez activer ou désactiver les stratégies de base, reportez-vous à la section relative à la [mise à jour de la liste des stratégies](#update-enabled-core)de base activées.

Vous pouvez mettre à jour une stratégie personnalisée existante en fournissant son identifiant dans le chemin d’une demande de PUT avec une charge utile qui inclut la forme mise à jour de la stratégie dans son intégralité. En d&#39;autres termes, la demande du PUT _réécrit_ essentiellement la politique.

>[!NOTE]
>
>Reportez-vous à la section relative à la [mise à jour d’une partie d’une stratégie](#patch) personnalisée si vous souhaitez uniquement mettre à jour un ou plusieurs champs d’une stratégie plutôt que de la remplacer.

**Format d’API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | The `id` of the policy you want to update. |

**Requête**

Dans cet exemple, les conditions d’exportation des données vers un tiers ont été modifiées. Vous devez définir la stratégie créée de sorte qu’elle rejette cette action marketing en présence d’étiquettes de données `C1 AND C5`. 

La requête suivante met à jour la stratégie existante pour inclure la nouvelle expression de stratégie. Notez que puisque cette requête réécrit essentiellement la stratégie, tous les champs doivent être inclus dans la charge utile, même si certaines de leurs valeurs ne sont pas mises à jour.

```sh
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
            {"label": "C5"}
          ]
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom d’affichage de la stratégie. |
| `status` | Statut actuel de la stratégie. Il existe trois états possibles : `DRAFT`, `ENABLED`ou `DISABLED`. By default, only `ENABLED` policies participate in evaluation. Pour plus d’informations, consultez l’aperçu de l’évaluation [des](../enforcement/overview.md) politiques. |
| `marketingActionRefs` | Tableau qui liste les URI de toutes les actions marketing applicables pour la stratégie. L’URI d’une action marketing est fourni sous `_links.self.href` la réponse pour la [recherche d’une action](./marketing-actions.md#look-up)marketing. |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas d’utilisation de la stratégie. |
| `deny` | L’expression de stratégie qui décrit l’utilisation spécifique des données ne peut pas être exécutée sur laquelle l’action marketing associée à la stratégie est limitée. Voir la section sur la [création d’une stratégie](#create-policy) pour plus d’informations sur cette propriété. |

**Réponse**

Une réponse réussie renvoie les détails de la stratégie mise à jour.

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
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Update a portion of a custom policy {#patch}

>[!IMPORTANT]
>
>Vous pouvez uniquement mettre à jour des stratégies personnalisées. Si vous souhaitez activer ou désactiver les stratégies de base, reportez-vous à la section relative à la [mise à jour de la liste des stratégies](#update-enabled-core)de base activées.

Vous pouvez mettre à jour une partie spécifique d’une stratégie à l’aide d’une requête PATCH. Contrairement aux demandes de PUT qui réécrivent la stratégie, les demandes de PATCH mettent à jour uniquement les propriétés spécifiées dans le corps de la demande. Cela s’avère particulièrement utile lorsque vous souhaitez activer ou désactiver une stratégie, car vous devez uniquement indiquer le chemin d’accès à la propriété (`/status`) appropriée et sa valeur (`ENABLED` ou `DISABLED`).

>[!NOTE]
>
>Les charges utiles pour les requêtes de PATCH suivent le formatage du correctif JSON. Pour plus d’informations sur la syntaxe acceptée, consultez le guide [des principes de base de l’](../../landing/api-fundamentals.md) API.

L’ [!DNL Policy Service] API prend en charge les opérations de correctif JSON `add`, `remove`et `replace`et vous permet de combiner plusieurs mises à jour en un seul appel, comme illustré dans l’exemple ci-dessous.

**Format d’API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Le nom `id` de la stratégie dont vous souhaitez mettre à jour les propriétés. |

**Requête**

La requête suivante utilise deux `replace` opérations pour modifier l’état de la stratégie `DRAFT` en `ENABLED`et pour mettre à jour le `description` champ avec une nouvelle description.

>[!IMPORTANT]
>
>Lors de l&#39;envoi de plusieurs opérations de PATCH dans une seule requête, elles sont traitées dans l&#39;ordre dans lequel elles apparaissent dans la baie. Assurez-vous que vous envoyez les requêtes dans le bon ordre, si nécessaire.

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

Une réponse réussie renvoie les détails de la stratégie mise à jour.


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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Suppression d’une stratégie personnalisée {#delete}

You can delete a custom policy by including its `id` in the path of a DELETE request.

>[!WARNING]
>
>Les stratégies supprimées ne peuvent pas être récupérées. It is best practice to [perform a lookup (GET) request](#lookup) first to view the policy and confirm it is the correct policy you wish to remove.

**Format d’API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | ID de la stratégie à supprimer. |

**Requête**

```sh
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 (OK) avec un corps vide.

Vous pouvez confirmer la suppression en tentant de rechercher (GET) à nouveau la stratégie. Vous devriez recevoir une erreur HTTP 404 (introuvable) si la stratégie a été correctement supprimée.

## Récupérer une liste de stratégies de base activées {#list-enabled-core}

Par défaut, seules les stratégies d’utilisation des données activées participent à l’évaluation. Vous pouvez récupérer une liste de stratégies de base actuellement activées par votre organisation en adressant une demande de GET au point de `/enabledCorePolicies` terminaison.

**Format d’API**

```http
GET /enabledCorePolicies
```

**Requête**

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la liste des stratégies de base activées sous une `policyIds` matrice.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Mettre à jour la liste des stratégies de base activées {#update-enabled-core}

Par défaut, seules les stratégies d’utilisation des données activées participent à l’évaluation. En adressant une requête de PUT au point de `/enabledCorePolicies` terminaison, vous pouvez mettre à jour la liste des stratégies de base activées pour votre organisation à l’aide d’un seul appel.

>[!NOTE]
>
>Seules les stratégies de base peuvent être activées ou désactivées par ce point de terminaison. Pour activer ou désactiver des stratégies personnalisées, reportez-vous à la section relative à la [mise à jour d’une partie d’une stratégie](#patch).

**Format d’API**

```http
PUT /enabledCorePolicies
```

**Requête**

La requête suivante met à jour la liste des stratégies de base activées en fonction des ID fournis dans la charge utile.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `policyIds` | Liste des identifiants de stratégie principaux à activer. Toutes les politiques de base qui ne sont pas incluses sont définies comme `DISABLED` statut et ne participeront pas à l’évaluation. |

**Réponse**

Une réponse réussie renvoie la liste mise à jour des stratégies principales activées sous une `policyIds` baie.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Étapes suivantes

Une fois que vous avez défini de nouvelles stratégies ou mis à jour des stratégies existantes, vous pouvez utiliser l’ [!DNL Policy Service] API pour tester les actions marketing par rapport à des étiquettes ou des jeux de données spécifiques et voir si vos stratégies génèrent des violations comme prévu. Consultez le guide sur les points de terminaison [de l’évaluation des](./evaluation.md) politiques pour en savoir plus.
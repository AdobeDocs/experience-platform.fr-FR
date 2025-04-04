---
keywords: Experience Platform;accueil;rubriques populaires Application des politiques;Application basée sur lʼAPI;gouvernance des données
solution: Experience Platform
title: Point d’entrée de l’API des politiques de gouvernance des données
description: Les politiques de gouvernance des données sont des règles adoptées par votre organisation qui décrivent les types d’actions marketing que vous êtes autorisé(e) ou non à effectuer sur les données dans Experience Platform. Le point d’entrée « /policies » est utilisé pour tous les appels d’API liés à lʼaffichage, la création, la mise à jour ou la suppression des politiques de gouvernance des données.
role: Developer
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 98%

---

# Point d’entrée des politiques de gouvernance des données

Les politiques de gouvernance des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé(e) ou non à effectuer sur des données dans [!DNL Experience Platform]. Le point d’entrée `/policies` dans l’[!DNL Policy Service API] vous permet de gérer par programmation les politiques de gouvernance des données pour votre organisation.

>[!IMPORTANT]
>
>Les politiques de gouvernance ne doivent pas être confondues avec les politiques de contrôle d’accès, qui déterminent les attributs de données spécifiques accessibles par certains utilisateurs et utilisatrices d’Experience Platform dans votre organisation. Reportez-vous au guide du point d’entrée `/policies` de l’[API de contrôle d’accès](../../access-control/abac/api/policies.md) pour plus d’informations sur la gestion par programmation des politiques de contrôle d’accès.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Récupération dʼune liste de politiques {#list}

Vous pouvez répertorier toutes les politiques `core` ou `custom` en effectuant une requête GET à `/policies/core` ou `/policies/custom`, respectivement.

**Format d’API**

```http
GET /policies/core
GET /policies/custom
```

**Requête**

La requête suivante récupère une liste de politiques personnalisées définies par votre organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie comprend un tableau `children` qui répertorie les détails de chaque politique récupérée, y compris leurs valeurs `id`. Vous pouvez utiliser le champ `id` dʼune politique spécifique pour effectuer des requêtes de [recherche](#lookup), de [mise à jour](#update) et de [suppression](#delete) pour cette politique.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `_page.count` | Nombre total de politiques récupérées. |
| `name` | Nom dʼaffichage dʼune politique. |
| `status` | État actuel dʼune politique. Il existe trois états possibles : `DRAFT`, `ENABLED` ou `DISABLED`. Par défaut, seules les politiques `ENABLED` participent à lʼévaluation. Pour plus dʼinformations, consultez la présentation sur lʼ[évaluation des politiques](../enforcement/overview.md). |
| `marketingActionRefs` | Tableau qui répertorie les URI de toutes les actions marketing applicables pour une politique. |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas dʼutilisation de la politique. |
| `deny` | Objet qui décrit les étiquettes dʼutilisation des données spécifiques sur lesquelles lʼaction marketing associée à une politique ne peut pas être effectuée. Pour plus dʼinformations sur cette propriété, consultez la section [Création dʼune politique](#create-policy). |

## Recherche dʼune politique {#look-up}

Vous pouvez rechercher une politique spécifique en incluant la propriété `id` de cette politique dans le chemin dʼune requête GET.

**Format d’API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Champ `id` de la politique que vous souhaitez rechercher. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la politique.

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
    "imsOrg": "{ORG_ID}",
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
| `name` | Nom dʼaffichage de la politique. |
| `status` | État actuel de la politique. Il existe trois états possibles : `DRAFT`, `ENABLED` ou `DISABLED`. Par défaut, seules les politiques `ENABLED` participent à lʼévaluation. Pour plus dʼinformations, consultez la présentation sur lʼ[évaluation des politiques](../enforcement/overview.md). |
| `marketingActionRefs` | Tableau qui répertorie les URI de toutes les actions marketing applicables pour la politique. |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas dʼutilisation de la politique. |
| `deny` | Objet qui décrit les étiquettes dʼutilisation des données spécifiques sur lesquelles lʼaction marketing associée à la politique ne peut pas être effectuée. Pour plus dʼinformations sur cette propriété, consultez la section [Création dʼune politique](#create-policy). |

## Création dʼune politique personnalisée {#create-policy}

Dans lʼAPI [!DNL Policy Service], une politique est définie par les éléments suivants :

* référence à une action marketing spécifique
* expression décrivant les étiquettes dʼutilisation des données pour lesquelles lʼaction marketing ne peut pas être effectuée.

Pour satisfaire à cette dernière exigence, les définitions des politiques doivent inclure une expression booléenne par rapport à la présence dʼétiquettes dʼutilisation des données. Cette expression sʼappelle une expression de politique.

Les expressions de politique sont fournies sous la forme dʼune propriété `deny` dans chaque définition de politique. Voici un exemple dʼobjet `deny` simple qui vérifie uniquement la présence dʼune seule étiquette :

```json
"deny": {
    "label": "C1"
}
```

Cependant, de nombreuses politiques spécifient des conditions plus complexes par rapport à la présence dʼétiquettes dʼutilisation des données. Pour prendre en charge ces cas dʼutilisation, vous pouvez également inclure des opérations booléennes pour décrire vos expressions de politique. Lʼobjet dʼexpression de politique doit contenir soit une étiquette soit un opérateur et des opérandes, mais pas les deux. De même, chaque opérande est également un objet d’expression de politique.

Par exemple, afin de définir une politique qui interdit lʼexécution dʼune action marketing sur des données contenant des étiquettes `C1 OR (C3 AND C7)`, la propriété `deny` de la politique est spécifiée comme suit :

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
| `operator` | Indique la relation conditionnelle entre les étiquettes fournies dans le tableau `operands` frère. Les valeurs acceptées sont les suivantes : <ul><li>`OR` : lʼexpression est résolue en « true » si lʼune des étiquettes du tableau `operands` est présente.</li><li>`AND` : lʼexpression est résolue en « true » uniquement si toutes les étiquettes du tableau `operands` sont présentes.</li></ul> |
| `operands` | Tableau dʼobjets, chaque objet représentant soit une seule étiquette, soit une paire supplémentaire de propriétés `operator` et `operands`. La présence des étiquettes et/ou des opérations dans un tableau `operands` est résolue en « true » ou « false » en fonction de la valeur de sa propriété `operator` frère. |
| `label` | Nom dʼune étiquette unique dʼutilisation des données qui sʼapplique à la politique. |

Vous pouvez créer une nouvelle politique personnalisée en effectuant une requête POST vers le point d’entrée `/policies/custom`.

**Format d’API**

```http
POST /policies/custom
```

**Requête**

La requête suivante crée une nouvelle politique qui limite lʼexécution de lʼaction marketing `exportToThirdParty` sur les données contenant des étiquettes `C1 OR (C3 AND C7)`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Nom dʼaffichage de la politique. |
| `status` | État actuel de la politique. Il existe trois états possibles : `DRAFT`, `ENABLED` ou `DISABLED`. Par défaut, seules les politiques `ENABLED` participent à lʼévaluation. Pour plus dʼinformations, consultez la présentation sur lʼ[évaluation des politiques](../enforcement/overview.md). |
| `marketingActionRefs` | Tableau qui répertorie les URI de toutes les actions marketing applicables pour la politique. LʼURI dʼune action marketing est indiqué sous `_links.self.href` dans la réponse pour la [recherche dʼune action marketing](./marketing-actions.md#look-up). |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas dʼutilisation de la politique. |
| `deny` | Lʼexpression de politique qui décrit les étiquettes dʼutilisation des données spécifiques sur lesquelles lʼaction marketing associée à la politique ne peut pas être exécutée. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle politique créée, y compris son `id`. Cette valeur est en lecture seule et s’affiche automatiquement lors de la création de la politique.

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
    "imsOrg": "{ORG_ID}",
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

## Mise à jour dʼune politique personnalisée {#update}

>[!IMPORTANT]
>
>Vous pouvez uniquement mettre à jour des politiques personnalisées. Si vous souhaitez activer ou désactiver des politiques de base, consultez la section [Mise à jour de la liste des politiques de base activées](#update-enabled-core).

Vous pouvez mettre à jour une politique personnalisée existante en fournissant son identifiant dans le chemin dʼune requête PUT avec une payload qui inclut la version actualisée de la politique dans son intégralité. En dʼautres termes, la requête PUT réécrit essentiellement la politique.

>[!NOTE]
>
>Reportez-vous à la section [Mise à jour dʼune partie dʼune politique personnalisée](#patch) si vous souhaitez uniquement mettre à jour un ou plusieurs champs dʼune politique, plutôt que de la remplacer.

**Format d’API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Champ `id` de la politique à mettre à jour. |

**Requête**

Dans cet exemple, les conditions d’exportation des données vers un tiers ont été modifiées. Vous devez définir la politique créée de sorte qu’elle rejette cette action marketing en présence d’étiquettes de données `C1 AND C5`.

La requête suivante met à jour la politique existante pour inclure la nouvelle expression de politique. Remarquez que puisque cette requête réécrit essentiellement la politique, tous les champs doivent être inclus dans la payload, même si certaines de leurs valeurs ne sont pas mises à jour.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Nom dʼaffichage de la politique. |
| `status` | État actuel de la politique. Il existe trois états possibles : `DRAFT`, `ENABLED` ou `DISABLED`. Par défaut, seules les politiques `ENABLED` participent à lʼévaluation. Pour plus dʼinformations, consultez la présentation sur lʼ[évaluation des politiques](../enforcement/overview.md). |
| `marketingActionRefs` | Tableau qui répertorie les URI de toutes les actions marketing applicables pour la politique. LʼURI dʼune action marketing est indiqué sous `_links.self.href` dans la réponse pour la [recherche dʼune action marketing](./marketing-actions.md#look-up). |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas dʼutilisation de la politique. |
| `deny` | Lʼexpression de politique qui décrit les étiquettes dʼutilisation des données spécifiques sur lesquelles lʼaction marketing associée à la politique ne peut pas être exécutée. Pour plus dʼinformations sur cette propriété, consultez la section [Création dʼune politique](#create-policy). |

**Réponse**

Une réponse réussie renvoie les détails de la politique mise à jour.

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
    "imsOrg": "{ORG_ID}",
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

## Mise à jour dʼune partie dʼune politique {#patch}

>[!IMPORTANT]
>
>Vous pouvez uniquement mettre à jour des politiques personnalisées. Si vous souhaitez activer ou désactiver des politiques de base, consultez la section [Mise à jour de la liste des politiques de base activées](#update-enabled-core).

Vous pouvez mettre à jour une partie spécifique d’une politique à l’aide d’une requête PATCH. Contrairement aux requêtes PUT qui réécrivent la politique, les requêtes PATCH ne mettent à jour que les propriétés spécifiées dans le corps de la requête. Cela sʼavère particulièrement utile lorsque vous souhaitez activer ou désactiver une politique, car vous devez uniquement fournir le chemin dʼaccès à la propriété appropriée (`/status`) et sa valeur (`ENABLED` ou `DISABLED`).

>[!NOTE]
>
>Les payloads pour les requêtes PATCH respectent le format JSON Patch. Pour plus dʼinformations sur la syntaxe acceptée, consultez le [guide des principes de base des API](../../landing/api-fundamentals.md).

LʼAPI [!DNL Policy Service] prend en charge les opérations JSON Patch `add`, `remove`, `replace` et vous permet de combiner plusieurs mises à jour en un seul appel, comme illustré dans lʼexemple ci-dessous.

**Format d’API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Champ `id` de la politique dont vous souhaitez mettre à jour les propriétés. |

**Requête**

La requête suivante utilise deux opérations `replace` pour modifier lʼétat de la politique de `DRAFT` à `ENABLED` et pour mettre à jour le champ `description` avec une nouvelle description.

>[!IMPORTANT]
>
>Lors de lʼenvoi de plusieurs opérations PATCH dans une seule requête, elles seront traitées dans lʼordre dans lequel elles apparaissent dans le tableau. Assurez-vous que vous envoyez les requêtes dans le bon ordre, si nécessaire.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie les détails de la politique mise à jour.


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
    "imsOrg": "{ORG_ID}",
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

## Suppression dʼune politique personnalisée {#delete}

Vous pouvez supprimer une politique personnalisée en incluant son `id` dans le chemin dʼaccès dʼune requête DELETE.

>[!WARNING]
>
>Les politiques supprimées ne peuvent pas être récupérées. Il est recommandé dʼ[effectuer une requête de recherche GET](#lookup) avant dʼafficher la politique et de confirmer quʼil sʼagit bien de la politique à supprimer.

**Format d’API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Lʼidentifiant de la politique que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie lʼétat HTTP 200 (OK) avec un corps vide.

Vous pouvez confirmer la suppression de la politique en la recherchant à lʼaide de GET. Vous devriez recevoir une erreur HTTP 404 (Not Found) si la politique a bien été supprimée.

## Récupération dʼune liste de politiques de base activées {#list-enabled-core}

Par défaut, seules les politiques de gouvernance des données activées participent à lʼévaluation. Vous pouvez récupérer une liste de politiques de base actuellement activées par votre organisation en réalisant une requête GET au point d’entrée `/enabledCorePolicies`.

**Format d’API**

```http
GET /enabledCorePolicies
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la liste des politiques de base activées sous un tableau `policyIds`.

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
  "imsOrg": "{ORG_ID}",
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

## Mise à jour de la liste des politiques de base activées {#update-enabled-core}

Par défaut, seules les politiques de gouvernance des données activées participent à lʼévaluation. En réalisant une requête PUT au point d’entrée `/enabledCorePolicies`, vous pouvez mettre à jour la liste des politiques de base activées pour votre organisation en un seul appel.

>[!NOTE]
>
>Seules les politiques de base peuvent être activées ou désactivées par ce point d’entrée. Pour activer ou désactiver des politiques personnalisées, consultez la section [Mise à jour dʼune partie dʼune politique](#patch).

**Format d’API**

```http
PUT /enabledCorePolicies
```

**Requête**

La requête suivante met à jour la liste des politiques de base activées en fonction des identifiants fournis dans la payload.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `policyIds` | Liste dʼidentifiants de politiques de base à activer. Toutes les politiques de base qui ne sont pas incluses sont définies sur lʼétat `DISABLED` et ne participeront pas à lʼévaluation. |

**Réponse**

Une réponse réussie renvoie la liste mise à jour des politiques de base activées sous un tableau `policyIds`.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
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

Une fois que vous avez défini de nouvelles politiques ou mis à jour des politiques existantes, vous pouvez utiliser lʼAPI [!DNL Policy Service] pour tester les actions marketing par rapport à des étiquettes ou des jeux de données spécifiques et voir si vos politiques génèrent des violations comme prévu. Pour plus dʼinformations, consultez le guide sur les [points d’entrée dʼévaluation des politiques](./evaluation.md).

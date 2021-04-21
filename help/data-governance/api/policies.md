---
keywords: Experience Platform ; accueil ; rubriques populaires ; Application des stratégies ; Application basée sur les API ; gouvernance des données
solution: Experience Platform
title: Point de terminaison de l’API Stratégies
topic-legacy: developer guide
description: Les stratégies d’utilisation des données sont des règles adoptées par votre organisation qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur les données au sein d’Experience Platform. Le point de terminaison /policies est utilisé pour tous les appels d’API liés à l’affichage, la création, la mise à jour ou la suppression des stratégies d’utilisation des données.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 9%

---

# Point de terminaison des stratégies

Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé à exécuter, ou dont vous êtes limité à l’exécution, sur les données dans [!DNL Experience Platform]. Le point de terminaison `/policies` de [!DNL Policy Service API] vous permet de gérer par programmation les stratégies d&#39;utilisation des données pour votre entreprise.

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie de l&#39;[[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API [!DNL Experience Platform].

## Récupérer une liste de stratégies {#list}

Vous pouvez liste toutes les stratégies `core` ou `custom` en adressant une demande de GET à `/policies/core` ou `/policies/custom`, respectivement.

**Format d’API**

```http
GET /policies/core
GET /policies/custom
```

**Requête**

La requête suivante récupère une liste de stratégies personnalisées définies par votre organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie comprend un tableau `children` qui liste les détails de chaque stratégie récupérée, y compris leurs valeurs `id`. Vous pouvez utiliser le champ `id` d&#39;une stratégie spécifique pour exécuter des requêtes [recherche](#lookup), [mise à jour](#update) et [supprimer](#delete) pour cette stratégie.

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
| `status` | Statut actuel d’une stratégie. Il existe trois états possibles : `DRAFT`, `ENABLED` ou `DISABLED`. Par défaut, seules les stratégies `ENABLED` participent à l’évaluation. Pour plus d&#39;informations, consultez l&#39;aperçu de [l&#39;évaluation des politiques](../enforcement/overview.md). |
| `marketingActionRefs` | Tableau qui liste les URI de toutes les actions marketing applicables pour une stratégie. |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas d’utilisation de la stratégie. |
| `deny` | Objet qui décrit les étiquettes d’utilisation de données spécifiques sur lesquelles l’action marketing associée à une stratégie ne peut pas être exécutée. Pour plus d&#39;informations sur cette propriété, consultez la section [Création d&#39;une stratégie](#create-policy). |

## Rechercher une stratégie {#look-up}

Vous pouvez rechercher une stratégie spécifique en incluant la propriété `id` de cette stratégie dans le chemin d&#39;une demande de GET.

**Format d’API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | `id` de la stratégie que vous souhaitez rechercher. |

**Requête**

```shell
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
| `status` | Statut actuel de la stratégie. Il existe trois états possibles : `DRAFT`, `ENABLED` ou `DISABLED`. Par défaut, seules les stratégies `ENABLED` participent à l’évaluation. Pour plus d&#39;informations, consultez l&#39;aperçu de [l&#39;évaluation des politiques](../enforcement/overview.md). |
| `marketingActionRefs` | Tableau qui liste les URI de toutes les actions marketing applicables pour la stratégie. |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas d’utilisation de la stratégie. |
| `deny` | Objet qui décrit les étiquettes d’utilisation de données spécifiques sur lesquelles l’action marketing associée à la stratégie ne peut pas être exécutée. Pour plus d&#39;informations sur cette propriété, consultez la section [Création d&#39;une stratégie](#create-policy). |

## Créer une stratégie personnalisée {#create-policy}

Dans l&#39;API [!DNL Policy Service], une stratégie est définie par les éléments suivants :

* Référence à une action marketing spécifique
* Expression décrivant les étiquettes d’utilisation des données pour lesquelles l’action marketing ne peut pas être exécutée par rapport à

Pour satisfaire à cette dernière exigence, les définitions de stratégie doivent inclure une expression booléenne concernant la présence d’étiquettes d’utilisation des données. Cette expression s&#39;appelle une expression de politique.

Les expressions de stratégie sont fournies sous la forme d&#39;une propriété `deny` au sein de chaque définition de stratégie. Voici un exemple d&#39;objet `deny` simple qui ne vérifie la présence que d&#39;une seule étiquette :

```json
"deny": {
    "label": "C1"
}
```

Cependant, de nombreuses stratégies spécifient des conditions plus complexes concernant la présence d’étiquettes d’utilisation des données. Pour prendre en charge ces cas d’utilisation, vous pouvez également inclure des opérations booléennes pour décrire vos expressions de stratégie. L’objet d’expression de stratégie doit contenir un libellé ou un opérateur et des opérandes, mais pas les deux. De même, chaque opérande est également un objet d’expression de stratégie.

Par exemple, afin de définir une stratégie qui interdit l’exécution d’une action marketing sur des données contenant des étiquettes `C1 OR (C3 AND C7)`, la propriété `deny` de la stratégie est spécifiée comme suit :

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
| `operator` | Indique la relation conditionnelle entre les étiquettes fournies dans le tableau `operands` frère. Les valeurs acceptées sont les suivantes : <ul><li>`OR`: L&#39;expression est résolue sur true si l&#39;un des libellés du  `operands` tableau est présent.</li><li>`AND`: L&#39;expression se résout sur true uniquement si tous les libellés du  `operands` tableau sont présents.</li></ul> |
| `operands` | Tableau d’objets, chaque objet représentant soit une seule étiquette, soit une paire supplémentaire de propriétés `operator` et `operands`. La présence des libellés et/ou des opérations dans un tableau `operands` est résolue sur true ou false en fonction de la valeur de sa propriété `operator` frère. |
| `label` | Nom d’une étiquette d’utilisation de données unique qui s’applique à la stratégie. |

Vous pouvez créer une stratégie personnalisée en adressant une requête de POST au point de terminaison `/policies/custom`.

**Format d’API**

```http
POST /policies/custom
```

**Requête**

La requête suivante crée une nouvelle stratégie qui limite l&#39;action marketing `exportToThirdParty` à l&#39;exécution sur les données contenant des étiquettes `C1 OR (C3 AND C7)`.

```shell
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
| `status` | Statut actuel de la stratégie. Il existe trois états possibles : `DRAFT`, `ENABLED` ou `DISABLED`. Par défaut, seules les stratégies `ENABLED` participent à l’évaluation. Pour plus d&#39;informations, consultez l&#39;aperçu de [l&#39;évaluation des politiques](../enforcement/overview.md). |
| `marketingActionRefs` | Tableau qui liste les URI de toutes les actions marketing applicables pour la stratégie. L&#39;URI d&#39;une action marketing est indiqué sous `_links.self.href` dans la réponse pour [recherche d&#39;une action marketing](./marketing-actions.md#look-up). |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas d’utilisation de la stratégie. |
| `deny` | L’expression de stratégie qui décrit l’utilisation spécifique des données ne peut pas être exécutée sur laquelle l’action marketing associée à la stratégie est limitée. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle stratégie, y compris son `id`. Cette valeur est en lecture seule et s’affiche automatiquement lors de la création de la stratégie.

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
>Vous pouvez uniquement mettre à jour des stratégies personnalisées. Si vous souhaitez activer ou désactiver les stratégies de base, consultez la section [mise à jour de la liste des stratégies de base activées](#update-enabled-core).

Vous pouvez mettre à jour une stratégie personnalisée existante en fournissant son identifiant dans le chemin d’une demande de PUT avec une charge utile qui inclut la forme mise à jour de la stratégie dans son intégralité. En d&#39;autres termes, la demande du PUT réécrit essentiellement la politique.

>[!NOTE]
>
>Reportez-vous à la section [mise à jour d&#39;une partie d&#39;une stratégie personnalisée](#patch) si vous souhaitez uniquement mettre à jour un ou plusieurs champs d&#39;une stratégie, plutôt que de la remplacer.

**Format d’API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | `id` de la stratégie que vous souhaitez mettre à jour. |

**Requête**

Dans cet exemple, les conditions d’exportation des données vers un tiers ont été modifiées. Vous devez définir la stratégie créée de sorte qu’elle rejette cette action marketing en présence d’étiquettes de données `C1 AND C5`. 

La requête suivante met à jour la stratégie existante pour inclure la nouvelle expression de stratégie. Notez que puisque cette requête réécrit essentiellement la stratégie, tous les champs doivent être inclus dans la charge utile, même si certaines de leurs valeurs ne sont pas mises à jour.

```shell
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
| `status` | Statut actuel de la stratégie. Il existe trois états possibles : `DRAFT`, `ENABLED` ou `DISABLED`. Par défaut, seules les stratégies `ENABLED` participent à l’évaluation. Pour plus d&#39;informations, consultez l&#39;aperçu de [l&#39;évaluation des politiques](../enforcement/overview.md). |
| `marketingActionRefs` | Tableau qui liste les URI de toutes les actions marketing applicables pour la stratégie. L&#39;URI d&#39;une action marketing est indiqué sous `_links.self.href` dans la réponse pour [recherche d&#39;une action marketing](./marketing-actions.md#look-up). |
| `description` | Description facultative qui fournit un contexte plus détaillé au cas d’utilisation de la stratégie. |
| `deny` | L’expression de stratégie qui décrit l’utilisation spécifique des données ne peut pas être exécutée sur laquelle l’action marketing associée à la stratégie est limitée. Pour plus d&#39;informations sur cette propriété, consultez la section [Création d&#39;une stratégie](#create-policy). |

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

## Mettre à jour une partie d&#39;une stratégie personnalisée {#patch}

>[!IMPORTANT]
>
>Vous pouvez uniquement mettre à jour des stratégies personnalisées. Si vous souhaitez activer ou désactiver les stratégies de base, consultez la section [mise à jour de la liste des stratégies de base activées](#update-enabled-core).

Vous pouvez mettre à jour une partie spécifique d’une stratégie à l’aide d’une requête PATCH. Contrairement aux demandes de PUT qui réécrivent la stratégie, les demandes de PATCH mettent à jour uniquement les propriétés spécifiées dans le corps de la demande. Cela s’avère particulièrement utile lorsque vous souhaitez activer ou désactiver une stratégie, car vous devez uniquement indiquer le chemin d’accès à la propriété appropriée (`/status`) et sa valeur (`ENABLED` ou `DISABLED`).

>[!NOTE]
>
>Les charges utiles pour les requêtes de PATCH suivent le formatage du correctif JSON. Pour plus d&#39;informations sur la syntaxe acceptée, consultez le [guide des fondamentaux de l&#39;API](../../landing/api-fundamentals.md).

L’API [!DNL Policy Service] prend en charge les opérations de correctif JSON `add`, `remove` et `replace` et vous permet de combiner plusieurs mises à jour en un seul appel, comme illustré dans l’exemple ci-dessous.

**Format d’API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | `id` de la stratégie dont vous souhaitez mettre à jour les propriétés. |

**Requête**

La requête suivante utilise deux opérations `replace` pour modifier l&#39;état de la stratégie de `DRAFT` en `ENABLED` et pour mettre à jour le champ `description` avec une nouvelle description.

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

## Supprimer une stratégie personnalisée {#delete}

Vous pouvez supprimer une stratégie personnalisée en incluant `id` dans le chemin d’une demande de DELETE.

>[!WARNING]
>
>Les stratégies supprimées ne peuvent pas être récupérées. Il est recommandé d&#39;[exécuter d&#39;abord une requête de recherche (GET)](#lookup) pour vue de la stratégie et de vérifier qu&#39;il s&#39;agit de la stratégie correcte que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | ID de la stratégie à supprimer. |

**Requête**

```shell
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

Par défaut, seules les stratégies d’utilisation des données activées participent à l’évaluation. Vous pouvez récupérer une liste de stratégies de base actuellement activées par votre organisation en adressant une demande de GET au point de terminaison `/enabledCorePolicies`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la liste des stratégies de base activées sous un tableau `policyIds`.

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

Par défaut, seules les stratégies d’utilisation des données activées participent à l’évaluation. En adressant une requête de PUT au point de terminaison `/enabledCorePolicies`, vous pouvez mettre à jour la liste des stratégies de base activées pour votre organisation à l’aide d’un seul appel.

>[!NOTE]
>
>Seules les stratégies de base peuvent être activées ou désactivées par ce point de terminaison. Pour activer ou désactiver des stratégies personnalisées, consultez la section [Mise à jour d&#39;une partie d&#39;une stratégie](#patch).

**Format d’API**

```http
PUT /enabledCorePolicies
```

**Requête**

La requête suivante met à jour la liste des stratégies de base activées en fonction des ID fournis dans la charge utile.

```shell
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
| `policyIds` | Liste des identifiants de stratégie principaux à activer. Toutes les stratégies de base qui ne sont pas incluses sont définies sur `DISABLED` statut et ne participeront pas à l’évaluation. |

**Réponse**

Une réponse réussie renvoie la liste mise à jour des stratégies de base activées sous un tableau `policyIds`.

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

Une fois que vous avez défini de nouvelles stratégies ou mis à jour des stratégies existantes, vous pouvez utiliser l&#39;API [!DNL Policy Service] pour tester les actions marketing par rapport à des étiquettes ou des jeux de données spécifiques et voir si vos stratégies génèrent des violations comme prévu. Pour plus d&#39;informations, consultez le guide sur les [points de terminaison de l&#39;évaluation des politiques](./evaluation.md).

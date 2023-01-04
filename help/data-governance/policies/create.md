---
keywords: Experience Platform;accueil;rubriques populaires;gouvernance des données;stratégie d’utilisation des données
solution: Experience Platform
title: Création d’une stratégie de gouvernance des données dans l’API
topic-legacy: policies
type: Tutorial
description: Découvrez comment créer une stratégie de gouvernance des données à l’aide de l’API Policy Service.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 91%

---

# Création d’une stratégie de gouvernance des données dans l’API

Le [API Policy Service](https://www.adobe.io/experience-platform-apis/references/policy-service/) vous permet de créer et de gérer des stratégies de gouvernance des données afin de déterminer quelles actions marketing peuvent être entreprises concernant les données qui contiennent certains libellés d’utilisation des données.

Ce document fournit un tutoriel détaillé sur la création d’une stratégie de gouvernance à l’aide du [!DNL Policy Service] API.

>[!NOTE]
>
>Pour savoir comment créer une stratégie de contrôle d’accès, voir `/policies` guide de point d’entrée pour [API Access Control](../../access-control/abac/api/policies.md). Pour savoir comment créer une stratégie de consentement, voir [guide de l’interface utilisateur des stratégies](./user-guide.md#consent-policy).

## Prise en main

Ce tutoriel nécessite une compréhension pratique des concepts clés suivants, qui sont impliqués dans la création et l’évaluation des stratégies

* [Adobe Experience Platform Data Governance](../home.md) : cadre en fonction duquel [!DNL Platform] applique la conformité d’utilisation des données.
   * [Libellés d’utilisation des données](../labels/overview.md) : les libellés d’utilisation des données sont appliqués aux champs de données XDM, spécifiant les restrictions d’accès à ces données.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
* [Environnements de test](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Avant de commencer ce tutoriel, consultez le [guide de développement](../api/getting-started.md) pour obtenir les informations importantes à connaître afin d’effectuer avec succès des appels vers l’API [!DNL Policy Service], y compris les en-têtes requis et la méthode de lecture d’exemples d’appels API.

## Définition d’une action marketing {#define-action}

Dans le cadre de la gouvernance des données, une action marketing est une action entreprise par un utilisateur de données [!DNL Experience Platform] pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

La première étape de la création d’une stratégie d’utilisation des données consiste à déterminer l’action marketing évaluée par la stratégie. Pour ce faire, utilisez l’une des options suivantes :

* [Recherche d’une action marketing existante](#look-up)
* [Création d’une action marketing](#create-new)

### Recherche d’une action marketing existante {#look-up}

Vous pouvez rechercher des actions marketing existantes à évaluer par votre stratégie à l’aide d’une requête GET envoyée à l’un des points de terminaison `/marketingActions`.

**Format d’API**

Selon que vous recherchiez une action marketing fournie par [!DNL Experience Platform] ou une action marketing personnalisée créée par votre organisation, utilisez respectivement les points d’entrée `marketingActions/core` ou `marketingActions/custom`.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Requête**

La requête suivante utilise le point de terminaison `marketingActions/custom`, qui récupère une liste de toutes les actions marketing définies par votre organisation IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie le nombre total d’actions marketing trouvées (`count`) et liste les détails des actions marketing en elles-mêmes dans le tableau `children`.

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{ORG_ID}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `_links.self.href` | Chaque élément du tableau `children` contient un identifiant d’URI pour l’action marketing listée. |

Lorsque vous trouvez l’action marketing à utiliser, enregistrez la valeur de sa propriété `href`. Cette valeur est utilisée lors de l’étape suivante de la [création d’une stratégie](#create-policy).

### Création d’une action marketing {#create-new}

Vous pouvez créer une action marketing à l’aide d’une requête PUT envoyée au point de terminaison `/marketingActions/custom/` et en fournissant un nom pour l’action marketing à la fin du chemin d’accès de la requête.

**Format d’API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing que vous souhaitez créer. Ce nom agit comme l’identifiant principal de l’action marketing et doit donc être unique. Il est recommandé de donner à l’action marketing un nom descriptif, mais concis. |

**Requête**

La requête suivante crée une action marketing personnalisée appelée « exportToThirdParty ». Notez que dans le payload de la requête, `name` est identique au nom fourni dans le chemin d’accès de la requête.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de l’action marketing que vous souhaitez créer. Ce nom doit correspondre au nom fourni dans le chemin d’accès de la requête ou une erreur 400 (Bad Request) se produira. |
| `description` | Description lisible par l’utilisateur de l’action marketing. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et les détails de l’action marketing nouvellement créée.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| Propriété | Description |
| --- | --- |
| `_links.self.href` | Identifiant d’URI de l’action marketing. |

Enregistrez l’identifiant d’URI de l’action marketing nouvellement créée, car il sera utilisé à l’étape suivante de la création d’une stratégie

## Création d’une stratégie {#create-policy}

Pour créer une stratégie, vous devez fournir l’identifiant d’URI d’une action marketing avec l’expression des libellés d’utilisation qui interdisent cette action marketing.

Cette expression, appelée expression de stratégie, est un objet contenant soit (a) un libellé, soit (b) un opérateur et des opérandes, mais pas les deux. De même, chaque opérande est également un objet d’expression de stratégie. Par exemple, une stratégie relative à l’exportation de données vers un tiers peut être interdite en présence de libellés`C1 OR (C3 AND C7)`. Cette expression serait spécifiée comme suit :

```json
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
}
```

>[!NOTE]
>
>Seuls les opérateurs OR et AND sont pris en charge.

Une fois l’expression de stratégie définie, vous pouvez créer une stratégie à l’aide d’une requête POST envoyée au point de terminaison `/policies/custom`.

**Format d’API**

```http
POST /policies/custom
```

**Requête**

La requête suivante crée une stratégie appelée « Export Data to Third Party » en fournissant une action marketing et une expression de stratégie dans le payload de la requête.

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

| Propriété | Description |
| --- | --- |
| `marketingActionRefs` | Tableau contenant la valeur `href` d’une action marketing, obtenue à l’[étape précédente](#define-action). Bien que l’exemple ci-dessus ne liste qu’une action marketing, il est possible de fournir plusieurs actions. |
| `deny` | Objet de l’expression de stratégie. Définit les conditions et les libellés d’utilisation qui entraîneraient le rejet par la stratégie de l’action marketing référencée dans `marketingActionRefs`. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et les détails de la stratégie nouvellement créée.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
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
    "imsOrg": "{ORG_ID}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| Propriété | Description |
| --- | --- |
| `id` | Valeur générée par le système en lecture seule et qui identifie la stratégie de manière unique. |

Enregistrez l’identifiant d’URI de la stratégie nouvellement créée, car il est utilisé à l’étape suivante pour activer la stratégie.

## Activation de la stratégie

>[!NOTE]
>
>Bien que cette étape soit facultative si vous souhaitez laisser votre stratégie à l’état `DRAFT`, veuillez noter que, par défaut, une stratégie doit avoir l’état `ENABLED` pour participer à l’évaluation. Consultez le guide sur l’[application des stratégies](../enforcement/api-enforcement.md) pour apprendre à créer des exceptions pour les stratégies dont l’état est défini sur `DRAFT`.

Par défaut, les stratégies dont la propriété `status` est définie sur `DRAFT` ne participent pas à l’évaluation. Vous pouvez activer votre stratégie pour l’évaluation à l’aide d’une requête PATCH envoyée au point de terminaison `/policies/custom/` et en fournissant l’identifiant unique de la stratégie à la fin du chemin d’accès de la requête.

**Format d’API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Valeur `id` de la stratégie à activer. |

**Requête**

La requête suivante effectue une opération PATCH sur la propriété `status` de la stratégie, changeant la valeur `DRAFT` en `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| Propriété | Description |
| --- | --- |
| `op` | Type d’opération PATCH à effectuer. Cette requête effectue une opération « replace ». |
| `path` | Chemin d’accès du champ à mettre à jour. Lors de l’activation d’une stratégie, la valeur doit être définie sur « /status ». |
| `value` | Nouvelle valeur à attribuer à la propriété spécifiée dans `path`. Cette requête définit la propriété `status` de la stratégie sur « ENABLED ». |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 (OK) et les détails de la stratégie mise à jour, où `status` est défini sur `ENABLED`.

```json
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
    "imsOrg": "{ORG_ID}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER}",
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
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une stratégie d’utilisation des données pour une action marketing. Vous pouvez maintenant continuer avec le tutoriel sur l’[application des stratégies d’utilisation des données](../enforcement/api-enforcement.md) afin d’apprendre à rechercher les violations de stratégie et à les traiter dans votre application d’expérience.

Pour plus d’informations sur les différentes opérations disponibles dans l’API [!DNL Policy Service], consultez le [guide de développement de Policy Service](../api/getting-started.md). Pour plus d’informations sur l’application des stratégies pour les données du [!DNL Real-Time Customer Profile], consultez le tutoriel sur l’[application de la conformité de l’utilisation des données aux segments d’audience](../../segmentation/tutorials/governance.md).

Pour découvrir comment gérer les stratégies d’utilisation dans l’interface utilisateur [!DNL Experience Platform], consultez le [guide d’utilisation des stratégies](user-guide.md).

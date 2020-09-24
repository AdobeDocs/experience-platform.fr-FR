---
keywords: Experience Platform;home;popular topics;data governance;data usage policy
solution: Experience Platform
title: Création d’une stratégie d’utilisation des données
topic: policies
type: Tutorial
description: L’API Policy Service vous permet de créer et de gérer des stratégies d’utilisation des données afin de déterminer les actions marketing à entreprendre par rapport aux données qui contiennent certains libellés d’utilisation des données. Ce document fournit un tutoriel détaillé sur la création d’une stratégie à l’aide de l’API Policy Service.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 72%

---


# Création d’une stratégie d’utilisation des données dans l’API

The [Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) allows you to create and manage data usage policies to determine what marketing actions can be taken against data that contains certain data usage labels.

This document provides a step-by-step tutorial for creating a policy using the [!DNL Policy Service] API. Pour consulter un guide plus complet sur les différentes opérations disponibles dans l’API, référez-vous au [guide de développement de Policy Service](../api/getting-started.md).

## Prise en main

Ce tutoriel nécessite une compréhension pratique des concepts clés suivants, qui sont impliqués dans la création et l’évaluation des stratégies 

* [[ !Gouvernance des données DNL]](../home.md): Cadre selon lequel [!DNL Platform] applique la conformité à l’utilisation des données.
* [Libellés d’utilisation des données](../labels/overview.md) : les libellés d’utilisation des données sont appliqués aux champs de données XDM, spécifiant les restrictions d’accès à ces données.
* [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

Avant de commencer ce tutoriel, consultez le [guide de développement](../api/getting-started.md) pour obtenir les informations importantes à connaître afin d’effectuer avec succès des appels vers l’API , y compris les en-têtes requis et la méthode de lecture d’exemples d’appels API.[!DNL Policy Service]

## Définition d’une action marketing {#define-action}

In the [!DNL Data Governance] framework, a marketing action is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies.

La première étape de la création d’une stratégie d’utilisation des données consiste à déterminer l’action marketing qu’elle évaluera. Pour ce faire, utilisez l’une des options suivantes :

* [Recherche d’une action marketing existante](#look-up)
* [Création d’une action marketing](#create-new)

### Recherche d’une action marketing existante {#look-up}

Vous pouvez rechercher des actions marketing existantes à évaluer par votre stratégie à l’aide d’une requête GET envoyée à l’un des points de terminaison `/marketingActions`.

**Format d’API**

Depending on whether you are looking up a marketing action provided by [!DNL Experience Platform] or a custom marketing action created by your organization, use the `marketingActions/core` or `marketingActions/custom` endpoints, respectively.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Lorsque vous trouvez l’action marketing à utiliser, enregistrez la valeur de sa propriété `href`. Cette valeur est utilisée lors de l’étape suivante de la [création d’une stratégie ](#create-policy).

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

Pour créer une nouvelle stratégie, vous devez fournir l’ID URI d’une action marketing avec une expression des étiquettes d’utilisation qui interdisent cette action marketing.

Cette expression, appelée **expression de stratégie**, est un objet contenant soit (a) un libellé , soit (b) un opérateur et des opérandes, mais pas les deux. De même, chaque opérande est également un objet d’expression de stratégie. Par exemple, une stratégie relative à l’exportation de données vers un tiers peut être interdite en présence de libellés`C1 OR (C3 AND C7)`. Cette expression serait spécifiée comme suit :

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

| Propriété | Description |
| --- | --- |
| `marketingActionRefs` | Tableau contenant la valeur `href` d’une action marketing, obtenue à l’[étape précédente](#define-action). Bien que l’exemple ci-dessus ne liste qu’une action marketing, il est possible de fournir plusieurs actions. |
| `deny` | Objet de l’expression de stratégie. Defines the usage labels and conditions that would cause the policy to reject the marketing action referenced in `marketingActionRefs`. |

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
    "imsOrg": "{IMS_ORG}",
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

## Activer la stratégie

>[!NOTE]
>
>Bien que cette étape soit facultative si vous souhaitez laisser votre stratégie à l’état `DRAFT`, veuillez noter que, par défaut, une stratégie doit avoir l’état `ENABLED` pour participer à l’évaluation. See the guide on [policy enforcement](../enforcement/api-enforcement.md) for information on how to make exceptions for policies in `DRAFT` status.

By default, policies that have their `status` property set to `DRAFT` do not participate in evaluation. Vous pouvez activer votre stratégie pour l’évaluation à l’aide d’une requête PATCH envoyée au point de terminaison `/policies/custom/` et en fournissant l’identifiant unique de la stratégie à la fin du chemin d’accès de la requête.

**Format d’API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Valeur `id` de la stratégie à activer. |

**Requête**

La requête suivante effectue une opération PATCH sur la propriété `status` de la stratégie , changeant la valeur `DRAFT` en `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

For more information on the different available operations in the [!DNL Policy Service] API,  see the [Policy Service developer guide](../api/getting-started.md). For information on how to enforce policies for [!DNL Real-time Customer Profile] data, see the tutorial on [enforcing data usage compliance for audience segments](../../segmentation/tutorials/governance.md).

To learn how to manage usage policies in the [!DNL Experience Platform] user interface, see the [policy user guide](user-guide.md).
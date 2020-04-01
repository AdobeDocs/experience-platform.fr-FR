---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’une stratégie d’utilisation des données
topic: policies
translation-type: tm+mt
source-git-commit: 04b2e07ba39df9f530c9c93c4bf1af9e2cf30169

---


# Création d’une stratégie d’utilisation des données

L’étiquetage et l’application de l’utilisation des données (DULE) constituent le mécanisme de base de la gouvernance des données d’Adobe Experience Platform. L’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service vous permet de créer et de gérer des stratégies DULE afin de déterminer quelles actions marketing peuvent être entreprises par rapport aux données contenant certains libellés DULE.

Ce fournit un didacticiel détaillé pour la création d’une stratégie DULE à l’aide de l’API Policy Service. Pour un guide plus complet sur les différentes opérations disponibles dans l’API, consultez le guide [du développeur](../api/getting-started.md)Policy Service.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des concepts clés suivants, qui sont impliqués dans la création et l&#39;évaluation des politiques DULE :

* [Gouvernance](../home.md)des données : Cadre selon lequel la plateforme applique la conformité à l’utilisation des données.
* [Libellés](../labels/overview.md)d’utilisation des données : Les libellés d’utilisation des données sont appliqués aux champs de données XDM, en spécifiant les restrictions d’accès à ces données.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Avant de commencer ce didacticiel, veuillez consulter le guide [du](../api/getting-started.md) développeur pour obtenir des informations importantes que vous devez connaître afin d’effectuer des appels à l’API du service de stratégie DULE, y compris les en-têtes requis et pour savoir comment lire des exemples d’appels d’API.

## Définir une action marketing {#define-action}

Dans le cadre de la gouvernance des données, une action marketing est une action entreprise par un utilisateur de données de la plateforme d’expérience, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

La première étape de la création d’une stratégie DULE consiste à déterminer l’action marketing que la stratégie évaluera. Pour ce faire, utilisez l’une des options suivantes :

* [Rechercher une action marketing existante](#look-up)
* [Créer une action marketing](#create-new)

### Rechercher une action marketing existante {#look-up}

Vous pouvez rechercher les actions marketing existantes à évaluer par votre stratégie DULE en envoyant une requête GET à l’un des `/marketingActions` points de fin.

**Format API**

Selon que vous recherchez une action marketing fournie par Experience Platform ou une action marketing personnalisée créée par votre entreprise, utilisez respectivement les points de fin `marketingActions/core` ou `marketingActions/custom` .

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Requête**

La requête suivante utilise le `marketingActions/custom` point de fin, qui récupère un de toutes les actions marketing définies par votre organisation IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie le nombre total d&#39;actions marketing trouvées (`count`) et le nombre de  les détails des actions marketing elles-mêmes dans la `children` baie.

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
| `_links.self.href` | Chaque élément du `children` tableau contient un ID URI pour l’action marketing répertoriée. |

Lorsque vous trouvez l’action marketing que vous souhaitez utiliser, enregistrez la valeur de sa `href` propriété. Cette valeur est utilisée lors de l’étape suivante de [création d’une stratégie](#create-policy)DULE.

### Créer une action marketing {#create-new}

Vous pouvez créer une nouvelle action marketing en faisant une requête PUT au point de `/marketingActions/custom/` fin et en fournissant un nom pour l’action marketing à la fin du chemin de la requête.

**Format API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de la nouvelle action marketing que vous souhaitez créer. Ce nom agit comme identifiant principal de l’action marketing et doit donc être unique. Il est recommandé de donner à l’action marketing un nom descriptif mais concis. |

**Requête**

La requête suivante crée une nouvelle action marketing personnalisée appelée &quot;exportToThirdParty&quot;. Notez que la charge `name` dans la requête est identique au nom fourni dans le chemin d’accès à la requête.

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
| `name` | Nom de l’action marketing à créer. Ce nom doit correspondre au nom fourni dans le chemin d’accès à la requête, sinon une erreur 400 (Requête incorrecte) se produira. |
| `description` | Description intelligible de l’action marketing. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et les détails de l’action marketing nouvellement créée.

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
| `_links.self.href` | ID URI de l’action marketing. |

Enregistrez l’ID URI de l’action marketing nouvellement créée, car il sera utilisé à l’étape suivante de la création d’une stratégie DULE.

## Création d’une stratégie DULE {#create-policy}

Pour créer une nouvelle stratégie, vous devez fournir l’ID URI d’une action marketing avec un  des étiquettes DULE qui interdisent cette action marketing.

Ce   est appelé une **stratégie** et est un objet contenant soit (A) une étiquette DULE, soit (B) un opérateur et des opérandes, mais pas les deux. En retour, chaque opérande est également un objet  de stratégie . Par exemple, une stratégie relative à l’exportation de données vers un tiers peut être interdite si `C1 OR (C3 AND C7)` des étiquettes sont présentes. Ce   de serait spécifié comme suit :

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

>[!NOTE] Seuls les opérateurs OR et AND sont pris en charge.

Une fois que vous avez configuré votre stratégie  , vous pouvez créer une nouvelle stratégie DULE en envoyant une requête POST au point de `/policies/custom` fin.

**Format API**

```http
POST /policies/custom
```

**Requête**

La requête suivante crée une stratégie DULE appelée &quot;Exporter les données vers un tiers&quot; en fournissant une action et une stratégie marketing   dans la charge utile de la requête.

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
| `marketingActionRefs` | Tableau contenant la `href` valeur d’une action marketing, obtenue à l’étape [](#define-action)précédente. Bien que l’exemple ci-dessus ne  qu’une seule action marketing, plusieurs actions peuvent également être fournies. |
| `deny` | La stratégie  l’objet . Définit les étiquettes et les conditions DULE qui entraîneraient le rejet par la stratégie de l’action marketing référencée dans `marketingActionRefs`. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et les détails de la nouvelle stratégie créée.

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
| `id` | Valeur générée par le système en lecture seule qui identifie de manière unique la stratégie DULE. |

Enregistrez l’ID URI de la nouvelle stratégie DULE, tel qu’il est utilisé à l’étape suivante pour activer la stratégie.

## Activation de la stratégie DULE

>[!NOTE] Bien que cette étape soit facultative si vous souhaitez laisser votre stratégie DULE en `DRAFT` état, veuillez noter que, par défaut, une stratégie doit avoir le statut `ENABLED` pour participer à l’évaluation. Consultez le didacticiel sur l’ [application des stratégies](../enforcement/api-enforcement.md) DULE pour savoir comment créer des exceptions pour les stratégies `DRAFT` d’état.

Par défaut, les stratégies DULE dont la `status` propriété est définie sur `DRAFT` ne participent pas à l’évaluation. Vous pouvez activer votre stratégie pour l’évaluation en envoyant une requête PATCH au point de `/policies/custom/` fin et en fournissant l’identifiant unique de la stratégie à la fin du chemin de demande.

**Format API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Valeur `id` de la stratégie que vous souhaitez activer. |

**Requête**

La requête suivante effectue une opération PATCH sur la `status` propriété de la stratégie DULE, en remplaçant sa valeur `DRAFT` par `ENABLED`.

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
| `op` | Type d’opération PATCH à effectuer. Cette requête effectue une opération de &quot;remplacement&quot;. |
| `path` | Chemin d’accès au champ à mettre à jour. Lors de l’activation d’une stratégie, la valeur doit être définie sur &quot;/status&quot;. |
| `value` | Nouvelle valeur à affecter à la propriété spécifiée dans `path`. Cette requête définit la `status` propriété de la stratégie sur &quot;ENABLED&quot;. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 (OK) et les détails de la stratégie mise à jour, avec sa `status` valeur désormais `ENABLED`.

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

En suivant ce didacticiel, vous avez créé une stratégie DULE pour une action marketing. Vous pouvez maintenant continuer à suivre le didacticiel sur l’ [application des stratégies](../enforcement/api-enforcement.md) DULE pour savoir comment rechercher les violations de stratégies et les gérer dans votre application d’expérience.

Pour plus d&#39;informations sur les différentes opérations disponibles dans l&#39;API de service de stratégie, consultez le guide [du développeur de](../api/getting-started.md)service de stratégie. Pour plus d’informations sur la manière d’appliquer des stratégies DULE pour les données de  de clients en temps réel, voir le didacticiel sur l’ [application de la conformité à l’utilisation des données pour  segments](../../segmentation/tutorials/governance.md)de .
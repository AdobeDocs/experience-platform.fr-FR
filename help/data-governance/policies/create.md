---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’une stratégie d’utilisation des données
topic: policies
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 3%

---


# Création d’une stratégie d’utilisation des données dans l’API

L&#39;étiquetage et l&#39;application de l&#39;utilisation des données (DULE) est le mécanisme de base de la gouvernance des données d&#39;Adobe Experience Platform. L&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service vous permet de créer et de gérer des stratégies DULE afin de déterminer les actions marketing à entreprendre par rapport aux données contenant certains libellés DULE.

Ce document fournit un didacticiel détaillé pour la création d’une stratégie DULE à l’aide de l’ [!DNL Policy Service] API. Pour un guide plus complet sur les différentes opérations disponibles dans l’API, consultez le guide [du développeur](../api/getting-started.md)Policy Service.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des concepts clés suivants liés à la création et à l&#39;évaluation des politiques DULE :

* [Gouvernance](../home.md)des données : Cadre selon lequel [!DNL Platform] applique la conformité à l’utilisation des données.
* [Étiquettes](../labels/overview.md)d&#39;utilisation des données : Les étiquettes d’utilisation des données sont appliquées aux champs de données XDM, en spécifiant les restrictions d’accès à ces données.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

Avant de commencer ce didacticiel, veuillez consulter le guide [du](../api/getting-started.md) développeur pour obtenir des informations importantes que vous devez connaître afin de réussir à appeler l&#39; [!DNL Policy Service] API DULE, y compris les en-têtes requis et comment lire des exemples d&#39;appels d&#39;API.

## Définir une action marketing {#define-action}

Dans le [!DNL Data Governance] cadre, une action marketing est une action entreprise par un [!DNL Experience Platform] utilisateur de données, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

La première étape de la création d&#39;une stratégie DULE consiste à déterminer l&#39;action marketing qu&#39;elle évaluera. Pour ce faire, utilisez l’une des options suivantes :

* [Rechercher une action marketing existante](#look-up)
* [Créer une action marketing](#create-new)

### Rechercher une action marketing existante {#look-up}

Vous pouvez rechercher les actions marketing existantes à évaluer par votre stratégie DULE en adressant une requête GET à l’un des `/marketingActions` points de terminaison.

**Format d’API**

Selon que vous recherchez une action marketing fournie par [!DNL Experience Platform] ou une action marketing personnalisée créée par votre organisation, utilisez les `marketingActions/core` points de terminaison ou les `marketingActions/custom` points de terminaison, respectivement.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Requête**

La requête suivante utilise le point de `marketingActions/custom` terminaison, qui récupère une liste de toutes les actions marketing définies par votre organisation IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie le nombre total d&#39;actions marketing trouvées (`count`) et liste les détails des actions marketing elles-mêmes dans la `children` baie.

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
| `_links.self.href` | Chaque élément de la `children` baie contient un ID URI pour l’action marketing répertoriée. |

Lorsque vous trouvez l’action marketing à utiliser, enregistrez la valeur de sa `href` propriété. Cette valeur est utilisée lors de l’étape suivante de la [création d’une stratégie](#create-policy)DULE.

### Créer une action marketing {#create-new}

Vous pouvez créer une action marketing en envoyant une requête PUT au point de `/marketingActions/custom/` terminaison et en fournissant un nom à l’action marketing à la fin du chemin de la requête.

**Format d’API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de la nouvelle action marketing que vous souhaitez créer. Ce nom agit comme l’identifiant principal de l’action marketing et doit donc être unique. Il est recommandé de donner à l’action marketing un nom descriptif mais concis. |

**Requête**

La requête suivante crée une nouvelle action marketing personnalisée appelée &quot;exportToThirdParty&quot;. Notez que la charge utile `name` de la demande est identique au nom fourni dans le chemin d’accès à la demande.

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
| `name` | Nom de l’action marketing à créer. Ce nom doit correspondre au nom fourni dans le chemin d’accès à la requête, sinon une erreur 400 (Mauvaise requête) se produira. |
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

Pour créer une nouvelle stratégie, vous devez fournir l’ID URI d’une action marketing avec une expression des étiquettes DULE qui interdisent cette action marketing.

Cette expression est appelée expression **de** stratégie et est un objet contenant soit (A) un libellé DULE, soit (B) un opérateur et des opérandes, mais pas les deux. En retour, chaque opérande est également un objet d’expression de stratégie. Par exemple, une politique relative à l’exportation de données vers un tiers peut être interdite si `C1 OR (C3 AND C7)` des étiquettes sont présentes. Cette expression serait spécifiée comme suit :

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

Une fois que vous avez configuré votre expression de stratégie, vous pouvez créer une nouvelle stratégie DULE en envoyant une demande POST au point de `/policies/custom` terminaison.

**Format d’API**

```http
POST /policies/custom
```

**Requête**

La requête suivante crée une stratégie DULE appelée &quot;Exporter des données vers des tiers&quot; en fournissant une action marketing et une expression de stratégie dans la charge utile de la requête.

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
| `marketingActionRefs` | Tableau contenant la `href` valeur d&#39;une action marketing, obtenue à l&#39;étape [](#define-action)précédente. Bien que l’exemple ci-dessus ne liste qu’une seule action marketing, plusieurs actions peuvent également être fournies. |
| `deny` | Objet expression de stratégie. Définit les étiquettes et conditions DULE qui provoqueraient le rejet par la stratégie de l&#39;action marketing référencée dans `marketingActionRefs`. |

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

## Activer la stratégie DULE

>[!NOTE] Bien que cette étape soit facultative si vous souhaitez laisser votre stratégie DULE en `DRAFT` état, veuillez noter que, par défaut, une stratégie doit avoir son statut défini sur `ENABLED` pour pouvoir participer à l&#39;évaluation. Consultez le didacticiel sur l’ [application des stratégies](../enforcement/api-enforcement.md) DULE pour en savoir plus sur la manière de faire des exceptions pour les stratégies `DRAFT` d’état.

Par défaut, les stratégies DULE dont la `status` propriété est définie pour `DRAFT` ne pas participer à l’évaluation. Vous pouvez activer votre stratégie pour évaluation en envoyant une requête PATCH au point de `/policies/custom/` terminaison et en fournissant l’identifiant unique de la stratégie à la fin du chemin de la demande.

**Format d’API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| `{POLICY_ID}` | Valeur `id` de la stratégie que vous souhaitez activer. |

**Requête**

La requête suivante effectue une opération PATCH sur la `status` propriété de la stratégie DULE, en modifiant sa valeur `DRAFT` en `ENABLED`.

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
| `op` | Type d&#39;opération PATCH à effectuer. Cette demande effectue une opération de remplacement. |
| `path` | Chemin d’accès au champ à mettre à jour. Lors de l’activation d’une stratégie, la valeur doit être définie sur &quot;/status&quot;. |
| `value` | Nouvelle valeur à affecter à la propriété spécifiée dans `path`. Cette requête définit la `status` propriété de la stratégie sur &quot;ACTIVÉ&quot;. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 (OK) et les détails de la stratégie mise à jour, avec `status` maintenant la valeur `ENABLED`de cette dernière.

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

En suivant ce didacticiel, vous avez créé avec succès une stratégie d’utilisation des données pour une action marketing. Vous pouvez maintenant continuer à suivre le didacticiel sur l’ [application des stratégies](../enforcement/api-enforcement.md) d’utilisation des données pour savoir comment vérifier les violations de stratégies et les gérer dans votre application d’expérience.

Pour plus d&#39;informations sur les différentes opérations disponibles dans l&#39; [!DNL Policy Service] API, consultez le guide [du développeur](../api/getting-started.md)Policy Service. Pour plus d’informations sur la manière d’appliquer des stratégies pour [!DNL Real-time Customer Profile] les données, voir le didacticiel sur l’ [application de la conformité à l’utilisation des données pour les segments](../../segmentation/tutorials/governance.md)d’audience.

Pour savoir comment gérer les stratégies d’utilisation dans l’interface [!DNL Experience Platform] utilisateur, consultez le guide [d’utilisation des](user-guide.md)stratégies.
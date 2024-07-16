---
title: Point de terminaison de l’API Attributs calculés
description: Découvrez comment créer, afficher, mettre à jour et supprimer des attributs calculés à l’aide de l’API Real-time Customer Profile.
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 94c94b8a3757aca1a04ff4ffc3c62e84602805cc
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 10%

---

# Point d’entrée de l’API des attributs calculés

>[!IMPORTANT]
>
>L’accès à l’API est restreint. Pour savoir comment accéder à l’API des attributs calculés, contactez l’assistance Adobe.

Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation. Ce guide comprend des exemples d’appels API pour effectuer des opérations CRUD de base à l’aide du point d’entrée `/attributes`.

Pour en savoir plus sur les attributs calculés, commencez par lire la [présentation des attributs calculés](overview.md).

## Commencer

Le point de terminaison d’API utilisé dans ce guide fait partie de l’ [ API Real-Time Customer Profile](https://www.adobe.com/go/profile-apis-en).

Avant de poursuivre, consultez le [guide de prise en main de l’API Profile](../api/getting-started.md) pour obtenir des liens vers la documentation recommandée, un guide de lecture des exemples d’appels API qui apparaissent dans ce document et des informations importantes sur les en-têtes requis pour réussir les appels à une API Experience Platform.

En outre, veuillez consulter la documentation du service suivant :

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   - [Guide de prise en main du registre des schémas](../../xdm/api/getting-started.md#know-your-tenant_id) : des informations sur votre `{TENANT_ID}`, qui apparaissent dans les réponses de ce guide, sont fournies.

## Récupération d’une liste d’attributs calculés {#list}

Vous pouvez récupérer une liste de tous les attributs calculés pour votre organisation en envoyant une requête de GET au point de terminaison `/attributes`.

**Format d’API**

Le point d’entrée `/attributes` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais de gestion élevés lors de l’inscription de ressources. Si vous effectuez un appel vers ce point de terminaison sans paramètres, tous les attributs calculés disponibles pour votre organisation seront récupérés. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

Les paramètres de requête suivants peuvent être utilisés lors de la récupération d’une liste d’attributs calculés :

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `limit` | Un paramètre qui spécifie le nombre maximal d’éléments renvoyés dans le cadre de la réponse. La valeur minimale de ce paramètre est 1 et la valeur maximale est 40. Si ce paramètre n’est pas inclus, 20 éléments sont renvoyés par défaut. | `limit=20` |
| `offset` | Un paramètre qui spécifie le nombre d’éléments à ignorer avant de renvoyer les éléments. | `offset=5` |
| `sortBy` | Un paramètre qui spécifie l’ordre dans lequel les éléments renvoyés sont triés. Les options disponibles sont `name`, `status`, `updateEpoch` et `createEpoch`. Vous pouvez également choisir de trier dans l’ordre croissant ou décroissant en n’incluant pas ou en incluant une `-` devant l’option de tri. Par défaut, les éléments seront triés par `updateEpoch` dans l’ordre décroissant. | `sortBy=name` |
| `property` | Paramètre permettant de filtrer les données selon différents champs d’attribut calculés. Les propriétés prises en charge sont `name`, `createEpoch`, `mergeFunction.value`, `updateEpoch` et `status`. Les opérations prises en charge dépendent de la propriété répertoriée. <ul><li>`name` : `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`createEpoch` : `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value` : `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`updateEpoch` : `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=)</li><li>`status` : `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**Requête**

La requête suivante récupère les trois derniers attributs calculés qui ont été mis à jour dans votre organisation.

+++ Exemple de requête pour récupérer une liste d’attributs calculés.

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste des 3 derniers attributs calculés mis à jour appartenant à votre organisation et votre environnement de test.

+++ Exemple de réponse pour récupérer une liste d’attributs calculés.

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `_links` | Objet contenant les informations de pagination nécessaires pour accéder à la dernière page de résultats, à la page de résultats suivante, à la page de résultats précédente ou à la page de résultats active. |
| `computedAttributes` | Tableau contenant les attributs calculés en fonction de vos paramètres de requête. Vous trouverez plus d’informations sur le tableau d’attributs calculés dans la section [ de récupération d’un attribut calculé spécifique ](#get). |
| `_page` | Objet contenant des métadonnées sur les résultats renvoyés. Cela inclut des informations sur le décalage actuel, le nombre d’attributs calculés renvoyés, le nombre total d’attributs calculés, ainsi que la limite des attributs calculés renvoyés. |

+++

## Création d’un attribut calculé {#create}

Pour créer un attribut calculé, commencez par effectuer une requête de POST sur le point de terminaison `/attributes` avec un corps de requête contenant les détails de l’attribut calculé que vous souhaitez créer.

**Format d’API**

```http
POST /attributes
```

**Requête**

+++ Exemple de requête pour créer un attribut calculé.

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom du champ attribut calculé, sous forme de chaîne. Le nom de l’attribut calculé ne peut être composé que de caractères alphanumériques sans espaces ni traits de soulignement. Cette valeur **must** doit être unique parmi tous les attributs calculés. En règle générale, ce nom doit être une version CamelCase de `displayName`. |
| `description` | Une description de l’attribut calculé. Cela s’avère particulièrement utile une fois que plusieurs attributs calculés ont été définis, car cela aidera d’autres membres de votre organisation à déterminer l’attribut calculé correct à utiliser. |
| `displayName` | Nom d’affichage de l’attribut calculé. Il s’agit du nom qui s’affichera lors de la liste de vos attributs calculés dans l’interface utilisateur de Adobe Experience Platform. |
| `expression` | Un objet qui représente l’expression de requête de l’attribut calculé que vous essayez de créer. |
| `expression.type` | Type de l’expression. Actuellement, seul PQL est pris en charge. |
| `expression.format` | Format de l’expression. Actuellement, seul `pql/text` est pris en charge. |
| `expression.value` | La valeur de l’expression. |
| `keepCurrent` | Valeur booléenne qui détermine si la valeur de l’attribut calculé est actualisée ou non à l’aide d’une actualisation rapide. Actuellement, cette valeur doit être définie sur `false`. |
| `duration` | Objet qui représente la période de recherche arrière de l’attribut calculé. La période de recherche en amont représente le délai dans lequel il est possible de revenir en arrière pour calculer l’attribut calculé. |
| `duration.count` | Un nombre qui représente la durée de la période de recherche en amont. Les valeurs possibles dépendent de la valeur du champ `duration.unit`. <ul><li>`HOURS` : 1-24</li><li>`DAYS` : 1-7</li><li>`WEEKS` : 1-4</li><li>`MONTHS` : 1-6</li></ul> |
| `duration.unit` | Chaîne représentant l’unité de temps qui sera utilisée pour la période de recherche arrière. Les valeurs possibles sont les suivantes : `HOURS`, `DAYS`, `WEEKS` et `MONTHS`. |
| `status` | État de l’attribut calculé. Les valeurs possibles sont `DRAFT` et `NEW`. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur votre attribut calculé que vous venez de créer.

+++ Exemple de réponse lors de la création d’un attribut calculé.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | L’identifiant généré par le système de votre attribut calculé nouvellement créé. |
| `status` | État de l’attribut calculé. Il peut s’agir de `DRAFT` ou de `NEW`. |
| `createEpoch` | Heure à laquelle l’attribut calculé a été créé, en secondes. |
| `updateEpoch` | Heure à laquelle l’attribut calculé a été mis à jour pour la dernière fois, en secondes. |
| `createdBy` | L’identifiant de l’utilisateur qui a créé l’attribut calculé. |

+++

## Récupération d’un attribut calculé spécifique {#get}

Vous pouvez récupérer des informations détaillées sur un attribut calculé spécifique en effectuant une requête de GET sur le point de terminaison `/attributes` et en fournissant l’identifiant de l’attribut calculé que vous souhaitez récupérer dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**Requête**

+++ Exemple de requête pour récupérer un attribut calculé spécifique.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur l’attribut calculé spécifié.

+++ Exemple de réponse lors de la récupération d’un attribut calculé spécifique.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Un identifiant unique, en lecture seule, généré par le système que vous pouvez utiliser pour faire référence à l’attribut calculé pendant les autres opérations API. |
| `type` | Chaîne indiquant que l’objet renvoyé est un attribut calculé. |
| `name` | Nom de l’attribut calculé. |
| `displayName` | Nom d’affichage de l’attribut calculé. Il s’agit du nom qui s’affichera lors de la liste de vos attributs calculés dans l’interface utilisateur de Adobe Experience Platform. |
| `description` | Une description de l’attribut calculé. Cela s’avère particulièrement utile une fois que plusieurs attributs calculés ont été définis, car cela aidera d’autres membres de votre organisation à déterminer l’attribut calculé correct à utiliser. |
| `imsOrgId` | L’identifiant de l’organisation à laquelle appartient l’attribut calculé. |
| `sandbox` | L’objet Sandbox contient des détails sur le sandbox sur lequel l’attribut calculé a été configuré. Ces informations sont tirées de l’en-tête du sandbox envoyé dans la requête. Pour plus d’informations, consultez la [présentation des sandbox](../../sandboxes/home.md). |
| `path` | `path` à l’attribut calculé. |
| `keepCurrent` | Valeur booléenne qui détermine si la valeur de l’attribut calculé est actualisée ou non à l’aide d’une actualisation rapide. |
| `expression` | Objet contenant l’expression de l’attribut calculé. |
| `mergeFunction` | Objet contenant la fonction de fusion pour l’attribut calculé. Cette valeur est basée sur le paramètre d’agrégation correspondant dans l’expression de l’attribut calculé. Les valeurs possibles sont `SUM`, `MIN`, `MAX` et `MOST_RECENT`. |
| `status` | État de l’attribut calculé. Il peut s’agir de l’une des valeurs suivantes : `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED` ou `DISABLED`. |
| `schema` | Objet contenant des informations sur le schéma dans lequel l’expression est évaluée. Actuellement, seul `_xdm.context.profile` est pris en charge. |
| `lastEvaluationTs` | Horodatage qui représente le moment où l’attribut calculé a été évalué pour la dernière fois. |
| `createEpoch` | Heure à laquelle l’attribut calculé a été créé, en secondes. |
| `updateEpoch` | Heure à laquelle l’attribut calculé a été mis à jour pour la dernière fois, en secondes. |
| `createdBy` | L’identifiant de l’utilisateur qui a créé l’attribut calculé. |

+++

## Suppression d’un attribut calculé spécifique {#delete}

Vous pouvez supprimer un attribut calculé spécifique en effectuant une requête de DELETE sur le point de terminaison `/attributes` et en fournissant l’identifiant de l’attribut calculé que vous souhaitez supprimer dans le chemin d’accès de la requête.

>[!IMPORTANT]
>
>La requête de suppression ne peut être utilisée que pour supprimer les attributs calculés ayant un état **draft** (`DRAFT`). Ce point d’entrée **ne peut pas** être utilisé pour supprimer des attributs calculés dans un autre état.

**Format d’API**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | La valeur `id` de l’attribut calculé que vous souhaitez supprimer. |

**Requête**

+++ Exemple de requête pour supprimer un attribut calculé.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 202 avec les détails de l’attribut calculé supprimé.

+++ Exemple de réponse lors de la suppression d’un attribut calculé.

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## Mise à jour d’un attribut calculé spécifique

Vous pouvez mettre à jour un attribut calculé spécifique en effectuant une requête de PATCH sur le point de terminaison `/attributes` et en fournissant l’identifiant de l’attribut calculé que vous souhaitez mettre à jour dans le chemin d’accès de la requête.

>[!IMPORTANT]
>
>Lors de la mise à jour d’un attribut calculé, seuls les champs suivants peuvent être mis à jour :
>
>- Si l’état actuel est `NEW`, l’état peut uniquement être modifié en `DISABLED`.
>- Si l’état actuel est `DRAFT`, vous pouvez modifier les valeurs des champs suivants : `name`, `description`, `keepCurrent`, `expression` et `duration`. Vous pouvez également modifier l’état de `DRAFT` à `NEW`. Toutes les modifications apportées aux champs générés par le système, tels que `mergeFunction` ou `path`, renverront une erreur.
>- Si l’état actuel est `PROCESSING` ou `PROCESSED`, l’état peut uniquement être modifié en `DISABLED`.

**Format d’API**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | La valeur `id` de l’attribut calculé que vous souhaitez mettre à jour. |

**Requête**

La requête suivante mettra à jour l’état de l’attribut calculé de `DRAFT` à `NEW`.

+++ Exemple de requête pour mettre à jour un attribut calculé.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur votre attribut calculé que vous venez de mettre à jour.

+++ Exemple de réponse lors de la mise à jour d’un attribut calculé.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## Étapes suivantes

Maintenant que vous avez appris les bases des attributs calculés, vous êtes prêt à commencer à les définir pour votre organisation. Pour savoir comment utiliser les attributs calculés dans l’interface utilisateur de l’Experience Platform, consultez le [guide de l’interface utilisateur des attributs calculés](./ui.md).

---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur d’API  client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: 21935bb36d8c2a0ef17e586c0909cf316ef026cf

---


# Stratégies de fusion

Adobe Experience Platform vous permet de rassembler des données à partir de plusieurs sources et de les combiner afin de voir un  complet de chacun de vos clients individuels. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée. A l’aide des API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Ce guide décrit les étapes à suivre pour utiliser les stratégies de fusion à l’aide de l’API. Pour utiliser des stratégies de fusion à l’aide de l’interface utilisateur, consultez le guide [d’utilisation des stratégies de](../ui/merge-policies.md)fusion.

## Prise en main

Les points de fin d’API utilisés dans ce guide font partie de l’API de  client en temps réel. Avant de poursuivre, consultez le guide [du développeur](getting-started.md)de l’API  client en tempsréel. En particulier, la section [de](getting-started.md#getting-started) prise en main du guide du développeur de  de comprend des liens vers des sujets connexes, un guide pour lire les exemples d’appels d’API dans ce  d’et des informations importantes sur les en-têtes requis nécessaires pour effectuer des appels vers les API de plateforme d’expérience.

## Composants des stratégies de fusion {#components-of-merge-policies}

Les stratégies de fusion sont privées à votre organisation IMS, ce qui vous permet de créer différentes stratégies afin de fusionner les  de la manière spécifique dont vous avez besoin. Toute API accédant aux données  du requiert une stratégie de fusion, bien qu’une stratégie par défaut soit utilisée si elle n’est pas explicitement fournie. La plateforme fournit une stratégie de fusion par défaut ou vous pouvez créer une stratégie de fusion pour un spécifique et la marquer comme valeur par défaut pour votre organisation. Chaque organisation peut avoir plusieurs stratégies de fusion par , mais chaque  de ne peut avoir qu’une seule stratégie de fusion par défaut. Tout jeu de stratégies de fusion par défaut sera utilisé lorsque le nom du  du est fourni et qu’une stratégie de fusion est requise mais pas fournie. Lorsque vous définissez une stratégie de fusion comme stratégie par défaut, toute stratégie de fusion précédemment définie comme stratégie par défaut ne sera plus utilisée comme stratégie par défaut.

### Terminer l’objet de stratégie de fusion

L’objet de stratégie de fusion complet représente un ensemble de préférences contrôlant les aspects de la fusion de fragments de  de.

**Fusionner l’objet de stratégie**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": {BOOLEAN},
        "updateEpoch": {UPDATE_TIME}
    }
```

| Propriété | Description |
|---|---|
| `id` | Le système a généré un identifiant unique attribué au moment de la création |
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans  . |
| `imsOrgId` | ID d’organisation auquel appartient cette stratégie de fusion |
| `identityGraph` | [Objet de graphique](#identity-graph) d’identité indiquant le graphique d’identité à partir duquel les identités associées seront obtenues. Les fragments  trouvés pour toutes les identités associées seront fusionnés. |
| `attributeMerge` | [Objet de fusion](#attribute-merge) d’attributs indiquant la manière dont la stratégie de fusion établit la priorité des valeurs d’attributs  dans le cas de conflits de données. |
| `schema` | Objet [](#schema) sur lequel la stratégie de fusion peut être utilisée. |
| `default` | Valeur booléenne indiquant si cette stratégie de fusion est la valeur par défaut du  spécifié. |
| `version` | Version de la stratégie de fusion gérée par la plateforme. Cette valeur en lecture seule est incrémentée chaque fois qu’une stratégie de fusion est mise à jour. |
| `updateEpoch` | Date de la dernière mise à jour de la stratégie de fusion. |

**Exemple de stratégie de fusion**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Graphique d’identité {#identity-graph}

[Le service](../../identity-service/home.md) d’identité Adobe Experience Platform gère les graphiques d’identité utilisés globalement et pour chaque organisation sur Experience Platform. L’ `identityGraph` attribut de la stratégie de fusion définit la manière de déterminer les identités associées pour un utilisateur.

**IdentityGraph, objet**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Où `{IDENTITY_GRAPH_TYPE}` se trouve l’un des éléments suivants :

* **&quot;none&quot; :** Ne pas assembler d&#39;identité.
* **&quot;pdg&quot; :** Effectuez des assemblages d’identité en fonction du graphique de votre identité privée.

**Exemple`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Fusion d’attributs {#attribute-merge}

Un fragment de  est l’information  de d’une seule identité parmi les  d’identités qui existent pour un utilisateur particulier. Lorsque le type de graphique d’identité utilisé génère plusieurs identités, il existe un risque de conflit de valeurs pour les propriétés  du et la priorité doit être spécifiée. Vous `attributeMerge`pouvez ainsi spécifier les valeurs  jeu de données à classer par priorité dans le d’un conflit de fusion.

**attributeMerge, objet**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Où `{ATTRIBUTE_MERGE_TYPE}` se trouve l’un des éléments suivants :

* **&quot;timestampOrdered&quot;**: (par défaut) Donner la priorité au mis à jour en dernier en cas de conflit. Avec ce type de fusion, l’ `data` attribut n’est pas obligatoire.
* **&quot;dataSetPrecedence&quot;** : Attribuez la priorité aux fragments  en fonction du jeu de données à partir duquel ils sont arrivés. Cela peut être utilisé lorsque les informations présentes dans un jeu de données sont préférées ou approuvées par rapport aux données d’un autre jeu de données. Lors de l’utilisation de ce type de fusion, l’ `order` attribut est obligatoire, car il les jeux de données dans l’ordre de priorité.
   * **&quot;order&quot;**: Lorsque &quot;dataSetPrecedence&quot; est utilisé, un `order` tableau doit être fourni avec un de jeux de données. Les jeux de données non inclus dans le  du ne seront pas fusionnés. En d’autres termes, les jeux de données doivent être explicitement répertoriés pour être fusionnés dans un . Le `order` tableau  les ID des jeux de données par ordre de priorité.

**Exemple d’objet attributeMerge utilisant le type dataSetPrecedence**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**Exemple d’objet attributeMerge utilisant le type timestampOrdered**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schéma {#schema}

L’objet  spécifie le XDM pour lequel cette stratégie de fusion est créée.

**`schema`objet **

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Où la valeur de `name` est le nom de la classe XDM sur laquelle repose le associé à la stratégie de fusion.

**Exemple`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## Accès aux stratégies de fusion {#access-merge-policies}

Grâce à l’API  client en temps réel, le `/config/mergePolicies` point de fin vous permet d’effectuer une demande de recherche afin de  une stratégie de fusion spécifique par son ID ou d’accéder à toutes les stratégies de fusion de votre organisation IMS, filtrées selon des critères spécifiques.

### Accès à une stratégie de fusion unique par ID

Vous pouvez accéder à une stratégie de fusion unique à l’aide de son ID en exécutant une requête GET sur le `/config/mergePolicies` point de fin et en incluant la règle `mergePolicyId` dans le chemin d’accès à la requête.

**Format API**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la stratégie de fusion à supprimer. |

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Réponse**

Une réponse réussie renvoie les détails de la stratégie de fusion.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

Consultez la section [Composants des stratégies](#components-of-merge-policies) de fusion au début de ce pour en savoir plus sur chacun des éléments qui constituent une stratégie de fusion.

###  de plusieurs stratégies de fusion par critère

Vous pouvez plusieurs stratégies de fusion au sein de votre organisation IMS en envoyant une requête GET au `/config/mergePolicies` point de terminaison et en utilisant des paramètres de  de facultatifs pour filtrer, classer et paginer la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (&amp;). Un appel à ce point de fin sans paramètre récupérera toutes les stratégies de fusion disponibles pour votre entreprise.

**Format API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Paramètre | Description |
|---|---|
| `default` | Valeur booléenne dont le résultat  selon que les stratégies de fusion sont ou non la valeur par défaut d’une classe  de. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. Valeur par défaut : 20 |
| `orderBy` | Indique le champ par lequel classer les résultats comme dans `orderBy=name` ou `orderBy=+name` trier par nom dans l’ordre croissant ou `orderBy=-name`, dans l’ordre décroissant. Si vous omettez cette valeur, le tri par défaut est effectué `name` dans l’ordre croissant. |
| `schema.name` | Nom du  pour lequel récupérer les stratégies de fusion disponibles. |
| `identityGraph.type` | Résultats  par type de graphique d’identité. Les valeurs possibles sont &quot;none&quot; et &quot;pdg&quot; (graphique privé). |
| `attributeMerge.type` | Résultats  par type de fusion d’attributs utilisé. Les valeurs possibles sont &quot;timestampOrdered&quot; et &quot;dataSetPrecedence&quot;. |
| `start` | Décalage de page : spécifiez l&#39;ID de début pour les données à récupérer. Valeur par défaut : 0 |
| `version` | Indiquez cette valeur si vous souhaitez utiliser une version spécifique de la stratégie de fusion. Par défaut, la dernière version sera utilisée. |

Pour plus d’informations sur `schema.name`, `identityGraph.type`et `attributeMerge.type`, consultez la section [Composants des stratégies](#components-of-merge-policies) de fusion fournie précédemment dans ce guide.


**Requête**

Le de requêtes suivant  toutes les stratégies de fusion pour un donné  :

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Réponse**

Une réponse réussie renvoie un paginé de stratégies de fusion qui répond aux critères spécifiés par les paramètres  du envoyés dans la requête.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| Propriété | Description |
|---|---|
| `_links.next.href` | Adresse URI de la page suivante des résultats. Utilisez cet URI comme paramètre de requête pour un autre appel d’API vers le même point de terminaison pour de la page. S’il n’existe pas de page suivante, cette valeur est une chaîne vide. |

## Création d’une stratégie de fusion

Vous pouvez créer une nouvelle stratégie de fusion pour votre organisation en envoyant une requête POST au point de `/config/mergePolicies` fin.

**Format API**

```http
POST /config/mergePolicies
```

**Requête** La requête suivante crée une nouvelle stratégie de fusion, configurée par les valeurs d’attribut fournies dans la charge utile :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| Propriété | Description |
|---|---|
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans  . |
| `identityGraph.type` | Type de graphique d’identité à partir duquel obtenir les identités connexes à fusionner. Valeurs possibles : &quot;none&quot; ou &quot;pdg&quot; (graphique privé). |
| `attributeMerge` | Méthode de hiérarchisation des valeurs d’attribut  en cas de conflit de données. |
| `schema` | Classe de  XDM associée à la stratégie de fusion. |
| `default` | Indique si cette stratégie de fusion est la stratégie par défaut pour le  du. |

Consultez la section [Composants des stratégies](#components-of-merge-policies) de fusion pour en savoir plus.

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle stratégie de fusion créée.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

Consultez la section [Composants des stratégies](#components-of-merge-policies) de fusion au début de ce pour en savoir plus sur chacun des éléments qui constituent une stratégie de fusion.

## Mettre à jour une stratégie de fusion {#update}

Vous pouvez modifier une stratégie de fusion existante en modifiant des attributs individuels (PATCH) ou en remplaçant la stratégie de fusion complète par de nouveaux attributs (PUT). Des exemples de chacun d’eux sont présentés ci-dessous.

### Modifier des champs de stratégie de fusion individuels

Vous pouvez modifier des champs individuels pour une stratégie de fusion en exécutant une requête PATCH au point de `/config/mergePolicies/{mergePolicyId}` fin :

**Format API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la stratégie de fusion à supprimer. |

**Requête**

La requête suivante met à jour une stratégie de fusion spécifiée en remplaçant la valeur de sa `default` propriété par `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| Propriété | Description |
|---|---|
| `op` | Indique l’opération à effectuer. Vous trouverez des exemples d’autres opérations PATCH dans la documentation du correctif [JSON.](http://jsonpatch.com) |
| `path` | Chemin du champ à mettre à jour. Les valeurs acceptées sont les suivantes : &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | Valeur sur laquelle le champ spécifié doit être défini. |

Consultez la section [Composants des stratégies](#components-of-merge-policies) de fusion pour en savoir plus.


**Réponse**

Une réponse réussie renvoie les détails de la nouvelle stratégie de fusion mise à jour.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### Remplacer une stratégie de fusion

Une autre méthode de modification d’une stratégie de fusion consiste à utiliser une requête PUT, qui remplace la stratégie de fusion complète.

**Format API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la stratégie de fusion à remplacer. |

**Requête**

La requête suivante remplace la stratégie de fusion spécifiée, en remplaçant ses valeurs d’attribut par celles fournies dans la charge utile. Puisque cette requête remplace complètement une stratégie de fusion existante, vous devez fournir tous les champs requis lors de la définition initiale de la stratégie de fusion. Toutefois, cette fois, vous fournissez des valeurs mises à jour pour les champs que vous souhaitez modifier.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Propriété | Description |
|---|---|
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans  . |
| `identityGraph` | Graphique d’identité à partir duquel obtenir les identités connexes à fusionner. |
| `attributeMerge` | Méthode de hiérarchisation des valeurs d’attribut  en cas de conflit de données. |
| `schema` | Classe de  XDM associée à la stratégie de fusion. |
| `default` | Indique si cette stratégie de fusion est la stratégie par défaut pour le  du. |

Consultez la section [Composants des stratégies](#components-of-merge-policies) de fusion pour en savoir plus.


**Réponse**

Une réponse réussie renvoie les détails de la stratégie de fusion mise à jour.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## Suppression d’une stratégie de fusion

Vous pouvez supprimer une stratégie de fusion en faisant une requête DELETE au point de `/config/mergePolicies` fin et en incluant l’ID de la stratégie de fusion que vous souhaitez supprimer dans le chemin d’accès de la requête.

**Format API**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la stratégie de fusion à supprimer. |

**Requête**

La requête suivante supprime une stratégie de fusion.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une requête de suppression réussie renvoie HTTP Status 200 (OK) et un corps de réponse vide. Pour confirmer que la suppression a réussi, vous pouvez exécuter une requête GET pour la stratégie de fusion à l’aide de son ID. Si la stratégie de fusion a été supprimée, vous recevrez une erreur HTTP Status 404 (Introuvable).

## Étapes suivantes

Maintenant que vous savez comment créer et configurer des stratégies de fusion pour votre organisation IMS, vous pouvez les utiliser pour créer   segments à partir de vos données de client en temps réel. Consultez la documentation [d’](../../segmentation/home.md) Adobe Experience Platform Segmentation Service pour commencer à définir et à utiliser des segments.




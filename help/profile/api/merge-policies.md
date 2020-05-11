---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur de l’API de Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: 33091568c850375b399435f375e854667493152c
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 3%

---


# Stratégies de fusion

Adobe Experience Platform vous permet de rassembler des données à partir de plusieurs sources et de les combiner afin d’obtenir une vue complète de chacun de vos clients. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée. A l’aide des API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Ce guide décrit les étapes à suivre pour utiliser les stratégies de fusion à l’aide de l’API. Pour utiliser des stratégies de fusion à l’aide de l’interface utilisateur, consultez le guide [d’utilisation des stratégies de](../ui/merge-policies.md)fusion.

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API Profil client en temps réel. Avant de continuer, consultez le guide [du développeur de l’API Profil client en temps](getting-started.md)réel. En particulier, la section [](getting-started.md#getting-started) Prise en main du guide du développeur de Profils contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API de plateforme d’expérience.

## Composants des stratégies de fusion {#components-of-merge-policies}

Les stratégies de fusion sont privées à votre organisation IMS, ce qui vous permet de créer différentes stratégies afin de fusionner les schémas de la manière spécifique dont vous avez besoin. Toute API accédant aux données du Profil requiert une stratégie de fusion, bien qu’une stratégie par défaut soit utilisée si elle n’est pas explicitement fournie. La plate-forme fournit une stratégie de fusion par défaut ou vous pouvez créer une stratégie de fusion pour un schéma spécifique et la marquer comme la stratégie par défaut de votre organisation. Chaque organisation peut avoir plusieurs stratégies de fusion par schéma, mais chaque schéma ne peut avoir qu&#39;une seule stratégie de fusion par défaut. Tout jeu de stratégies de fusion par défaut est utilisé lorsque le nom du schéma est fourni et qu’une stratégie de fusion est requise mais pas fournie. Lorsque vous définissez une stratégie de fusion comme stratégie par défaut, toute stratégie de fusion existante précédemment définie comme stratégie par défaut sera automatiquement mise à jour afin de ne plus être utilisée comme stratégie par défaut.

### Objet de stratégie de fusion complète

L’objet de stratégie de fusion complet représente un ensemble de préférences contrôlant les aspects des fragments de profil fusionnés.

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
| `id` | Le système a généré un identifiant unique attribué au moment de la création. |
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans les vues de liste. |
| `imsOrgId` | ID d&#39;organisation auquel appartient cette stratégie de fusion |
| `identityGraph` | [Objet de graphique](#identity-graph) d&#39;identité indiquant le graphique d&#39;identité à partir duquel les identités liées seront obtenues. Les fragments de Profil trouvés pour toutes les identités associées seront fusionnés. |
| `attributeMerge` | [Objet de fusion](#attribute-merge) d’attributs indiquant la manière dont la stratégie de fusion attribuera la priorité aux valeurs d’attribut de profil en cas de conflit de données. |
| `schema` | Objet [schéma](#schema) sur lequel la stratégie de fusion peut être utilisée. |
| `default` | Valeur booléenne indiquant si cette stratégie de fusion est la stratégie par défaut du schéma spécifié. |
| `version` | Version conservée de la plateforme de la stratégie de fusion. Cette valeur en lecture seule est incrémentée chaque fois qu’une stratégie de fusion est mise à jour. |
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

### Graphique d&#39;identité {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) gère les graphiques d’identité utilisés globalement et pour chaque organisation sur Experience Platform. L’ `identityGraph` attribut de la stratégie de fusion définit comment déterminer les identités associées pour un utilisateur.

**identityGraph, objet**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Où `{IDENTITY_GRAPH_TYPE}` se trouve l’une des situations suivantes :

* **&quot;none&quot; :** N&#39;effectuez aucune assemblage d&#39;identité.
* **&quot;pdg&quot; :** Effectuez des assemblages d’identité en fonction de votre graphique d’identité privé.

**Exemple`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Fusion d’attributs {#attribute-merge}

Un fragment de profil est l’information de profil d’une seule identité sur la liste des identités qui existent pour un utilisateur particulier. Lorsque le type de graphique d&#39;identité utilisé génère plusieurs identités, il existe un risque de conflit de valeurs pour les propriétés du profil et la priorité doit être spécifiée. Grâce à `attributeMerge`cette option, vous pouvez spécifier les valeurs de profil de jeux de données à classer par priorité dans le événement d’un conflit de fusion.

**attributeMerge, objet**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Où `{ATTRIBUTE_MERGE_TYPE}` se trouve l’une des situations suivantes :

* **&quot;timestampOrdered&quot;**: (par défaut) Donner la priorité au profil mis à jour en dernier cas de conflit. Avec ce type de fusion, l’ `data` attribut n’est pas obligatoire.
* **&quot;dataSetPrecedence&quot;** : Donner la priorité aux fragments de profil en fonction du jeu de données à partir duquel ils sont arrivés. Cela peut être utilisé lorsque les informations présentes dans un jeu de données sont préférées ou approuvées par rapport aux données d&#39;un autre jeu de données. Lors de l’utilisation de ce type de fusion, l’ `order` attribut est obligatoire, car il liste les jeux de données dans l’ordre de priorité.
   * **&quot;order&quot;**: Lorsque &quot;dataSetPrecedence&quot; est utilisé, un `order` tableau doit être fourni avec une liste de jeux de données. Les jeux de données non inclus dans la liste ne seront pas fusionnés. En d&#39;autres termes, les jeux de données doivent être explicitement répertoriés pour être fusionnés dans un profil. Le `order` tableau liste les ID des jeux de données par ordre de priorité.

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

L’objet schéma spécifie le schéma XDM pour lequel cette stratégie de fusion est créée.

**`schema`objet **

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Où la valeur de `name` est le nom de la classe XDM sur laquelle repose le schéma associé à la stratégie de fusion.

**Exemple`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## Stratégies de fusion d’accès {#access-merge-policies}

Grâce à l’API Profil client en temps réel, le `/config/mergePolicies` point de terminaison vous permet d’effectuer une demande de recherche pour vue d’une stratégie de fusion spécifique à l’aide de son identifiant ou d’accéder à toutes les stratégies de fusion de votre organisation IMS, filtrées selon des critères spécifiques. Vous pouvez également utiliser le `/config/mergePolicies/bulk-get` point de terminaison pour récupérer plusieurs stratégies de fusion à l’aide de leur ID. Les étapes d&#39;exécution de chacun de ces appels sont décrites dans les sections suivantes.

### Accès à une stratégie de fusion unique par ID

Vous pouvez accéder à une stratégie de fusion unique à l’aide de son identifiant en exécutant une requête GET sur le point de `/config/mergePolicies` terminaison et en incluant la stratégie `mergePolicyId` dans le chemin d’accès à la requête.

**Format d’API**

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

Consultez la section [composants des stratégies](#components-of-merge-policies) de fusion au début de ce document pour en savoir plus sur chacun des éléments qui constituent une stratégie de fusion.

### Récupérer plusieurs stratégies de fusion à l’aide de leur ID

Vous pouvez récupérer plusieurs stratégies de fusion en envoyant une requête POST au point de `/config/mergePolicies/bulk-get` terminaison et en incluant les ID des stratégies de fusion que vous souhaitez récupérer dans le corps de la requête.

**Format d’API**

```http
POST /config/mergePolicies/bulk-get
```

**Requête**

Le corps de la requête comprend un tableau &quot;id&quot; avec des objets individuels contenant l&#39;&quot;id&quot; pour chaque stratégie de fusion pour laquelle vous souhaitez récupérer des détails.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          }
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie HTTP Status 207 (Multi-Status) et les détails des stratégies de fusion dont les ID ont été fournis dans la demande POST.

```json
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
```

Consultez la section [composants des stratégies](#components-of-merge-policies) de fusion au début de ce document pour en savoir plus sur chacun des éléments qui constituent une stratégie de fusion.

### Liste de plusieurs stratégies de fusion par critère

Vous pouvez liste plusieurs stratégies de fusion au sein de votre organisation IMS en émettant une requête GET au point de `/config/mergePolicies` terminaison et en utilisant des paramètres de requête facultatifs pour filtrer, classer et paginer la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (&amp;). Un appel à ce point de terminaison sans paramètre récupérera toutes les stratégies de fusion disponibles pour votre entreprise.

**Format d’API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Paramètre | Description |
|---|---|
| `default` | Valeur booléenne qui filtres les résultats selon que les stratégies de fusion sont ou non la valeur par défaut d&#39;une classe de schéma. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. Valeur par défaut : 20 |
| `orderBy` | Indique le champ par lequel classer les résultats comme dans `orderBy=name` ou `orderBy=+name` trier par nom dans l’ordre croissant ou `orderBy=-name`dans l’ordre décroissant. Si cette valeur est omise, le tri par défaut est effectué dans `name` l’ordre croissant. |
| `schema.name` | Nom du schéma pour lequel récupérer les stratégies de fusion disponibles. |
| `identityGraph.type` | Filtres les résultats par type de graphique d&#39;identité. Les valeurs possibles sont &quot;none&quot; et &quot;pdg&quot; (graphique privé). |
| `attributeMerge.type` | Filtres les résultats selon le type de fusion d&#39;attribut utilisé. Les valeurs possibles sont &quot;timestampOrdered&quot; et &quot;dataSetPrecedence&quot;. |
| `start` | Décalage de page : spécifiez l&#39;ID de début pour les données à récupérer. Valeur par défaut : 0 |
| `version` | Indiquez cette valeur si vous souhaitez utiliser une version spécifique de la stratégie de fusion. Par défaut, la dernière version sera utilisée. |

Pour plus d&#39;informations sur `schema.name`, `identityGraph.type`et `attributeMerge.type`, consultez la section [composants des stratégies](#components-of-merge-policies) de fusion fournie plus haut dans ce guide.


**Requête**

Les listes de requête suivantes fusionnent toutes les stratégies pour un schéma donné :

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Réponse**

Une réponse réussie renvoie une liste paginée de stratégies de fusion qui répond aux critères spécifiés par les paramètres de requête envoyés dans la demande.

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
| `_links.next.href` | Adresse URI de la page de résultats suivante. Utilisez cet URI comme paramètre de requête pour un autre appel d’API vers le même point de terminaison pour vue de la page. S’il n’existe pas de page suivante, cette valeur sera une chaîne vide. |

## Création d’une stratégie de fusion

Vous pouvez créer une nouvelle stratégie de fusion pour votre organisation en envoyant une requête POST au point de `/config/mergePolicies` terminaison.

**Format d’API**

```http
POST /config/mergePolicies
```

**Requête** La requête suivante crée une nouvelle stratégie de fusion, qui est configurée par les valeurs d’attribut fournies dans la charge utile :

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
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans les vues de liste. |
| `identityGraph.type` | Type de graphique d&#39;identité à partir duquel obtenir les identités associées à fusionner. Valeurs possibles : &quot;none&quot; ou &quot;pdg&quot; (graphique privé). |
| `attributeMerge` | Méthode de hiérarchisation des valeurs d’attribut de profil en cas de conflit de données. |
| `schema` | Classe de schéma XDM associée à la stratégie de fusion. |
| `default` | Indique si cette stratégie de fusion est la stratégie par défaut pour le schéma. |

Consultez la section [composants des stratégies](#components-of-merge-policies) de fusion pour plus d’informations.

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

Consultez la section [composants des stratégies](#components-of-merge-policies) de fusion au début de ce document pour en savoir plus sur chacun des éléments qui constituent une stratégie de fusion.

## Mettre à jour une stratégie de fusion {#update}

Vous pouvez modifier une stratégie de fusion existante en modifiant des attributs individuels (PATCH) ou en remplaçant la stratégie de fusion complète par de nouveaux attributs (PUT). Les exemples de chacun sont présentés ci-dessous.

### Modifier des champs de stratégie de fusion individuels

Vous pouvez modifier des champs individuels pour une stratégie de fusion en adressant une requête PATCH au point de `/config/mergePolicies/{mergePolicyId}` terminaison :

**Format d’API**

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
| `op` | Indique l’opération à effectuer. Des exemples d’autres opérations PATCH se trouvent dans la documentation du correctif [JSON.](http://jsonpatch.com) |
| `path` | Chemin d’accès du champ à mettre à jour. Les valeurs acceptées sont les suivantes : &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | Valeur à laquelle le champ spécifié doit être défini. |

Consultez la section [composants des stratégies](#components-of-merge-policies) de fusion pour plus d’informations.


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

Une autre manière de modifier une stratégie de fusion consiste à utiliser une requête PUT, qui remplace la stratégie de fusion complète.

**Format d’API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la stratégie de fusion à remplacer. |

**Requête**

La requête suivante remplace la stratégie de fusion spécifiée, en remplaçant ses valeurs d’attribut par celles fournies dans la charge utile. Puisque cette requête remplace complètement une stratégie de fusion existante, vous devez fournir tous les champs requis lors de la définition initiale de la stratégie de fusion. Cependant, cette fois, vous fournissez des valeurs mises à jour pour les champs que vous souhaitez modifier.

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
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans les vues de liste. |
| `identityGraph` | Graphique d&#39;identité à partir duquel obtenir les identités associées à fusionner. |
| `attributeMerge` | Méthode de hiérarchisation des valeurs d’attribut de profil en cas de conflit de données. |
| `schema` | Classe de schéma XDM associée à la stratégie de fusion. |
| `default` | Indique si cette stratégie de fusion est la stratégie par défaut pour le schéma. |

Consultez la section [composants des stratégies](#components-of-merge-policies) de fusion pour plus d’informations.


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

## Supprimer une stratégie de fusion

Une stratégie de fusion peut être supprimée en faisant une requête DELETE au point de `/config/mergePolicies` terminaison et en incluant l&#39;ID de la stratégie de fusion que vous souhaitez supprimer dans le chemin de requête.

**Format d’API**

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

Une requête de suppression réussie renvoie HTTP Status 200 (OK) et un corps de réponse vide. Pour confirmer que la suppression a réussi, vous pouvez exécuter une requête GET pour vue à la stratégie de fusion à l’aide de son identifiant. Si la stratégie de fusion a été supprimée, vous recevrez une erreur HTTP Status 404 (Not Trouvé).

## Étapes suivantes

Maintenant que vous savez comment créer et configurer des stratégies de fusion pour votre organisation IMS, vous pouvez les utiliser pour créer des segments d’audience à partir de vos données de Profil client en temps réel. Consultez la documentation [d’](../../segmentation/home.md) Adobe Experience Platform Segmentation Service pour commencer à définir et à utiliser des segments.




---
keywords: Experience Platform ; profil ; profil client en temps réel ; dépannage ; API
title: Point de terminaison de l’API de fusion de stratégies
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform vous permet de rassembler des fragments de données provenant de plusieurs sources et de les combiner afin d’obtenir une vue complète de chacun de vos clients. Lorsque ces données sont regroupées, les stratégies de fusion sont les règles utilisées par Plateforme pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer une vue unifiée.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2560'
ht-degree: 54%

---

# Point de terminaison de la fusion de stratégies

Adobe Experience Platform vous permet de rassembler des fragments de données provenant de plusieurs sources et de les combiner afin d’obtenir une vue complète de chacun de vos clients. Lorsque ces données sont regroupées, les stratégies de fusion sont les règles que [!DNL Platform] utilise pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer une vue unifiée.

Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre entreprise aura plusieurs fragments de profil liés à ce client unique qui apparaîtront dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans la plate-forme, ils sont fusionnés ensemble afin de créer un profil unique pour ce client. Lorsque les données provenant de plusieurs sources entrent en conflit (par exemple, un fragment liste le client comme &quot;unique&quot; tandis que les autres listes le client comme &quot;marié&quot;), la stratégie de fusion détermine les informations à inclure dans le profil de la personne.

À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Ce guide décrit les étapes à suivre pour utiliser les stratégies de fusion à l’aide de l’API.

Pour utiliser des stratégies de fusion à l’aide de l’interface utilisateur, consultez le [guide d’interface utilisateur des stratégies de fusion](../ui/merge-policies.md).

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie du [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API [!DNL Experience Platform].

## Composants des stratégies de fusion {#components-of-merge-policies}

Les stratégies de fusion sont privées à votre organisation IMS, ce qui vous permet de créer différentes stratégies pour fusionner des schémas de la manière dont vous avez besoin. Toute API accédant aux données [!DNL Profile] nécessite une stratégie de fusion, bien qu&#39;une stratégie par défaut soit utilisée si elle n&#39;est pas explicitement fournie. [!DNL Platform] fournit aux entreprises une stratégie de fusion par défaut ou vous pouvez créer une stratégie de fusion pour une classe de schéma de modèle de données d’expérience (XDM) spécifique et la marquer comme valeur par défaut pour votre entreprise.

Bien que chaque organisation puisse avoir plusieurs stratégies de fusion par classe de schéma, chaque classe ne peut avoir qu&#39;une seule stratégie de fusion par défaut. Tout jeu de stratégies de fusion par défaut est utilisé lorsque le nom de la classe de schéma est fourni et qu’une stratégie de fusion est requise mais pas fournie.

>[!NOTE]
>
>Lorsque vous définissez une nouvelle stratégie de fusion comme stratégie par défaut, toute stratégie de fusion existante précédemment définie comme stratégie par défaut ne sera plus utilisée comme stratégie par défaut.

### Objet de stratégie de fusion complet

L’objet de stratégie de fusion complet est un ensemble de préférences contrôlant les aspects de la fusion de fragments de profil.

**Objet de stratégie de fusion**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Propriété | Description |
|---|---|
| `id` | Le système a généré un identifiant unique attribué au moment de la création. |
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans les affichages en liste. |
| `imsOrgId` | Identifiant d’organisation auquel appartient cette stratégie de fusion. |
| `identityGraph` | Objet de [graphique d’identités](#identity-graph) indiquant le graphique d’identités à partir duquel les identités associées seront obtenues. Les fragments de profil trouvés pour toutes les identités associées seront fusionnés. |
| `attributeMerge` | [Attribut ](#attribute-merge) mergeobject indiquant la manière dont la stratégie de fusion attribuera la priorité aux attributs de profil en cas de conflit de données. |
| `schema.name` | Dans l&#39;objet [`schema`](#schema), le champ `name` contient la classe de schéma XDM à laquelle se rapporte la stratégie de fusion. Pour plus d&#39;informations sur les schémas et les classes, consultez la [documentation XDM](../../xdm/home.md). |
| `default` | Valeur booléenne indiquant si cette stratégie de fusion est la valeur par défaut du schéma spécifié. |
| `version` | [!DNL Platform]Version de la stratégie de fusion gérée par Cette valeur en lecture seule est incrémentée chaque fois qu’une stratégie de fusion est mise à jour. |
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

### Graphique d’identités {#identity-graph}

[Adobe Experience Platform Identity ](../../identity-service/home.md) Service gère les graphiques d&#39;identité utilisés dans le monde entier et pour chaque organisation  [!DNL Experience Platform]. L’attribut `identityGraph` de la stratégie de fusion définit la manière de déterminer les identités associées pour un utilisateur.

**Objet identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Où `{IDENTITY_GRAPH_TYPE}` peut prendre une de ces valeurs :

* **&quot;none&quot; :** ne réalise aucune combinaison d’identités.
* **&quot;pdg&quot; :** effectue des combinaisons d’identités en se basant sur votre graphique d’identités privé.

**Exemple`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Fusion d’attributs {#attribute-merge}

Un fragment de profil correspond aux informations de profil d’une seule identité de la liste d’identités qui existe pour un utilisateur particulier. Lorsque le type de graphique d&#39;identité utilisé génère plusieurs identités, il existe un risque de conflit d&#39;attributs de profil et la priorité doit être spécifiée. `attributeMerge` permet de spécifier les attributs de profil à prioriser dans le événement d&#39;un conflit de fusion entre des jeux de données de type Valeur clé (données d&#39;enregistrement) et Données d&#39;enregistrement.

**Objet attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Où `{ATTRIBUTE_MERGE_TYPE}` peut prendre une de ces valeurs :

* **`timestampOrdered`**: (par défaut) Attribuez la priorité au profil qui a été mis à jour en dernier. Avec ce type de fusion, l’attribut `data` n’est pas obligatoire. `timestampOrdered` prend également en charge les horodatages personnalisés qui sont prioritaires lors de la fusion de fragments de profil dans ou entre des jeux de données. Pour en savoir plus, voir la section Annexe sur [l&#39;utilisation d&#39;horodatages personnalisés](#custom-timestamps).
* **`dataSetPrecedence`** : Donner la priorité aux fragments de profil en fonction du jeu de données à partir duquel ils sont arrivés. Cela peut être utilisé lorsque les informations présentes dans un jeu de données sont préférées ou approuvées par rapport aux données d’un autre jeu de données. Lors de l’utilisation de ce type de fusion, l’attribut `order` est obligatoire, car il répertorie les jeux de données dans l’ordre de priorité.
   * **`order`**: Lorsque &quot;dataSetPrecedence&quot; est utilisé, un  `order` tableau doit être fourni avec une liste de jeux de données. Les jeux de données qui ne font pas partie de la liste ne sont pas fusionnés. En d’autres termes, les jeux de données doivent être explicitement répertoriés pour être fusionnés dans un profil. Le tableau `order` répertorie les identifiants des jeux de données par ordre de priorité.

#### Exemple d&#39;objet `attributeMerge` utilisant le type `dataSetPrecedence`

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

#### Exemple d&#39;objet `attributeMerge` utilisant le type `timestampOrdered`

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schéma {#schema}

L’objet schéma spécifie la classe de schéma Modèle de données d’expérience (XDM) pour laquelle cette stratégie de fusion est créée.

**`schema`Objet**

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

Pour en savoir plus sur XDM et travailler avec des schémas en Experience Platform, lisez tout d&#39;abord [Présentation du système XDM](../../xdm/home.md).

## Accès aux stratégies de fusion {#access-merge-policies}

En utilisant l&#39;API [!DNL Real-time Customer Profile], le point de terminaison `/config/mergePolicies` vous permet d&#39;effectuer une demande de recherche pour vue d&#39;une stratégie de fusion spécifique par son identifiant, ou d&#39;accéder à toutes les stratégies de fusion de votre organisation IMS, filtrées selon des critères spécifiques. Vous pouvez également utiliser le point de terminaison `/config/mergePolicies/bulk-get` pour récupérer plusieurs stratégies de fusion en fonction de leurs ID. Les étapes d&#39;exécution de chacun de ces appels sont décrites dans les sections suivantes.

### Accès à une stratégie de fusion unique par identifiant

Vous pouvez accéder à une stratégie de fusion unique à l’aide de son identifiant en exécutant une requête GET sur le point de terminaison `/config/mergePolicies` et en incluant le paramètre `mergePolicyId` dans le chemin d’accès de la requête.

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

Pour en savoir plus sur chacun des éléments qui constituent une stratégie de fusion, reportez-vous à la section [Composants des stratégies de fusion](#components-of-merge-policies) au début de ce document.

### Récupérer plusieurs stratégies de fusion à l’aide de leur ID

Vous pouvez récupérer plusieurs stratégies de fusion en adressant une requête de POST au point de terminaison `/config/mergePolicies/bulk-get` et en incluant les ID des stratégies de fusion que vous souhaitez récupérer dans le corps de la requête.

**Format d’API**

```http
POST /config/mergePolicies/bulk-get
```

**Requête**

Le corps de la requête comprend un tableau &quot;id&quot; avec des objets individuels contenant &quot;id&quot; pour chaque stratégie de fusion pour laquelle vous souhaitez récupérer des détails.

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
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie HTTP Status 207 (Multi-Status) et les détails des stratégies de fusion dont les ID ont été fournis dans la demande de POST.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
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
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
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
    }
}
```

Pour en savoir plus sur chacun des éléments qui constituent une stratégie de fusion, reportez-vous à la section [Composants des stratégies de fusion](#components-of-merge-policies) au début de ce document.

### Répertorier plusieurs stratégies de fusion par critère

Vous pouvez répertorier plusieurs stratégies de fusion au sein de votre organisation IMS en envoyant une requête GET au point de terminaison `/config/mergePolicies` et en utilisant des paramètres de requête facultatifs pour filtrer, classer et paginer la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (&amp;). Un appel à ce point de terminaison sans paramètre permet de récupérer toutes les stratégies de fusion disponibles pour votre organisation.

**Format d’API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Paramètre | Description |
|---|---|
| `default` | Valeur booléenne filtrant les résultats selon que les stratégies de fusion sont ou non la valeur par défaut d’une classe de schémas. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. Valeur par défaut : 20 |
| `orderBy` | Spécifie le champ de référence pour classer les résultats comme dans `orderBy=name` ou `orderBy=+name` pour un tri par nom dans l’ordre croissant ou `orderBy=-name` pour un tri dans l’ordre décroissant. Si vous omettez cette valeur, le tri par défaut de `name` s’effectue dans l’ordre croissant. |
| `schema.name` | Nom du schéma pour lequel récupérer les stratégies de fusion disponibles. |
| `identityGraph.type` | Filtre les résultats par type de graphique d’identités. Les valeurs possibles sont &quot;none&quot; et &quot;pdg&quot; (graphique privé). |
| `attributeMerge.type` | Filtre les résultats par type de fusion d’attributs utilisé. Les valeurs possibles sont &quot;timestampOrdered&quot; et &quot;dataSetPrecedence&quot;. |
| `start` | Décalage de page : spécifiez l’identifiant de début pour les données à récupérer. Valeur par défaut : 0 |
| `version` | Indiquez cette valeur si vous souhaitez utiliser une version spécifique de la stratégie de fusion. Par défaut, la dernière version sera utilisée. |

Pour plus d’informations sur `schema.name`, `identityGraph.type` et `attributeMerge.type`, référez-vous à la section [Composants des stratégies de fusion](#components-of-merge-policies) au début de ce document.


**Requête**

La requête suivante répertorie toutes les stratégies de fusion pour un schéma donné :

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Réponse**

Une réponse réussie renvoie une liste paginée de stratégies de fusion qui répond aux critères spécifiés par les paramètres envoyés dans la requête.

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
| `_links.next.href` | Adresse URI de la page de résultats suivante. Utilisez cet URI comme paramètre de requête pour un autre appel API vers le même point de terminaison pour afficher la page. S’il n’y a pas de page suivante, cette valeur est une chaîne vide. |

## Création d’une stratégie de fusion

Vous pouvez créer une stratégie de fusion pour votre organisation en exécutant une requête POST sur le point de terminaison `/config/mergePolicies`.

**Format d’API**

```http
POST /config/mergePolicies
```

**Requête**
La requête suivante crée une nouvelle stratégie de fusion, configurée par les valeurs d’attribut fournies dans le payload :

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
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans les affichages en liste. |
| `identityGraph.type` | Type de graphique d’identités à partir duquel obtenir les identités connexes à fusionner. Valeurs possibles : &quot;none&quot; ou &quot;pdg&quot; (graphique privé). |
| `attributeMerge` | Méthode de hiérarchisation des valeurs d’attribut de profil en cas de conflit de données. |
| `schema` | Classe de schéma XDM associée à la stratégie de fusion. |
| `default` | Spécifie si cette stratégie de fusion est la stratégie par défaut pour le schéma. |

Pour plus d’informations, reportez-vous à la section [Composants des stratégies de fusion](#components-of-merge-policies).

**Réponse**

Une réponse réussie renvoie les détails de la stratégie de fusion créée.

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

Pour en savoir plus sur chacun des éléments qui constituent une stratégie de fusion, reportez-vous à la section [Composants des stratégies de fusion](#components-of-merge-policies) au début de ce document.

## Mise à jour d’une stratégie de fusion {#update}

Vous pouvez modifier une stratégie de fusion existante en changeant les attributs individuels (PATCH) ou en remplaçant la stratégie de fusion complète par de nouveaux attributs (PUT). Vous en trouverez des exemples ci-dessous.

### Modification des champs de stratégie de fusion individuels

Vous pouvez modifier des champs individuels pour une stratégie de fusion en exécutant une requête PATCH au point de terminaison `/config/mergePolicies/{mergePolicyId}` :

**Format d’API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la stratégie de fusion à supprimer. |

**Requête**

La requête suivante met à jour une stratégie de fusion spécifiée en définissant la valeur de sa propriété `default` sur `true` :

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
| `op` | Spécifie l’opération à effectuer. Vous trouverez des exemples d’autres opérations PATCH dans la documentation [JSON Patch](http://jsonpatch.com). |
| `path` | Chemin du champ à mettre à jour. Les valeurs acceptées sont les suivantes : &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;. |
| `value` | Valeur sur laquelle le champ spécifié doit être défini. |

Pour plus d’informations, reportez-vous à la section [Composants des stratégies de fusion](#components-of-merge-policies).


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

### Remplacement d’une stratégie de fusion

Une façon de modifier une stratégie de fusion consiste à utiliser une requête PUT, qui remplace entièrement la stratégie de fusion.

**Format d’API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la stratégie de fusion à remplacer. |

**Requête**

La requête suivante remplace la stratégie de fusion spécifiée, en changeant ses valeurs d’attribut par celles fournies dans le payload. Puisque cette requête remplace complètement une stratégie de fusion existante, vous devez fournir tous les champs requis lors de la définition initiale de la stratégie de fusion. Toutefois, cette fois, vous fournissez des valeurs mises à jour pour les champs que vous souhaitez modifier.

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
| `name` | Nom convivial par lequel la stratégie de fusion peut être identifiée dans les affichages en liste. |
| `identityGraph` | Graphique d’identités à partir duquel obtenir les identités connexes à fusionner. |
| `attributeMerge` | Méthode de hiérarchisation des valeurs d’attribut de profil en cas de conflit de données. |
| `schema` | Classe de schéma XDM associée à la stratégie de fusion. |
| `default` | Spécifie si cette stratégie de fusion est la stratégie par défaut pour le schéma. |

Pour plus d’informations, reportez-vous à la section [Composants des stratégies de fusion](#components-of-merge-policies).


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

Vous pouvez supprimer une stratégie de fusion en exécutant une requête DELETE au point de terminaison `/config/mergePolicies` et en incluant l’identifiant de la stratégie de fusion que vous souhaitez supprimer dans le chemin d’accès de la requête.

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

Une requête de suppression réussie renvoie un état HTTP 200 (OK) et un corps de réponse vide. Pour confirmer que la suppression a réussi, vous pouvez exécuter une requête GET pour afficher la stratégie de fusion à l’aide de son identifiant. Si la stratégie de fusion a été supprimée, vous recevrez un état HTTP 404 (Introuvable).

## Étapes suivantes

Maintenant que vous savez comment créer et configurer des stratégies de fusion pour votre entreprise, vous pouvez les utiliser pour ajuster la vue des profils client dans la plateforme et pour créer des segments d&#39;audience à partir de vos données [!DNL Real-time Customer Profile]. Consultez l’[aide d’Adobe Experience Platform Segmentation Service](../../segmentation/home.md) pour commencer à définir et à utiliser des segments.

## Annexe

Cette section fournit des informations supplémentaires sur l’utilisation des stratégies de fusion.

### Utilisation d’horodatages personnalisés {#custom-timestamps}

Comme les enregistrements sont ingérés dans l&#39;Experience Platform, un horodatage système est obtenu au moment de l&#39;assimilation et ajouté à l&#39;enregistrement. Lorsque `timestampOrdered` est sélectionné comme type `attributeMerge` pour une stratégie de fusion, les profils sont fusionnés en fonction de l&#39;horodatage système. En d’autres termes, la fusion est effectuée en fonction de l’horodatage du moment où l’enregistrement a été ingéré dans la plate-forme.

Il peut arriver, par exemple, que des données soient renvoyées ou que l’ordre des événements soit correct si les enregistrements sont ingérés dans l’ordre, lorsqu’il est nécessaire de fournir un horodatage personnalisé et que la stratégie de fusion respecte l’horodatage personnalisé plutôt que l’horodatage système.

Pour utiliser un horodatage personnalisé, [[!DNL External Source System Audit Details Mixin]](#mixin-details) doit être ajouté à votre schéma de Profil. Une fois ajouté, l’horodatage personnalisé peut être renseigné à l’aide du champ `xdm:lastUpdatedDate`. Lorsqu&#39;un enregistrement est assimilé au champ `xdm:lastUpdatedDate` renseigné, l&#39;Experience Platform utilise ce champ pour fusionner des enregistrements ou des fragments de profil dans et entre des jeux de données. Si `xdm:lastUpdatedDate` n&#39;est pas présent ou n&#39;est pas renseigné, Platform continuera à utiliser l&#39;horodatage système.

>[!NOTE]
>
>Vous devez vous assurer que l&#39;horodatage `xdm:lastUpdatedDate` est renseigné lors de l&#39;envoi d&#39;un PATCH sur le même enregistrement.

Pour obtenir des instructions détaillées sur l&#39;utilisation des schémas à l&#39;aide de l&#39;API Schéma Registry, y compris sur la façon d&#39;ajouter des mixins aux schémas, consultez le [didacticiel de création d&#39;un schéma à l&#39;aide de l&#39;API](../../xdm/tutorials/create-schema-api.md).

Pour utiliser des horodatages personnalisés à l’aide de l’interface utilisateur, reportez-vous à la section [en utilisant des horodatages personnalisés](../ui/merge-policies.md#custom-timestamps) dans le [guide de l’utilisateur des stratégies de fusion](../ui/merge-policies.md).

#### [!DNL External Source System Audit Details Mixin] détails  {#mixin-details}

L&#39;exemple suivant montre les champs correctement renseignés dans [!DNL External Source System Audit Details Mixin]. Le mixin JSON complet peut également être visualisé dans le rapport [Modèle de données d’expérience publique (XDM)](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json) sur GitHub.

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```

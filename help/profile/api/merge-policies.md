---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Point d’entrée de l’API des politiques de fusion
type: Documentation
description: Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chacun de vos clients. Les politiques de fusion sont les règles utilisées par Experience Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée.
role: Developer
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 63%

---

# Point d’entrée des politiques de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chacun de vos clients. Les politiques de fusion sont les règles utilisées par [!DNL Experience Platform] pour déterminer la priorité des données et les données qui seront combinées pour créer cette vue unifiée.

Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Experience Platform, ils sont fusionnés afin de créer un profil unique pour ce client. Lorsque les données provenant de plusieurs sources entrent en conflit (par exemple, si un fragment classe le client comme étant « célibataire » tandis qu’un autre le classe comme étant « marié »), la politique de fusion détermine les informations qui doivent passer en priorité et être incluses dans le profil de l’individu.

À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des politiques de fusion, gérer des politiques existantes et définir une politique de fusion par défaut pour votre organisation dans l’interface utilisateur. Ce guide décrit les étapes à suivre pour utiliser des politiques de fusion à l’aide de l’API .

Pour utiliser les politiques de fusion à l’aide de l’interface utilisateur, reportez-vous au [guide de l’interface utilisateur des politiques de fusion](../merge-policies/ui-guide.md). Pour en savoir plus sur les politiques de fusion en général et sur leur rôle dans Experience Platform, commencez par lire la [ présentation des politiques de fusion ](../merge-policies/overview.md).

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Composants des politiques de fusion {#components-of-merge-policies}

Les politiques de fusion sont privées pour votre organisation, ce qui vous permet de créer différentes politiques pour fusionner les schémas de la manière spécifique dont vous en avez besoin. Toute API accédant à [!DNL Profile] données nécessite une politique de fusion, bien qu’une valeur par défaut soit utilisée si elle n’est pas explicitement fournie. [!DNL Experience Platform] fournit aux organisations une politique de fusion par défaut, ou vous pouvez créer une politique de fusion pour une classe de schéma de modèle de données d’expérience (XDM) spécifique et la marquer comme politique par défaut pour votre organisation.

Chaque organisation peut éventuellement avoir plusieurs politiques de fusion par classe de schéma, mais chaque classe ne peut avoir qu’une seule politique de fusion par défaut. Toute politique de fusion définie par défaut sera utilisée dans les cas où le nom de la classe de schéma est fourni et qu’une politique de fusion est requise, mais pas fournie.

>[!NOTE]
>
>Lorsque vous définissez une nouvelle politique de fusion comme valeur par défaut, toute politique de fusion existante précédemment définie comme valeur par défaut est automatiquement mise à jour et ne sera plus utilisée comme valeur par défaut.

Pour garantir que tous les consommateurs de profils utilisent la même vue sur les bords, les politiques de fusion peuvent être marquées comme Active-on-Edge (actives sur le bord). Pour qu’une audience soit activée sur le serveur Edge (marquée comme audience Edge), elle doit être liée à une politique de fusion marquée comme Active-on-Edge (active sur le serveur Edge). Si une audience n’est **pas** liée à une politique de fusion marquée comme Active-On-Edge (active sur le bord), l’audience ne sera pas marquée comme Active-On-Edge (active sur le bord), et sera marquée comme une audience de diffusion en continu.

En outre, chaque organisation ne peut avoir qu’une seule politique de fusion **une** Active-On-Edge (active sur le bord). Si une politique de fusion est active sur le serveur Edge, elle peut être utilisée pour d’autres systèmes sur le serveur Edge, tels que le profil Edge, la segmentation Edge et les destinations sur Edge.

### Objet de politique de fusion complet

L’objet de politique de fusion complet est un ensemble de préférences contrôlant les aspects de la fusion de fragments de profil.

**Objet de politique de fusion**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Propriété | Description |
|---|---|
| `id` | Le système a généré un identifiant unique attribué au moment de la création. |
| `name` | Nom convivial par lequel la politique de fusion peut être identifiée dans les vues Liste. |
| `imsOrgId` | Identifiant d’organisation auquel appartient cette politique de fusion. |
| `schema.name` | Faisant partie de l’objet [`schema`](#schema) , le champ `name` contient la classe de schéma XDM à laquelle la politique de fusion se rapporte. Pour plus d’informations sur les schémas et les classes, consultez la [documentation XDM](../../xdm/home.md). |
| `version` | [!DNL Experience Platform] version conservée de la politique de fusion. Cette valeur en lecture seule est incrémentée chaque fois qu’une politique de fusion est mise à jour. |
| `identityGraph` | Objet de [graphique d’identités](#identity-graph) indiquant le graphique d’identités à partir duquel les identités associées seront obtenues. Les fragments de profil trouvés pour toutes les identités associées seront fusionnés. |
| `attributeMerge` | [Fusion d’attributs](#attribute-merge) objet indiquant la manière dont la politique de fusion donnera la priorité aux attributs de profil en cas de conflits de données. |
| `isActiveOnEdge` | Valeur booléenne indiquant si cette politique de fusion peut être utilisée sur Edge. Par défaut, cette valeur est `false`. |
| `default` | Valeur booléenne indiquant si cette politique de fusion est la valeur par défaut du schéma spécifié. |
| `updateEpoch` | Date de la dernière mise à jour de la politique de fusion. |

**Exemple de stratégie de fusion**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Graphique d’identités {#identity-graph}

[Adobe Experience Platform Identity Service ](../../identity-service/home.md) gère les graphiques d’identités utilisés au niveau mondial et pour chaque organisation sur [!DNL Experience Platform]. L’attribut `identityGraph` de la politique de fusion définit la manière de déterminer les identités associées pour un utilisateur.

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

Un fragment de profil correspond aux informations de profil d’une seule identité de la liste d’identités qui existe pour un utilisateur particulier. Lorsque le type de graphique d’identité utilisé génère plusieurs identités, il existe un risque de conflit entre les attributs de profil. Une priorité doit alors être spécifiée. En utilisant `attributeMerge`, vous pouvez spécifier les attributs de profil auxquels donner la priorité en cas de conflit de fusion entre des jeux de données de type Valeur clé (données d’enregistrement) .

**Objet attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Où `{ATTRIBUTE_MERGE_TYPE}` peut prendre une de ces valeurs :

* **`timestampOrdered`** : (par défaut) donnez la priorité au profil qui a été mis à jour en dernier. Avec ce type de fusion, l’attribut `data` n’est pas obligatoire.
* **`dataSetPrecedence`** : donnez la priorité aux fragments de profil en fonction du jeu de données duquel ils sont issus. Cela peut être utilisé lorsque les informations présentes dans un jeu de données sont préférées ou approuvées par rapport aux données d’un autre jeu de données. Lors de l’utilisation de ce type de fusion, l’attribut `order` est obligatoire, car il répertorie les jeux de données dans l’ordre de priorité.
   * **`order`** : lorsque « dataSetPrecedence » est utilisé, un tableau `order` doit être fourni avec une liste de jeux de données. Les jeux de données qui ne font pas partie de la liste ne sont pas fusionnés. En d’autres termes, les jeux de données doivent être explicitement répertoriés pour être fusionnés dans un profil. Le tableau `order` répertorie les identifiants des jeux de données par ordre de priorité.

#### Exemple d’objet `attributeMerge` utilisant le type de `dataSetPrecedence`

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### Exemple d’objet `attributeMerge` utilisant le type de `timestampOrdered`

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schéma {#schema}

L’objet de schéma spécifie la classe de schéma du modèle de données d’expérience (XDM) pour laquelle cette politique de fusion est créée.

**`schema`Objet**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Où la valeur de `name` est le nom de la classe XDM sur laquelle repose le schéma associé à la politique de fusion.

**Exemple`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Pour en savoir plus sur XDM et l’utilisation des schémas dans Experience Platform, commencez par lire la [présentation du système XDM](../../xdm/home.md).

## Accéder aux politiques de fusion {#access-merge-policies}

À l’aide de l’API [!DNL Real-Time Customer Profile], le point d’entrée `/config/mergePolicies` vous permet d’effectuer une requête de recherche pour afficher une politique de fusion spécifique selon son identifiant ou d’accéder à toutes les politiques de fusion de votre organisation, filtrées selon des critères spécifiques. Vous pouvez également utiliser le point d’entrée `/config/mergePolicies/bulk-get` pour récupérer plusieurs politiques de fusion en fonction de leurs identifiants. Les étapes de chacun de ces appels sont décrites dans les sections suivantes.

### Accès à une politique de fusion unique par identifiant

Vous pouvez accéder à une politique de fusion unique à l’aide de son identifiant en exécutant une requête GET sur le point de terminaison `/config/mergePolicies` et en incluant le paramètre `mergePolicyId` dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la politique de fusion à supprimer. |

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Réponse**

Une réponse réussie renvoie les détails de la politique de fusion.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

Pour en savoir plus sur chacun des éléments qui constituent une politique de fusion, reportez-vous à la section [Composants des politiques de fusion](#components-of-merge-policies) au début de ce document.

### Récupérer plusieurs politiques de fusion en fonction de leurs identifiants

Vous pouvez récupérer plusieurs politiques de fusion en adressant une requête POST au point d’entrée `/config/mergePolicies/bulk-get` et en incluant les identifiants des politiques de fusion que vous souhaitez récupérer dans le corps de la requête.

**Format d’API**

```http
POST /config/mergePolicies/bulk-get
```

**Requête**

Le corps de la requête comprend un tableau « ids » avec des objets individuels contenant l’« id » pour chaque politique de fusion pour laquelle vous souhaitez récupérer des détails.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie le statut HTTP 207 (multi-statut) et les détails des politiques de fusion dont les ID ont été fournis dans la requête POST.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Pour en savoir plus sur chacun des éléments qui constituent une politique de fusion, reportez-vous à la section [Composants des politiques de fusion](#components-of-merge-policies) au début de ce document.

### Répertorier plusieurs politiques de fusion par critère

Vous pouvez répertorier plusieurs politiques de fusion au sein de votre organisation en émettant une requête GET au point d’entrée `/config/mergePolicies` et en utilisant des paramètres de requête facultatifs pour filtrer, classer et paginer la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (&amp;). Un appel à ce point de terminaison sans paramètre permet de récupérer toutes les politiques de fusion disponibles pour votre organisation.

**Format d’API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Paramètre | Description |
|---|---|
| `default` | Valeur booléenne filtrant les résultats selon que les politiques de fusion sont ou non la valeur par défaut d’une classe de schémas. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. Valeur par défaut : 20 |
| `orderBy` | Spécifie le champ de référence pour classer les résultats comme dans `orderBy=name` ou `orderBy=+name` pour un tri par nom dans l’ordre croissant ou `orderBy=-name` pour un tri dans l’ordre décroissant. Si vous omettez cette valeur, le tri par défaut de `name` s’effectue dans l’ordre croissant. |
| `isActiveOnEdge` | Valeurs booléennes qui filtrent les résultats selon que les politiques de fusion sont actives ou non sur le serveur Edge. |
| `schema.name` | Nom du schéma pour lequel récupérer les politiques de fusion disponibles. |
| `identityGraph.type` | Filtre les résultats par type de graphique d’identités. Les valeurs possibles sont &quot;none&quot; et &quot;pdg&quot; (graphique privé). |
| `attributeMerge.type` | Filtre les résultats par type de fusion d’attributs utilisé. Les valeurs possibles sont &quot;timestampOrdered&quot; et &quot;dataSetPrecedence&quot;. |
| `start` | Décalage de page : spécifiez l’identifiant de début pour les données à récupérer. Valeur par défaut : 0 |
| `version` | Indiquez cette valeur si vous souhaitez utiliser une version spécifique de la politique de fusion. Par défaut, la dernière version sera utilisée. |

Pour plus d’informations sur `schema.name`, `identityGraph.type` et `attributeMerge.type`, référez-vous à la section [Composants des politiques de fusion](#components-of-merge-policies) au début de ce document.


**Requête**

La requête suivante répertorie toutes les politiques de fusion pour un schéma donné :

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Réponse**

Une réponse réussie renvoie une liste paginée de politiques de fusion qui répond aux critères spécifiés par les paramètres envoyés dans la requête.

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
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
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
| `_links.next.href` | Adresse URI de la page de résultats suivante. Utilisez cet URI comme paramètre de requête pour un autre appel API vers le même point d’entrée pour afficher la page. S’il n’y a pas de page suivante, cette valeur est une chaîne vide. |

## Création d’une politique de fusion

Vous pouvez créer une politique de fusion pour votre organisation en exécutant une requête POST sur le point de terminaison `/config/mergePolicies`.

**Format d’API**

```http
POST /config/mergePolicies
```

**Requête**
La requête suivante crée une nouvelle politique de fusion, configurée par les valeurs d’attribut fournies dans le payload :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| Propriété | Description |
|---|---|
| `name` | Nom convivial par lequel la politique de fusion peut être identifiée dans les vues Liste. |
| `identityGraph.type` | Type de graphique d’identités à partir duquel obtenir les identités connexes à fusionner. Valeurs possibles : &quot;none&quot; ou &quot;pdg&quot; (graphique privé). |
| `attributeMerge` | Méthode de hiérarchisation des valeurs d’attribut de profil en cas de conflit de données. |
| `schema` | Classe de schéma XDM associée à la politique de fusion. |
| `isActiveOnEdge` | Indique si cette politique de fusion est active sur le serveur Edge. |
| `default` | Spécifie si cette politique de fusion est la politique par défaut pour le schéma. |

Pour plus d’informations, reportez-vous à la section [Composants des politiques de fusion](#components-of-merge-policies).

**Réponse**

Une réponse réussie renvoie les détails de la politique de fusion créée.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

Pour en savoir plus sur chacun des éléments qui constituent une politique de fusion, reportez-vous à la section [Composants des politiques de fusion](#components-of-merge-policies) au début de ce document.

## Mise à jour d’une politique de fusion {#update}

Vous pouvez modifier une politique de fusion existante en changeant les attributs individuels (PATCH) ou en remplaçant la politique de fusion complète par de nouveaux attributs (PUT). Vous en trouverez des exemples ci-dessous.

### Modification des champs de politique de fusion individuels

Vous pouvez modifier des champs individuels pour une politique de fusion en exécutant une requête PATCH au point de terminaison `/config/mergePolicies/{mergePolicyId}` :

**Format d’API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la politique de fusion à supprimer. |

**Requête**

La requête suivante met à jour une politique de fusion spécifiée en définissant la valeur de sa propriété `default` sur `true` :

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Spécifie l’opération à effectuer. Vous trouverez des exemples d’autres opérations PATCH dans la documentation [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902). |
| `path` | Chemin du champ à mettre à jour. Les valeurs acceptées sont les suivantes : « /name », « /identityGraph.type », « /attributeMerge.type », « /schema.name », « /version », « /default », « /isActiveOnEdge » |
| `value` | Valeur sur laquelle le champ spécifié doit être défini. |

Pour plus d’informations, reportez-vous à la section [Composants des politiques de fusion](#components-of-merge-policies).


**Réponse**

Une réponse réussie renvoie les détails de la politique de fusion mise à jour.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

### Remplacement d’une politique de fusion

Une façon de modifier une politique de fusion consiste à utiliser une requête PUT, qui remplace entièrement la politique de fusion.

**Format d’API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la politique de fusion à remplacer. |

**Requête**

La requête suivante remplace la politique de fusion spécifiée, en changeant ses valeurs d’attribut par celles fournies dans le payload. Puisque cette requête remplace complètement une politique de fusion existante, vous devez fournir tous les champs requis lors de la définition initiale de la politique de fusion. Toutefois, cette fois, vous fournissez des valeurs mises à jour pour les champs que vous souhaitez modifier.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": true,
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Propriété | Description |
|---|---|
| `name` | Nom convivial par lequel la politique de fusion peut être identifiée dans les vues Liste. |
| `identityGraph` | Graphique d’identités à partir duquel obtenir les identités connexes à fusionner. |
| `attributeMerge` | Méthode de hiérarchisation des valeurs d’attribut de profil en cas de conflit de données. |
| `schema` | Classe de schéma XDM associée à la politique de fusion. |
| `isActiveOnEdge` | Indique si cette politique de fusion est active sur le serveur Edge. |
| `default` | Spécifie si cette politique de fusion est la politique par défaut pour le schéma. |

Pour plus d’informations, reportez-vous à la section [Composants des politiques de fusion](#components-of-merge-policies).

**Réponse**

Une réponse réussie renvoie les détails de la politique de fusion mise à jour.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## Suppression d’une politique de fusion

Vous pouvez supprimer une politique de fusion en exécutant une requête DELETE au point de terminaison `/config/mergePolicies` et en incluant l’identifiant de la politique de fusion que vous souhaitez supprimer dans le chemin d’accès de la requête.

>[!NOTE]
>
>Si la politique de fusion a `isActiveOnEdge` définie sur true, la politique de fusion **ne peut pas** ne peut pas être supprimée. Utilisez les points d’entrée [PATCH](#edit-individual-merge-policy-fields) ou [PUT](#overwrite-a-merge-policy) pour mettre à jour la politique de fusion avant de la supprimer.

**Format d’API**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Paramètre | Description |
|---|---|
| `{mergePolicyId}` | Identifiant de la politique de fusion à supprimer. |

**Requête**

La requête suivante supprime une politique de fusion.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une requête de suppression réussie renvoie un état HTTP 200 (OK) et un corps de réponse vide. Pour confirmer que la suppression a réussi, vous pouvez exécuter une requête GET pour afficher la politique de fusion à l’aide de son identifiant. Si la politique de fusion a été supprimée, vous recevrez un état HTTP 404 (Introuvable).

## Étapes suivantes

Maintenant que vous savez comment créer et configurer des politiques de fusion pour votre organisation, vous pouvez les utiliser pour ajuster la vue des profils clients dans Experience Platform et pour créer des audiences à partir de vos données [!DNL Real-Time Customer Profile].

Consultez la [documentation du service de segmentation Adobe Experience Platform](../../segmentation/home.md) pour commencer à définir et à utiliser les audiences.

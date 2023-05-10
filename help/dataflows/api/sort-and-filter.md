---
title: Tri et filtrage des réponses dans l’API Flow Service
description: Ce tutoriel décrit la syntaxe à utiliser pour trier et filtrer à l’aide des paramètres de requête dans l’API Flow Service, y compris certains cas d’utilisation avancés.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: ef8db14b1eb7ea555135ac621a6c155ef920e89a
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 4%

---

# Tri et filtrage des réponses dans l’API Flow Service

Lors de l’exécution de requêtes de liste (GET) dans la variable [API de service de flux](https://www.adobe.io/experience-platform-apis/references/flow-service/), vous pouvez utiliser des paramètres de requête pour trier et filtrer les réponses. Ce guide fournit une référence pour l’utilisation de ces paramètres pour différents cas d’utilisation.

## Tri 

Vous pouvez trier les réponses à l’aide d’une `orderby` paramètre de requête. Les ressources suivantes peuvent être triées dans l’API :

* [Connexions](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Connexions source](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Connexions à Target](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flux](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Exécutions](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Pour utiliser le paramètre , vous devez définir sa valeur sur la propriété spécifique selon laquelle vous souhaitez effectuer un tri (par exemple, `?orderby=name`). Vous pouvez ajouter en préfixe la valeur à l’aide d’un signe plus (`+`) pour l’ordre croissant ou le signe moins (`-`) pour l’ordre décroissant. Si aucun préfixe d’ordre n’est fourni, la liste est triée par défaut dans l’ordre croissant.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

Vous pouvez également combiner un paramètre de tri avec un paramètre de filtrage à l’aide d’un symbole &quot;et&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtrage

Vous pouvez filtrer les réponses à l’aide d’une `property` avec une expression clé-valeur. Par exemple : `?property=id==12345` renvoie uniquement les ressources dont la `id` est exactement égal à `12345`.

Le filtrage peut être appliqué de manière générique sur n’importe quelle propriété d’une entité tant que le chemin d’accès valide à cette propriété est connu.

>[!NOTE]
>
>Si une propriété est imbriquée dans un élément de tableau, vous devez ajouter des crochets (`[]`) au tableau du chemin d’accès. Voir la section sur [filtrage sur les propriétés de tableau](#arrays) pour obtenir des exemples.

**Renvoie toutes les connexions source dont le nom de la table source est `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Renvoie tous les flux pour un identifiant de segment spécifique :**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Combinaison de filtres

Multiple `property` Les filtres peuvent être inclus dans une requête à condition qu’ils soient séparés par des caractères &quot;et&quot; (`&`). Une relation ET est supposée lors de la combinaison de filtres, ce qui signifie qu’une entité doit satisfaire tous les filtres pour qu’elle soit incluse dans la réponse.

**Renvoie tous les flux activés pour un identifiant de segment :**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtrage sur les propriétés de tableau {#arrays}

Vous pouvez filtrer selon les propriétés des éléments dans des tableaux en ajoutant `[]` au nom de la propriété de tableau.

**Flux de retour associés à des connexions source spécifiques :**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Renvoie les flux qui ont une transformation contenant un identifiant de valeur de sélecteur spécifique :**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Renvoie les connexions source qui comportent une colonne avec une `name` value:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Recherchez l’identifiant d’exécution de flux pour une destination en filtrant sur l’identifiant de segment :**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Toute requête de filtrage peut être ajoutée avec `count` paramètre de requête avec la valeur de `true` pour renvoyer le nombre de résultats. La réponse de l’API contient une `count` dont la valeur représente le nombre total d’éléments filtrés. Les éléments filtrés réels ne sont pas renvoyés dans cet appel.

**Renvoie le nombre de flux activés dans le système :**

```http
GET /flows?property=state==enabled&count=true
```

La réponse à la requête ci-dessus ressemblerait à ce qui suit :

```json
{
  "count": 95
}
```

### Propriétés filtrables par ressource

Selon l’entité de service de flux que vous récupérez, différentes propriétés peuvent être utilisées pour le filtrage. Les tableaux ci-dessous ventilent les champs au niveau racine pour chaque ressource couramment utilisée dans les cas d’utilisation de filtrage.

**`connectionSpec`**

| Propriété | Exemple |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| Propriété | Exemple |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| Propriété | Exemple |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| Propriété | Exemple |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| Propriété | Exemple |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`flow`**

| Propriété | Exemple |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style="table-layout:auto"}

**`run`**

| Propriété | Exemple |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## Étapes suivantes

Ce guide explique comment utiliser la variable `orderby` et `property` paramètres de requête pour trier et filtrer les réponses dans l’API Flow Service. Pour obtenir des guides détaillés sur l’utilisation de l’API pour les processus courants dans Platform, consultez les tutoriels sur l’API contenus dans la [sources](../../sources/home.md) et [destinations](../../destinations/home.md) documentation.

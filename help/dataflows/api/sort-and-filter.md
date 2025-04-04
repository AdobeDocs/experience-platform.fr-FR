---
title: Tri et filtrage des réponses dans l’API Flow Service
description: Ce tutoriel décrit la syntaxe pour le tri et le filtrage à l’aide de paramètres de requête dans l’API Flow Service, y compris certains cas d’utilisation avancés.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---

# Tri et filtrage des réponses dans l’API Flow Service

Lors de l’exécution de requêtes de liste (GET) dans l’[API Flow Service](https://www.adobe.io/experience-platform-apis/references/flow-service/), vous pouvez utiliser des paramètres de requête pour trier et filtrer les réponses. Ce guide fournit une référence sur l’utilisation de ces paramètres pour différents cas d’utilisation.

## Tri

Vous pouvez trier les réponses à l’aide d’un paramètre de requête `orderby`. Les ressources suivantes peuvent être triées dans l’API :

* [Connexions](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Connexions Source](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Connexions Target](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flux](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Exécutions](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Pour utiliser le paramètre , vous devez définir sa valeur sur la propriété spécifique selon laquelle vous souhaitez effectuer un tri (par exemple, `?orderby=name`). Vous pouvez ajouter le signe plus (`+`) comme signe plus (croissant) ou le signe moins (`-`) comme signe moins (décroissant). Si aucun préfixe de tri n’est fourni, la liste est triée par défaut par ordre croissant.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

Vous pouvez également combiner un paramètre de tri avec un paramètre de filtrage à l’aide d’un symbole « et » (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtrage

Vous pouvez filtrer les réponses à l’aide d’un paramètre `property` avec une expression clé-valeur. Par exemple, `?property=id==12345` renvoie uniquement les ressources dont la propriété `id` est exactement égale à `12345`.

Le filtrage peut être appliqué de manière générique à n’importe quelle propriété d’une entité tant que le chemin d’accès valide à cette propriété est connu.

>[!NOTE]
>
>Si une propriété est imbriquée dans un élément de tableau, vous devez ajouter des crochets (`[]`) au tableau du chemin d’accès . Voir la section sur le [filtrage sur les propriétés de tableau](#arrays) pour obtenir des exemples.

**Renvoyer toutes les connexions source dont le nom de la table source est `lead` :**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Renvoie tous les flux pour un identifiant de segment spécifique :**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Combinaison de filtres

Plusieurs filtres `property` peuvent être inclus dans une requête à condition qu’ils soient séparés par des caractères « et » (`&`). Une relation AND est supposée lors de la combinaison de filtres, ce qui signifie qu’une entité doit satisfaire tous les filtres pour être incluse dans la réponse.

**Renvoyer tous les flux activés pour un identifiant de segment :**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtrage sur les propriétés du tableau {#arrays}

Vous pouvez filtrer en fonction des propriétés des éléments dans les tableaux en ajoutant `[]` au nom de la propriété de tableau.

**Flux de retour associés à des connexions source spécifiques :**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Flux de retour ayant une transformation contenant une valeur de sélecteur spécifique ID:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Renvoyer les connexions source qui ont une colonne avec une valeur de `name` spécifique :**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Recherchez l’identifiant d’exécution de flux pour une destination en filtrant sur l’identifiant de segment :**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Toute requête de filtrage peut être ajoutée avec `count` paramètre de requête avec une valeur de `true` pour renvoyer le nombre de résultats. La réponse de l’API contient une propriété `count` dont la valeur représente le nombre total d’éléments filtrés. Les éléments filtrés réels ne sont pas renvoyés dans cet appel.

**Renvoyer le nombre de flux activés dans le système :**

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

Selon l’entité de service de flux que vous récupérez, différentes propriétés peuvent être utilisées pour le filtrage. Les tableaux ci-dessous répartissent les champs au niveau racine pour chaque ressource couramment utilisée dans le filtrage des cas d’utilisation.

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

## Cas d’utilisation {#use-cases}

Lisez cette section pour obtenir des exemples spécifiques d’utilisation du filtrage et du tri pour renvoyer des informations sur certains connecteurs ou pour vous aider à déboguer les problèmes. Si vous souhaitez qu’Adobe ajoute d’autres cas d’utilisation, utilisez les **[!UICONTROL options de commentaires détaillés]** de la page pour envoyer une demande.

**Filtrer pour renvoyer les connexions vers une certaine destination uniquement**

Vous pouvez utiliser des filtres pour renvoyer les connexions à certaines destinations uniquement. Tout d’abord, interrogez le point d’entrée `connectionSpecs` comme suit :

```http
GET /connectionSpecs
```

Ensuite, recherchez l’`connectionSpec` souhaitée en examinant le paramètre `name` . Par exemple, recherchez Amazon Ads, Pega, SFTP, etc. dans le paramètre `name`. L’`id` correspondant est le `connectionSpec` par lequel vous pouvez effectuer une recherche dans l’appel API suivant.

Par exemple, filtrez vos destinations pour renvoyer uniquement les connexions existantes aux connexions Amazon S3 :

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtrer pour renvoyer uniquement les flux de données aux destinations**

Lors de l’interrogation du point d’entrée `/flows`, au lieu de renvoyer tous les flux de données sources et destinations, vous pouvez utiliser un filtre pour renvoyer uniquement les flux de données aux destinations. Pour ce faire, utilisez `isDestinationFlow` comme paramètre de requête, comme suit :

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**Filtrer pour renvoyer les flux de données vers une certaine source ou destination uniquement**

Vous pouvez filtrer les flux de données pour renvoyer les flux de données vers une certaine destination ou à partir d’une certaine source uniquement. Par exemple, filtrez vos destinations pour renvoyer uniquement les connexions existantes aux connexions Amazon S3 :

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtrer pour obtenir toutes les exécutions d’un flux de données pour une période spécifique**

Vous pouvez filtrer les exécutions d’un flux de données pour n’examiner que les exécutions d’un certain intervalle de temps, comme ci-dessous :

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**Filtrer pour renvoyer uniquement les flux de données ayant échoué**

À des fins de débogage, vous pouvez filtrer et afficher toutes les exécutions de flux de données ayant échoué pour un certain flux de données source ou de destination, comme ci-dessous :

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Étapes suivantes

Ce guide explique comment utiliser les paramètres de requête `orderby` et `property` pour trier et filtrer les réponses dans l’API Flow Service. Pour obtenir des guides détaillés sur l’utilisation de l’API pour les workflows courants dans Experience Platform, consultez les tutoriels sur l’API contenus dans les documents [sources](../../sources/home.md) et [destinations](../../destinations/home.md).

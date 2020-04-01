---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation du langage  (PQL)
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Présentation du langage  (PQL)

Le langage  de  de (PQL) est un langage delangage compatible XDM (Experience Data Model), conçu pour prendre en charge la définition et l’exécution de l’de segmentation pour les données de l’analyse desclients en temps réel.

Ce guide présente un aperçu général de PQL, qui couvre les lignes directrices de formatage et fournit des exemples de  PQL .

## Formatage des PQL 

Les  PQL ont la signature suivante :

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Le paramètre d’entrée peut être une primitive simple, telle qu’une valeur booléenne ou une chaîne, ou un type plus complexe, tel qu’un objet, un tableau ou un mappage.

Il existe **trois** façons différentes de faire référence aux paramètres d’entrée dans le corps d’un  PQL  :

### Référence implicite au premier paramètre

Dans l’exemple ci-dessous, puisque le premier paramètre est toujours dans le contexte, une référence de propriété (`homeAddress`) peut être directement associée.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Référence explicite au premier paramètre

Dans l’exemple ci-dessous, `$1` fait référence au premier paramètre. Par conséquent, `$2` ferait référence au deuxième paramètre, etc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Utilisation de variables nommées, à l’aide de la notation lambda

Dans l’exemple ci-dessous, `Profile` il s’agit d’un nom de variable qui peut être choisi par l’auteur du .

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Littéraux PQL

PQL prend en charge les types littéraux suivants :

| Littéral | Définition | Exemple |
| ------- | ---------- | ------- |
| Chaîne | Type de données composé de caractères entourés de guillemets . | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booléen | Type de données vrai ou faux. | `true`, `false` |
| Entier | Type de données représentant un nombre entier. Il peut être positif, négatif ou nul. | `-201`, `0`, `412` |
| Double | Type de données représentant n’importe quel nombre réel. Il peut être positif, négatif ou nul. | `-51.24`, `3.14`, `0.6942058` |
| Date | Type de données pouvant être utilisé pour créer des dates basées sur l’année, le mois et le jour sous forme de paramètres entiers. It is formatted as `date(year, month, day)` | `date(2020, 3, 14)` |
| Tableau | Type de données constitué d’un groupe d’autres valeurs littérales. Elle utilise des crochets pour regrouper et des virgules pour délimiter différentes valeurs. <br> **Remarque :** Vous ne pouvez pas accéder directement aux propriétés des éléments d’un tableau. Ainsi, si vous devez accéder à une propriété dans un tableau, la méthode prise en charge est `select X from array where X.item = ...`. <br> PQL se réserve le droit `xEvent` de faire référence à un ensemble de d’expérience liés à un . | `[1, 4, 7]`, `["US", "CA"]` |
| Références temporelles relatives | Mots réservés pouvant être utilisés pour former des références d’horodatage et d’intervalle de temps. <ul><li>aujourd&#39;hui, hier, demain</li><li>ceci, dernier, suivant</li><li>before, after, from</li><li>milliseconde(s), deuxième(s), minute(s), heure(s), jour(s), semaine(s), mois, année(s), décennie(s), siècle/siècles, millénaire/millénaire</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## Fonctions PQL

Le tableau suivant décrit les différents  des fonctions PQL prises en charge, y compris des liens vers d’autres documents pour plus d’informations.

| Catégorie | Définition |
| -------- | ---------- |
| Booléen | Utilisé pour implémenter l’algèbre booléenne dans PQL. Vous trouverez plus d&#39;informations sur ces fonctions dans le de fonctions [booléennes](./boolean-functions.md). |
| Comparaison | Utilisé pour comparer différents éléments PQL. Vous trouverez plus d&#39;informations sur ces fonctions dans le des fonctions de [comparaison](./comparison-functions.md). |
| Tableau,  et définition | Utilisé pour interagir avec des tableaux, des  et des ensembles. Vous trouverez plus d&#39;informations sur ces fonctions dans le [tableau, le  et le des fonctions de définition des fonctions](./array-functions.md). |
| Carte | Utilisé pour interagir avec les cartes. Vous trouverez plus d&#39;informations sur ces fonctions dans le de fonctions [map](./map-functions.md). |
| Chaîne | Utilisé pour interagir avec des chaînes. Vous trouverez plus d&#39;informations sur ces fonctions dans le des fonctions de [chaîne](./string-functions.md). |
| Arithmétique | Utilisé pour effectuer des opérations arithmétiques de base sur des éléments PQL. Pour plus d&#39;informations sur ces fonctions, reportez-vous au des fonctions [arithmétiques](./arithmetic-functions.md) |
| Agrégation | Utilisé pour combiner les résultats d’un tableau en un résultat unique. Vous trouverez plus d&#39;informations sur les fonctions d&#39;agrégation dans le [des fonctions d&#39;agrégation](./aggregation-functions.md). |
| Date et heure | Utilisé conjointement avec les objets date, time et datetime. Pour plus d&#39;informations sur ces fonctions, consultez le [des fonctions de date et d&#39;heure](./datetime-functions.md). |
| Filtrer | Utilisé pour filtrer les données dans les tableaux. Vous trouverez plus d&#39;informations sur ces fonctions dans le des fonctions de [filtre](./filter-functions.md). |
| Quantificateurs logiques | Utilisé pour insérer des conditions dans un tableau. Vous trouverez plus d&#39;informations dans le des quantificateurs [logiques](./logical-quantifiers.md). |
| Divers | Les fonctions qui ne tiennent pas dans l&#39;un des  ci-dessus se trouvent dans le des fonctions [diverses](./misc-functions.md). |

## Étapes suivantes

Maintenant que vous avez appris à utiliser le langage de , vous pouvez utiliser PQL lors de la création et de la modification de segments. Pour plus d’informations sur la segmentation, veuillez lire la présentation [de la](../home.md)segmentation.
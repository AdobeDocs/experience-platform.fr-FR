---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation du langage PQL (Profil Requête Language)
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 3%

---


# Présentation du langage PQL (Profil Requête Language)

Le langage PQL (Profil Requête Language) est un langage de requête compatible XDM (Experience Data Model) conçu pour prendre en charge la définition et l’exécution de requêtes de segmentation pour les données de Profil client en temps réel.

Ce guide présente un aperçu général de PQL, qui couvre les lignes directrices de formatage et fournit des exemples d’expressions PQL.

## Mise en forme des requêtes PQL

Les requêtes PQL ont la signature suivante :

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Le paramètre d’entrée peut être une primitive simple, telle qu’une valeur booléenne ou une chaîne, ou un type plus complexe, tel qu’un objet, un tableau ou une carte.

Il existe **trois** façons différentes de faire référence aux paramètres d’entrée dans le corps d’une expression PQL :

### Référence implicite au premier paramètre

Dans l’exemple ci-dessous, puisque le premier paramètre est toujours en contexte, une référence de propriété (`homeAddress`) peut être directement associée à celui-ci.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Référence explicite au premier paramètre

Dans l’exemple ci-dessous, `$1` fait référence au premier paramètre. Par conséquent, `$2` se reporter au deuxième paramètre, etc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Utilisation de variables nommées, à l’aide de la notation lambda

Dans l&#39;exemple ci-dessous, `Profile` est un nom de variable, qui peut être choisi par l&#39;auteur de la requête.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Littéraux PQL

PQL prend en charge les types littéraux suivants :

| Littéral | Définition | Exemple |
| ------- | ---------- | ------- |
| Chaîne | Type de données composé de caractères entourés de guillemets de doublon. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booléen | Type de données vrai ou faux. | `true`, `false` |
| Entier | Type de données représentant un nombre entier. Il peut être positif, négatif ou nul. | `-201`, `0`, `412` |
| Double | Type de données représentant n’importe quel nombre réel. Il peut être positif, négatif ou nul. | `-51.24`, `3.14`, `0.6942058` |
| Date | Type de données qui peut être utilisé pour créer des dates basées sur l’année, le mois et le jour sous forme de paramètres entiers. It is formatted as `date(year, month, day)` | `date(2020, 3, 14)` |
| Tableau | Type de données composé en tant que groupe d’autres valeurs littérales. Elle utilise des crochets pour regrouper et des virgules pour délimiter les valeurs. <br> **Remarque :** Vous ne pouvez pas accéder directement aux propriétés des éléments d&#39;un tableau. Ainsi, si vous devez accéder à une propriété dans un tableau, la méthode prise en charge est `select X from array where X.item = ...`. <br> PQL se réserve le mot `xEvent` pour faire référence à un ensemble de événements d&#39;expérience liés à un profil. | `[1, 4, 7]`, `["US", "CA"]` |
| Références temporelles relatives | Mots réservés pouvant être utilisés pour former des références d’horodatage et d’intervalle de temps. <ul><li>maintenant, aujourd&#39;hui, hier, demain</li><li>this, last, next</li><li>avant, après, de</li><li>milliseconde(s), deuxième(s), minute(s), heure(s), jour(s), semaine(s), mois, année(s), décennie(s), siècle/siècles, millénaire/millénaire</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## Fonctions PQL

Le tableau suivant présente les différentes catégories des fonctions PQL prises en charge, y compris les liens vers d’autres documents pour plus d’informations.

| Catégorie | Définition |
| -------- | ---------- |
| Booléen | Utilisé pour implémenter l’algèbre booléenne dans PQL. Vous trouverez plus d&#39;informations sur ces fonctions dans le document [des fonctions](./boolean-functions.md)booléennes. |
| Comparaison | Utilisé pour comparer différents éléments PQL. Pour plus d&#39;informations sur ces fonctions, consultez le document [des fonctions de](./comparison-functions.md)comparaison. |
| Tableau, liste et ensemble | Utilisé pour interagir avec des tableaux, des listes et des ensembles. Vous trouverez plus d&#39;informations sur ces fonctions dans le document [](./array-functions.md)de la baie, de la liste et des fonctions de définition. |
| Carte | Utilisé pour interagir avec les cartes. Vous trouverez plus d&#39;informations sur ces fonctions dans le document [des fonctions de](./map-functions.md)carte. |
| Chaîne | Utilisé pour interagir avec des chaînes. Vous trouverez plus d&#39;informations sur ces fonctions dans le document [des fonctions de](./string-functions.md)chaîne. |
| Arithmétique | Utilisé pour effectuer des opérations arithmétiques de base sur des éléments PQL. Vous trouverez plus d&#39;informations sur ces fonctions dans le document des fonctions [arithmétiques](./arithmetic-functions.md) |
| Agrégation | Utilisé pour combiner les résultats d&#39;un tableau en un résultat unique. Vous trouverez plus d&#39;informations sur les fonctions d&#39;agrégation dans le document [des fonctions d&#39;](./aggregation-functions.md)agrégation. |
| Date et heure | Utilisé conjointement avec les objets Date, Heure et Date-Time. Vous trouverez plus d&#39;informations sur ces fonctions dans le document [des fonctions](./datetime-functions.md)date/heure. |
| Filtrer | Utilisé pour filtrer les données dans les tableaux. Vous trouverez plus d&#39;informations sur ces fonctions dans le document [des fonctions de](./filter-functions.md)filtrage. |
| Quantificateurs logiques | Utilisé pour insérer des conditions dans un tableau. Vous trouverez plus d&#39;informations dans le document [des quantificateurs](./logical-quantifiers.md)logiques. |
| Divers | Les fonctions qui ne correspondent à aucune des catégories ci-dessus se trouvent dans le document [des fonctions](./misc-functions.md)diverses. |

## Étapes suivantes

Maintenant que vous avez appris à utiliser le langage de Requête de Profil, vous pouvez utiliser PQL lors de la création et de la modification de segments. Pour plus d’informations sur la segmentation, consultez la présentation [de la](../home.md)segmentation.
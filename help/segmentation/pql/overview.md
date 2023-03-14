---
keywords: Experience Platform;accueil;rubriques les plus consultées;PQL;pql;profile query language
solution: Experience Platform
title: Vue d’ensemble de PQL (Profile Query Language)
description: Ce guide présente un aperçu général de PQL, couvre les instructions de formatage et apporte des exemples d’expressions PQL.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 100%

---

# Vue d’ensemble de PQL ([!DNL Profile Query Language])

PQL ([!DNL Profile Query Language]) est un langage de requête compatible avec [!DNL Experience Data Model] (XDM) qui a été conçu pour prendre en charge la définition et l’exécution des requêtes de segmentation pour les données [!DNL Real-Time Customer Profile].

Ce guide présente un aperçu général de PQL, couvre les instructions de formatage et apporte des exemples d’expressions PQL.

## Formatage des requêtes PQL

Les requêtes PQL possèdent la signature suivante :

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Le paramètre d’entrée peut être un primitif simple, comme un booléen ou une chaîne de type plus complexe, comme un objet, un tableau ou une carte.

Il existe trois manières différentes de faire référence aux paramètres d’entrée dans le corps d’une expression PQL :

### Référence implicite au premier paramètre

Dans l’exemple ci-dessous, étant donné le premier paramètre est toujours en contexte, une référence de propriété (`homeAddress`) peut y être directement associée.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Référence explicite au premier paramètre

Dans l’exemple ci-dessous, `$1` fait référence au premier paramètre. Par conséquent, `$2` fait référence au deuxième paramètre, etc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Utilisation de variables nommées, à l’aide de la notation lambda

Dans l’exemple ci-dessous, `Profile` est un nom de variable que l’auteur de la requête peut sélectionner.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Littéraux PQL

PQL prend en charge les types littéraux suivants :

| Littéral | Définition | Exemple |
| ------- | ---------- | ------- |
| Chaîne | Un type de données composé de caractères entourés par des guillemets doubles. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booléen | Un type de données qui est soit vrai soit faux. | `true`, `false` |
| Entier | Un type de données représentant un nombre entier. Ce nombre peut être positif, négatif ou nul. | `-201`, `0`, `412` |
| Double | Un type de données représentant n’importe quel nombre réel. Ce nombre peut être positif, négatif ou nul. | `-51.24`, `3.14`, `0.6942058` |
| Date | Un type de données pouvant être utilisé pour créer des dates en fonction de l’année, du mois et du jour comme paramètres entiers. Celui-ci a la forme `date(year, month, day)` | `date(2020, 3, 14)` |
| Tableau | Un type de données composé d’un groupe d’autres valeurs littérales. Elle utilise des crochets pour regrouper et des virgules pour délimiter les différentes valeurs. <br> **Remarque :** vous ne pouvez pas accéder directement aux propriétés des éléments d’un tableau. C’est pourquoi, si vous devez accéder à une propriété d’un tableau, la méthode prise en charge est `select X from array where X.item = ...`. <br> PQL réserve le terme `xEvent` pour faire référence à un tableau d’événements d’expérience associés à un profil. | `[1, 4, 7]`, `["US", "CA"]` |
| Références de temps relatives | Termes réservés pouvant être utilisés pour former des références de date et heure et d’intervalle de temps. <ul><li>maintenant, aujourd’hui, hier, demain</li><li>ceci, précédent, suivant</li><li>avant, après, depuis</li><li>milliseconde(s), seconde(s), minute(s), heure(s), jour(s), semaine(s), mois, année(s), décennie(s), siècle(s), millénaire(s)</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## Fonctions PQL

Le tableau suivant décrit les différentes catégories des fonctions PQL prises en charge, y compris des liens vers d’autres documents pour plus d’informations.

| Catégorie | Définition |
| -------- | ---------- |
| Booléen | Utilisé pour implémenter une algèbre booléenne dans PQL. Vous trouverez plus d’informations sur ces fonctions dans la [documentation consacrée aux fonctions booléennes](./boolean-functions.md). |
| Comparaison | Utilisé pour comparer différents éléments PQL. Vous trouverez plus d’informations sur ces fonctions dans la [documentation consacrée aux fonctions de comparaison](./comparison-functions.md). |
| Tableau, liste et ensemble | Utilisé pour interagir avec des tableaux, des listes et des ensembles. Vous trouverez plus d’informations sur ces fonctions dans la [documentation consacrée aux fonctions de tableau, de liste et d’ensemble](./array-functions.md). |
| Map | Utilisé pour interagir avec des maps. Vous trouverez plus d’informations sur ces fonctions dans la [documentation consacrée aux fonctions de mappage](./map-functions.md). |
| Chaîne | Utilisé pour interagir avec des chaînes. Vous trouverez plus d’informations sur ces fonctions dans la [documentation consacrée aux fonctions de chaîne](./string-functions.md). |
| Objet | Utilisé pour interagir avec des objets. Vous trouverez plus d’informations sur ces fonctions dans la [documentation consacrée aux fonctions d’objets](./object-functions.md). |
| Arithmétique | Utilisé pour réaliser des fonctions arithmétiques de base sur des éléments PQL. Vous trouverez plus d’informations sur ces fonctions dans la [documentation consacrée aux fonctions arithmétiques](./arithmetic-functions.md) |
| Agrégation | Utilisé pour combiner les résultats d’un tableau en un résultat unique. Vous trouverez plus d’informations sur les fonctions d’agrégation dans la [documentation consacrée aux fonctions d’agrégation](./aggregation-functions.md). |
| Date et heure | Utilisé en association avec les objets date, heure et date-heure. Vous trouverez plus d’informations sur ces fonctions dans la [documentation des fonctions de date/d’heure](./datetime-functions.md). |
| Filtre | Utilisé pour filtrer les données de tableaux. Vous trouverez plus d’informations sur ces fonctions dans la [documentation consacrée aux fonctions de filtre](./filter-functions.md). |
| Quantificateurs logiques | Utilisés pour insérer des conditions dans un tableau. Vous trouverez plus d’informations dans la [documentation consacrée aux quantificateurs logiques](./logical-quantifiers.md). |
| Divers | Vous trouverez des fonctions qui ne correspondent pas à l’une des catégories ci-dessus dans la [documentation consacrée aux fonctions diverses](./misc-functions.md). |

## Étapes suivantes

Maintenant que vous savez comment utiliser [!DNL Profile Query Language], vous pouvez utiliser PQL lorsque vous créez et modifiez des segments. Pour plus d’informations sur la segmentation, veuillez lire la [présentation de la segmentation](../home.md).

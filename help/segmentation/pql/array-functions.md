---
solution: Experience Platform
title: Fonctions de tableau, de liste et de définition de PQL
description: Profile Query Language (PQL) offre des fonctions pour faciliter l’interaction avec des tableaux, des listes et des chaînes.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 57%

---

# Fonctions de tableau, de liste et d’ensemble

[!DNL Profile Query Language] (PQL) offre des fonctions pour faciliter l’interaction avec des tableaux, des listes et des chaînes. Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Dans

La fonction `in` est utilisée pour déterminer si un élément est membre d’un tableau ou d’une liste en tant que valeur booléenne.

**Format**

```sql
{VALUE} in {ARRAY}
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire est en mars, juin ou septembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Not in

La fonction `notIn` permet de déterminer si un élément n’est pas membre d’un tableau ou d’une liste en tant que valeur booléenne.

>[!NOTE]
>
>La fonction `notIn` assure *également* qu&#39;aucune valeur n&#39;est nulle. Par conséquent, les résultats ne sont pas une négation exacte de la fonction `in`.

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire n’est ni en mars, ni en juin, ni en septembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersects

La fonction `intersects` permet de déterminer si deux tableaux ou deux listes ont au moins un membre commun en tant que valeur booléenne.

**Format**

```sql
{ARRAY}.intersects({ARRAY})
```

**Exemple**

La requête PQL suivante définit les personnes dont les couleurs préférées comprennent au moins le rouge, le bleu ou le vert.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersection

La fonction `intersection` est utilisée pour déterminer les membres communs de deux tableaux ou deux listes en tant que liste.

**Format**

```sql
{ARRAY}.intersection({ARRAY})
```

**Exemple**

La requête PQL suivante définit si la personne 1 et la personne°2 ont toutes deux des couleurs préférées parmi le rouge, le bleu et le vert.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subset of

La fonction `subsetOf` sert à déterminer si un tableau spécifique (tableau A) est un sous-ensemble d&#39;un autre tableau (tableau B). En d’autres termes, que tous les éléments du tableau A sont des éléments du tableau B sous la forme d’une valeur booléenne.

**Format**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Exemple**

La requête PQL suivante définit les personnes qui ont visité toutes leurs villes préférées.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superset of

La fonction `supersetOf` sert à déterminer si un tableau spécifique (tableau A) est un sur-ensemble d&#39;un autre tableau (tableau B). En d’autres termes, ce tableau A contient tous les éléments du tableau B sous forme de valeur booléenne.

**Format**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Exemple**

La requête PQL suivante définit les personnes qui ont mangé des sushis et de la pizza au moins une fois.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Includes

La fonction `includes` permet de déterminer si un tableau ou une liste contient un élément donné comme valeur booléenne.

**Format**

```sql
{ARRAY}.includes({ITEM})
```

**Exemple**

La requête PQL suivante définit les personnes dont le rouge est l’une des couleurs préférées.

```sql
person.favoriteColors.includes("red")
```

## Distinct

La fonction `distinct` est utilisée pour supprimer les valeurs en double d’un tableau ou d’une liste en tant que tableau.

**Format**

```sql
{ARRAY}.distinct()
```

**Exemple**

La requête PQL suivante définit les personnes qui ont passé des commandes dans plusieurs magasins.

```sql
person.orders.storeId.distinct().count() > 1
```

## Group by

La fonction `groupBy` est utilisée pour partitionner les valeurs d’un tableau ou d’une liste dans un groupe en fonction de la valeur de l’expression sous la forme d’un mappage à partir des valeurs uniques de l’expression de regroupement vers des tableaux qui sont des partitions de la valeur de l’expression de tableau.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION})
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou liste à regrouper. |
| `{EXPRESSION}` | Expression qui mappe chaque élément du tableau ou de la liste renvoyée. |

**Exemple**

La requête PQL suivante regroupe toutes les commandes par boutique dans laquelle la commande a été placée.

```sql
xEvent[type="order"].groupBy(storeId)
```

## Filtre

La fonction `filter` est utilisée pour filtrer un tableau ou une liste en fonction d’une expression sous la forme d’un tableau ou d’une liste, selon l’entrée.

**Format**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou liste à filtrer. |
| `{EXPRESSION}` | Expression par laquelle filtrer. |

**Exemple**

La requête PQL suivante définit toutes les personnes de 21 ans ou plus.

```sql
person.filter(age >= 21)
```

## Map

La fonction `map` est utilisée pour créer un tableau en appliquant une expression à chaque élément d’un tableau donné sous forme de tableau.

**Format**

```sql
array.map(expression)
```

**Exemple**

La requête PQL suivante crée un tableau de nombres et élève les valeurs d’origine au carré.

```sql
numbers.map(square)
```

## First `n` in array {#first-n}

La fonction `topN` est utilisée pour renvoyer les premiers éléments `N` d’un tableau, lorsqu’ils sont triés dans l’ordre croissant en fonction de l’expression numérique donnée sous forme de tableau.

**Format**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou liste à trier. |
| `{VALUE}` | Propriété dans laquelle trier le tableau ou la liste. |
| `{AMOUNT}` | Nombre d&#39;éléments à renvoyer. |

**Exemple**

La requête PQL suivante renvoie les cinq premières commandes au prix le plus élevé.

```sql
orders.topN(price, 5)
```

## Last `n` in array

La fonction `bottomN` est utilisée pour renvoyer les `N` derniers éléments d’un tableau, lorsqu’ils sont triés dans l’ordre croissant en fonction de l’expression numérique donnée sous forme de tableau.

**Format**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Description |
| --------- | ----------- | 
| `{ARRAY}` | Tableau ou liste à trier. |
| `{VALUE}` | Propriété dans laquelle trier le tableau ou la liste. |
| `{AMOUNT}` | Nombre d&#39;éléments à renvoyer. |

**Exemple**

La requête PQL suivante renvoie les cinq premières commandes au prix le plus bas.

```sql
orders.bottomN(price, 5)
```

## First item

La fonction `head` est utilisée pour renvoyer le premier élément du tableau ou de la liste en tant qu’objet.

**Format**

```sql
{ARRAY}.head()
```

**Exemple**

La requête PQL suivante renvoie la première des cinq premières commandes au prix le plus élevé. Vous trouverez plus d’informations sur la fonction `topN` dans la section [First `n` in array](#first-n).

```sql
orders.topN(price, 5).head()
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions de tableau, de liste et d’ensemble, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).

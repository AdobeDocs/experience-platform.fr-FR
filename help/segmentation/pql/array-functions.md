---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tableau,  et définition de fonctions
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Tableau,  et définition de fonctions

 langage de  de (PQL)  fonctions de afin de faciliter l’interaction avec les tableaux, les et les chaînes. Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## In

La `in` fonction permet de déterminer si un élément est membre d’un tableau ou d’un.

**Format**

```sql
{VALUE} in {ARRAY}
```

**Exemple**

Le PQL suivant  définit les personnes ayant un anniversaire en mars, juin ou septembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Pas dans

La `notIn` fonction permet de déterminer si un élément n’est pas membre d’un tableau ou d’un .

>[!NOTE] La fonction `notIn` assure *également* qu’aucune valeur n’est égale à null. Par conséquent, les résultats ne sont pas une négation exacte de la `in` fonction.

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**Exemple**

Le PQL suivant définit les personnes dont les anniversaires ne sont pas définis en mars, juin ou septembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersectes

La `intersects` fonction permet de déterminer si deux tableaux ou  ont au moins un membre commun.

**Format**

```sql
{ARRAY}.intersects({ARRAY})
```

**Exemple**

Le PQL suivant définit les personnes dont les couleurs préférées comprennent au moins une couleur rouge, bleue ou verte.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersection

La `intersection` fonction sert à déterminer les membres communs de deux tableaux ou de deux  de.

**Format**

```sql
{ARRAY}.intersection({ARRAY})
```

**Exemple**

Le PQL suivant définit si la personne 1 et la personne 2 ont toutes deux des couleurs préférées de rouge, de bleu et de vert.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Sous-ensemble de

La `subsetOf` fonction sert à déterminer si un tableau spécifique (tableau A) est un sous-ensemble d&#39;un autre tableau (tableau B). En d’autres termes, tous les éléments du tableau A sont des éléments du tableau B.

**Format**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Exemple**

Le PQL suivant définit les personnes qui ont visité toutes leurs villes préférées.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superset de

La `supersetOf` fonction sert à déterminer si un tableau spécifique (tableau A) est un superset d&#39;un autre tableau (tableau B). En d’autres termes, ce tableau A contient tous les éléments du tableau B.

**Format**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Exemple**

Le PQL suivant définit les personnes qui ont mangé des sushis et des pizzas au moins une fois.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Inclut

La `includes` fonction permet de déterminer si un tableau ou un contient un élément donné.

**Format**

```sql
{ARRAY}.includes({ITEM})
```

**Exemple**

Le PQL suivant définit les personnes dont la couleur préférée est le rouge.

```sql
person.favoriteColors.includes("red")
```

## Distinct

La `distinct` fonction est utilisée pour supprimer les valeurs  d’un tableau ou d’un  de.

**Format**

```sql
{ARRAY}.distinct()
```

**Exemple**

Le PQL suivant spécifie les personnes qui ont passé des commandes dans plusieurs magasins.

```sql
person.orders.storeId.distinct().count() > 1
```

## Regrouper par

La `groupBy` fonction est utilisée pour partitionner les valeurs d’un tableau ou d’un dans un groupe en fonction de la valeur de la   de l’.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou à regrouper. |
| `{EXPRESSION}` | Un   qui mappe chaque élément du tableau ou le  renvoyé. |

**Exemple**

Le PQL suivant regroupe toutes les commandes dans lesquelles la commande a été placée.

```sql
orders.groupBy(storeId)
```

## Filtrer

La `filter` fonction est utilisée pour filtrer un tableau ou un en fonction d’un  de.

**Format**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou à filtrer. |
| `{EXPRESSION}` | Un  par lequel filtrer. |

**Exemple**

Le PQL suivant définit toutes les personnes de 21 ans ou plus.

```sql
person.filter(age >= 21)
```

## Carte

La `map` fonction sert à créer un tableau en appliquant un   à chaque élément d’un tableau donné.

**Format**

```sql
array.map(expression)
```

**Exemple**

Le PQL suivant crée un nouveau tableau de nombres et place la valeur des nombres d’origine.

```sql
numbers.map(square)
```

## Premier `n` tableau

La `topN` fonction est utilisée pour renvoyer les premiers `N` éléments d’un tableau, lorsqu’ils sont triés dans l’ordre croissant en fonction du de  numérique donné.

**Format**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou à trier. |
| `{VALUE}` | Propriété dans laquelle trier le tableau ou le. |
| `{AMOUNT}` | Nombre d’éléments à renvoyer. |

**Exemple**

Le PQL suivant renvoie les cinq premières commandes au prix le plus élevé.

```sql
orders.topN(price, 5)
```

## Dernier `n` tableau

La `bottomN` fonction est utilisée pour renvoyer les derniers éléments `N` d’un tableau, lorsqu’ils sont triés dans l’ordre croissant en fonction du de  numérique donné.

**Format**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Description |
| --------- | ----------- | 
| `{ARRAY}` | Tableau ou à trier. |
| `{VALUE}` | Propriété dans laquelle trier le tableau ou le. |
| `{AMOUNT}` | Nombre d’éléments à renvoyer. |

**Exemple**

Le PQL suivant renvoie les cinq premières commandes avec le prix le plus bas.

```sql
orders.bottomN(price, 5)
```

## Premier élément

La `head` fonction est utilisée pour renvoyer le premier élément du tableau ou du.

**Format**

```sql
{ARRAY}.head()
```

**Exemple**

Le PQL suivant renvoie la première des cinq premières commandes ayant le prix le plus élevé. Vous trouverez plus d&#39;informations sur la `topN` fonction dans la [première `n` section du tableau](#first-n-in-array) .

```sql
orders.topN(price, 5).head()
```

## Étapes suivantes

Maintenant que vous avez appris sur les baies, les  et les fonctions définies, vous pouvez les utiliser dans votre PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).

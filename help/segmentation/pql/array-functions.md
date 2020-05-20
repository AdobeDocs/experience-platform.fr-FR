---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de tableau, de liste et de définition
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 5%

---


# Fonctions de tableau, de liste et de définition

Les fonctions d’offres PQL (Profil Requête Language) facilitent l’interaction avec les tableaux, les listes et les chaînes. Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## Dans

La `in` fonction est utilisée pour déterminer si un élément est membre d&#39;un tableau ou d&#39;une liste.

**Format**

```sql
{VALUE} in {ARRAY}
```

**Exemple**

La requête PQL suivante définit les personnes ayant un anniversaire en mars, juin ou septembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Pas dans

La `notIn` fonction permet de déterminer si un élément n&#39;est pas membre d&#39;une baie ou d&#39;une liste.

>[!NOTE] La fonction `notIn` assure *également* qu’aucune valeur n’est égale à null. Par conséquent, les résultats ne sont pas une négation exacte de la `in` fonction.

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire n’est ni en mars, ni en juin, ni en septembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersectes

La `intersects` fonction est utilisée pour déterminer si deux baies ou listes ont au moins un membre commun.

**Format**

```sql
{ARRAY}.intersects({ARRAY})
```

**Exemple**

La requête PQL suivante définit les personnes dont les couleurs préférées comprennent au moins une couleur rouge, bleue ou verte.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersection

La `intersection` fonction est utilisée pour déterminer les membres communs de deux tableaux ou listes.

**Format**

```sql
{ARRAY}.intersection({ARRAY})
```

**Exemple**

La requête PQL suivante définit si la personne 1 et la personne 2 ont toutes deux des couleurs préférées de rouge, de bleu et de vert.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Sous-ensemble de

La `subsetOf` fonction est utilisée pour déterminer si un tableau spécifique (tableau A) est un sous-ensemble d&#39;un autre tableau (tableau B). En d&#39;autres termes, tous les éléments du tableau A sont des éléments du tableau B.

**Format**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Exemple**

La requête PQL suivante définit les personnes qui ont visité toutes leurs villes préférées.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Paramètre supérieur à

La `supersetOf` fonction est utilisée pour déterminer si un tableau spécifique (tableau A) est un superset d&#39;un autre tableau (tableau B). En d&#39;autres termes, ce tableau A contient tous les éléments du tableau B.

**Format**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Exemple**

La requête PQL suivante définit les personnes qui ont mangé au moins une fois des sushis et des pizzas.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Inclut

La `includes` fonction permet de déterminer si un tableau ou une liste contient un élément donné.

**Format**

```sql
{ARRAY}.includes({ITEM})
```

**Exemple**

La requête PQL suivante définit les personnes dont la couleur préférée est le rouge.

```sql
person.favoriteColors.includes("red")
```

## Distinct

La `distinct` fonction est utilisée pour supprimer des valeurs de duplicata d&#39;un tableau ou d&#39;une liste.

**Format**

```sql
{ARRAY}.distinct()
```

**Exemple**

La requête PQL suivante spécifie les personnes qui ont passé des commandes dans plusieurs magasins.

```sql
person.orders.storeId.distinct().count() > 1
```

## Regrouper par

La `groupBy` fonction est utilisée pour partitionner les valeurs d&#39;un tableau ou d&#39;une liste dans un groupe en fonction de la valeur de l&#39;expression.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou liste à regrouper. |
| `{EXPRESSION}` | expression qui mappe chaque élément du tableau ou de la liste renvoyé. |

**Exemple**

La requête PQL suivante regroupe toutes les commandes dans lesquelles la commande a été placée.

```sql
orders.groupBy(storeId)
```

## Filtrer

La `filter` fonction est utilisée pour filtrer un tableau ou une liste en fonction d&#39;une expression.

**Format**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou liste à filtrer. |
| `{EXPRESSION}` | expression par laquelle filtrer. |

**Exemple**

La requête PQL suivante définit toutes les personnes de 21 ans ou plus.

```sql
person.filter(age >= 21)
```

## Carte

La `map` fonction est utilisée pour créer un nouveau tableau en appliquant une expression à chaque élément d&#39;un tableau donné.

**Format**

```sql
array.map(expression)
```

**Exemple**

La requête PQL suivante crée un nouveau tableau de nombres et carré la valeur des nombres d’origine.

```sql
numbers.map(square)
```

## Premier `n` tableau

La `topN` fonction est utilisée pour renvoyer les premiers éléments `N` d&#39;un tableau, lorsqu&#39;ils sont triés par ordre croissant en fonction de l&#39;expression numérique donnée.

**Format**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou liste à trier. |
| `{VALUE}` | Propriété dans laquelle trier le tableau ou la liste. |
| `{AMOUNT}` | Nombre d’éléments à renvoyer. |

**Exemple**

La requête PQL suivante renvoie les cinq premières commandes au prix le plus élevé.

```sql
orders.topN(price, 5)
```

## Dernier `n` tableau

La `bottomN` fonction est utilisée pour renvoyer les derniers éléments `N` d&#39;un tableau, lorsqu&#39;ils sont triés par ordre croissant en fonction de l&#39;expression numérique donnée.

**Format**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Description |
| --------- | ----------- | 
| `{ARRAY}` | Tableau ou liste à trier. |
| `{VALUE}` | Propriété dans laquelle trier le tableau ou la liste. |
| `{AMOUNT}` | Nombre d’éléments à renvoyer. |

**Exemple**

La requête PQL suivante renvoie les cinq premières commandes ayant le prix le plus bas.

```sql
orders.bottomN(price, 5)
```

## Premier élément

La `head` fonction est utilisée pour renvoyer le premier élément du tableau ou de la liste.

**Format**

```sql
{ARRAY}.head()
```

**Exemple**

La requête PQL suivante renvoie la première des cinq premières commandes ayant le prix le plus élevé. Vous trouverez plus d&#39;informations sur la `topN` fonction dans la [première section `n` de la baie de disques](#first-n-in-array) .

```sql
orders.topN(price, 5).head()
```

## Étapes suivantes

Maintenant que vous avez pris connaissance de la baie, de la liste et des fonctions définies, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.

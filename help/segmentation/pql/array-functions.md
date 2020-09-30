---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;array functions;array;
solution: Experience Platform
title: Fonctions de tableau, de liste et d’ensemble
topic: developer guide
description: Le langage de requête de profil (PQL) offre des fonctions pour faciliter l’interaction avec des tableaux, des listes et des chaînes.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 96%

---


# Fonctions de tableau, de liste et d’ensemble

[!DNL Profile Query Language] (PQL) offre des fonctions pour faciliter l&#39;interaction avec les tableaux, les listes et les chaînes. More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

## In

La fonction `in` permet de déterminer si un élément est un membre d’un tableau ou d’une liste.

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

La fonction `notIn` permet de déterminer si un élément n’est pas un membre d’un tableau ou d’une liste.

>[!NOTE]
>
>La fonction `notIn` assure *également* qu’aucune valeur n’est nulle. Par conséquent, les résultats ne sont pas une négation exacte de la fonction `in`.

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

La fonction `intersects` permet de déterminer si deux tableaux ou deux listes ont au moins un membre commun.

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

La fonction `intersection` sert à déterminer les membres communs à deux tableaux ou deux listes.

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

La fonction `subsetOf` sert à déterminer si un tableau spécifique (tableau A) est un sous-ensemble d’un autre tableau (tableau B). En d’autres termes, elle permet de déterminer si tous les éléments du tableau A sont des éléments du tableau B.

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

La fonction `supersetOf` sert à déterminer si un tableau spécifique (tableau A) est un sur-ensemble d’un autre tableau (tableau B). En d’autres termes, elle permet de déterminer si le tableau A contient tous les éléments du tableau B.

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

La fonction `includes` permet de déterminer si un tableau ou une liste contient un élément donné.

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

La fonction `distinct` est utilisée pour supprimer les doublons d’un tableau ou d’une liste.

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

La fonction `groupBy` est utilisée pour partitionner les valeurs d’un tableau ou d’une liste dans un groupe, en fonction de la valeur de l’expression.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argument | Description |
| --------- | ----------- |
| `{ARRAY}` | Tableau ou liste à regrouper. |
| `{EXPRESSION}` | Expression qui mappe chaque élément du tableau ou de la liste renvoyée. |

**Exemple**

La requête PQL suivante regroupe toutes les commandes par boutique dans laquelle la commande a été placée.

```sql
orders.groupBy(storeId)
```

## Filtre

La fonction `filter` est utilisée pour filtrer un tableau ou une liste en fonction d’une expression.

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

La fonction `map` sert à créer un tableau en appliquant une expression à chaque élément d’un tableau donné.

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

La fonction `topN` est utilisée pour renvoyer les premiers éléments `N` d’un tableau, lorsqu’ils sont triés dans l’ordre croissant en fonction d’une expression numérique donnée.

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

## Last `n` in array

La fonction `bottomN` est utilisée pour renvoyer les derniers éléments `N` d’un tableau, lorsqu’ils sont triés dans l’ordre croissant en fonction d’une expression numérique donnée.

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

La requête PQL suivante renvoie les cinq premières commandes au prix le plus bas.

```sql
orders.bottomN(price, 5)
```

## First item

La fonction `head` est utilisée pour renvoyer le premier élément du tableau ou de la liste.

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

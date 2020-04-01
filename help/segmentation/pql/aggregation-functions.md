---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions d'agrégation
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Fonctions d&#39;agrégation

Les fonctions d’agrégation sont utilisées pour regrouper plusieurs valeurs dans des tableaux PQL (Language)  afin de former une seule valeur de résumé. Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Décompte

La `count` fonction renvoie le nombre d&#39;éléments dans le tableau donné.

**Format**

```sql
{ARRAY}.count()
```

**Exemple**

Le PQL suivant renvoie le nombre de commandes dans le tableau.

```sql
orders.count()
```

## Sum

La `sum` fonction renvoie la somme de toutes les valeurs sélectionnées dans le tableau.

**Format**

```sql
{ARRAY}.sum()
```

**Exemple**

Le PQL suivant renvoie la somme des prix de toutes les commandes.

```sql
orders.sum(order.price)
```

## Moyenne

La `average` fonction renvoie la moyenne arithmétique de toutes les valeurs sélectionnées dans le tableau.

**Format**

```sql
{ARRAY}.average()
```

**Exemple**

Le PQL suivant renvoie le prix moyen de toutes les commandes.

```sql
orders.average(order.price)
```

## Minimum

La `min` fonction renvoie la plus petite des valeurs sélectionnées dans le tableau.

**Format**

```sql
{ARRAY}.min()
```

**Exemple**

Le PQL suivant renvoie le prix le plus bas de toutes les commandes.

```sql
orders.min(order.price)
```

## Maximum

La `max` fonction renvoie la plus grande de toutes les valeurs sélectionnées dans le tableau.

**Format**

```sql
{ARRAY}.max()
```

**Exemple**

Le PQL suivant renvoie le prix le plus élevé de toutes les commandes.

```sql
orders.max(order.price)
```

## Étapes suivantes

Maintenant que vous avez appris les fonctions d’agrégation, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).

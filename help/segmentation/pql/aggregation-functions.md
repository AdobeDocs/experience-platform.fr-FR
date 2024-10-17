---
solution: Experience Platform
title: Fonctions d’agrégation PQL
description: Les fonctions d’agrégation sont utilisées pour regrouper plusieurs valeurs dans des tableaux Profile Query Language (PQL) afin de former une seule valeur de résumé.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 45%

---

# Fonctions d’agrégation

Les fonctions d’agrégation sont utilisées pour regrouper plusieurs valeurs dans des tableaux [!DNL Profile Query Language] (PQL) afin de former une seule valeur de résumé. Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Nombre

La fonction `count` renvoie le nombre d’éléments dans le tableau donné sous la forme d’un nombre.

**Format**

```sql
{ARRAY}.count()
```

**Exemple**

La requête PQL suivante renvoie le nombre de commandes du tableau.

```sql
orders.count()
```

## Sum

La fonction `sum` renvoie la somme de toutes les valeurs sélectionnées dans le tableau sous la forme d’un nombre.

**Format**

```sql
{ARRAY}.sum()
```

**Exemple**

La requête PQL suivante renvoie la somme des prix de toutes les commandes.

```sql
orders.sum(order.price)
```

## Average

La fonction `average` renvoie la moyenne arithmétique de toutes les valeurs sélectionnées dans le tableau sous la forme d’un nombre.

**Format**

```sql
{ARRAY}.average()
```

**Exemple**

La requête PQL suivante renvoie le prix moyen de toutes les commandes.

```sql
orders.average(order.price)
```

## Minimum

La fonction `min` renvoie la plus petite de toutes les valeurs sélectionnées dans le tableau sous la forme d’un nombre.

**Format**

```sql
{ARRAY}.min()
```

**Exemple**

La requête PQL suivante renvoie le prix le plus bas de toutes les commandes.

```sql
orders.min(order.price)
```

## Maximum

La fonction `max` renvoie la plus grande de toutes les valeurs sélectionnées dans le tableau sous la forme d’un nombre.

**Format**

```sql
{ARRAY}.max()
```

**Exemple**

La requête PQL suivante renvoie le prix le plus élevé de toutes les commandes.

```sql
orders.max(order.price)
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions d’agrégation, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).

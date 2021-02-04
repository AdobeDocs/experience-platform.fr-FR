---
keywords: Experience Platform;accueil;rubriques populaires;segmentation;Segmentation;Segmentation Service;pql;PQL;Profil Requête Language;agrégation fonctions;agrégation;
solution: Experience Platform
title: Fonctions d’agrégation
topic: developer guide
description: 'Fonctions d’agrégation sont utilisées pour regrouper plusieurs valeurs dans des tableaux PQL (Profil Requête Language) afin de former une seule valeur de synthèse. '
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 73%

---


# Fonctions d’agrégation

Fonctions d’agrégation sont utilisées pour regrouper plusieurs valeurs dans des tableaux [!DNL Profile Query Language] (PQL) afin de former une seule valeur de synthèse. Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans le [[!DNL Profile Query Language] overview](./overview.md).

## Count

La fonction `count` renvoie le nombre d’éléments dans le tableau donné.

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

La fonction `sum` renvoie la somme de toutes les valeurs sélectionnées dans le tableau.

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

La fonction `average` renvoie la moyenne arithmétique de toutes les valeurs sélectionnées dans le tableau.

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

La fonction `min` renvoie la plus petite de toutes les valeurs sélectionnées dans le tableau.

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

La fonction `max` renvoie la plus grande de toutes les valeurs sélectionnées dans le tableau.

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

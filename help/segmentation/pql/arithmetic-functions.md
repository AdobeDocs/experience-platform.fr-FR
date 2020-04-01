---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions arithmétiques
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Fonctions arithmétiques

Les fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur des valeurs dans le langage  de (PQL). Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Add (Ajouter)

La fonction `+` (addition) est utilisée pour rechercher la somme de deux arguments  .

**Format**

```sql
{NUMBER} + {NUMBER}
```

**Exemple**

Le PQL suivant  le prix de deux produits différents.

```sql
product1.price + product2.price
```

## Multiplier

La fonction `*` (multiplication) est utilisée pour rechercher le produit de deux arguments  .

**Format**

```sql
{NUMBER} * {NUMBER}
```

**Exemple**

Le PQL suivant trouve le produit de l&#39;inventaire et le prix d&#39;un produit pour trouver la valeur brute du produit.

```sql
product.inventory * product.price
```

## Soustraire

La fonction `-` (soustraction) permet de trouver la différence entre deux arguments  .

**Format**

```sql
{NUMBER} - {NUMBER}
```

**Exemple**

Le PQL ci-dessous trouve la différence de prix entre deux produits différents.

```sql
product1.price - product2.price
```

## Diviser

La fonction `/` (division) est utilisée pour trouver le quotient de deux arguments  .

**Format**

```sql
{NUMBER} / {NUMBER}
```

**Exemple**

Le PQL suivant trouve le quotient entre le total des produits vendus et le total des revenus gagnés pour déterminer le coût moyen par article.

```sql
totalProduct.price / totalProduct.sold
```

## Rappel

La fonction `%` (modulo/reste) est utilisée pour trouver le reste après la division des deux arguments  .

**Format**

```sql
{NUMBER} % {NUMBER}
```

**Exemple**

Le PQL suivant vérifie si l&#39;âge de la personne est divisible de cinq ans.

```sql
person.age % 5 = 0
```

## Étapes suivantes

Maintenant que vous avez appris les fonctions arithmétiques, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).

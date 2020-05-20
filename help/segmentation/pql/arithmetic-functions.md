---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions arithmétiques
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 5%

---


# Fonctions arithmétiques

Les fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur les valeurs dans le langage PQL (Profil Requête Language). Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## Add (Ajouter)

La fonction `+` (addition) est utilisée pour rechercher la somme de deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} + {NUMBER}
```

**Exemple**

La requête PQL suivante résume le prix de deux produits différents.

```sql
product1.price + product2.price
```

## Multiplier

La fonction `*` (multiplication) est utilisée pour trouver le produit de deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} * {NUMBER}
```

**Exemple**

La requête suivante de la LPQ recherche le produit de l&#39;inventaire et le prix d&#39;un produit pour déterminer la valeur brute du produit.

```sql
product.inventory * product.price
```

## Soustraire

La fonction `-` (soustraction) permet de trouver la différence entre deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} - {NUMBER}
```

**Exemple**

La requête PQL suivante identifie la différence de prix entre deux produits différents.

```sql
product1.price - product2.price
```

## Diviser

La fonction `/` (division) est utilisée pour trouver le quotient de deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} / {NUMBER}
```

**Exemple**

La requête suivante de PQL recherche le quotient entre le total des produits vendus et le total des sommes gagnées pour déterminer le coût moyen par article.

```sql
totalProduct.price / totalProduct.sold
```

## Reste

La fonction `%` (modulo/reste) est utilisée pour trouver le reste après la division des deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} % {NUMBER}
```

**Exemple**

La requête PQL suivante vérifie si l&#39;âge de la personne est divisible de cinq ans.

```sql
person.age % 5 = 0
```

## Étapes suivantes

Maintenant que vous avez appris les fonctions arithmétiques, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.

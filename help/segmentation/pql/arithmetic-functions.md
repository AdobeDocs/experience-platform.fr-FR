---
solution: Experience Platform
title: Fonctions arithmétiques PAL
description: Les fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur les valeurs dans Profile Query Language (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 82%

---

# Fonctions arithmétiques

Les fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur les valeurs dans [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Addition

La fonction `+` (addition) est utilisée pour trouver la somme de deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} + {NUMBER}
```

**Exemple**

La requête PQL suivante additionne le prix de deux produits différents.

```sql
product1.price + product2.price
```

## Multiplication

La fonction `*` (multiplication) est utilisée pour trouver le produit de deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} * {NUMBER}
```

**Exemple**

La requête PQL suivante trouve le produit de l’inventaire et du prix d’un produit pour obtenir la valeur brute du produit.

```sql
product.inventory * product.price
```

## Soustraction

La fonction `-` (soustraction) permet de trouver la différence entre deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} - {NUMBER}
```

**Exemple**

La requête PQL suivante trouve la différence de prix entre deux produits différents.

```sql
product1.price - product2.price
```

## Division

La fonction `/` (division) est utilisée pour trouver le quotient de deux expressions d&#39;argument.

**Format**

```sql
{NUMBER} / {NUMBER}
```

**Exemple**

La requête PQL suivante trouve le quotient entre le total des produits vendus et le total des revenus obtenus pour déterminer le coût moyen par article.

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

La requête PQL suivante vérifie si l’âge de la personne est divisible par cinq.

```sql
person.age % 5 = 0
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions arithmétiques, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).

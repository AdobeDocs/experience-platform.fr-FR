---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;arithmetic functions;arithmetic;
solution: Experience Platform
title: Fonctions arithmétiques
topic: developer guide
description: Fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur des valeurs dans le langage PQL (Profil Requête Language).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 85%

---


# Fonctions arithmétiques

Fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur les valeurs de [!DNL Profile Query Language] (PQL). More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

## Addition

La fonction `+` (addition) est utilisée pour trouver la somme de deux expressions d’argument.

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

La fonction `*` (multiplication) est utilisée pour trouver le produit de deux expressions d’argument.

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

La fonction `-` (soustraction) permet de trouver la différence entre deux expressions d’argument.

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

La fonction `/` (division) est utilisée pour trouver le quotient de deux expressions d’argument.

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

La fonction `%` (modulo/reste) est utilisée pour trouver le reste après la division des deux expressions d’argument.

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

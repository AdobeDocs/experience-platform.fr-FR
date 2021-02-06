---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; pql ; PQL ; Profil Requête Language ; fonctions arithmétiques ; arithmétique ;
solution: Experience Platform
title: Fonctions arithmétiques PAL
topic: developer guide
description: Les fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur des valeurs dans le langage de requête de profil (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 83%

---


# Fonctions arithmétiques

Fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur les valeurs de [!DNL Profile Query Language] (PQL). Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans le [[!DNL Profile Query Language] overview](./overview.md).

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

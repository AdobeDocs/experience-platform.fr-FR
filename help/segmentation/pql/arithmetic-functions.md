---
solution: Experience Platform
title: Fonctions arithmétiques PAL
description: Les fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur des valeurs dans Profile Query Language (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
TQID: https://experienceleague.adobe.com/aJnwR9-ZH5bTzU9VetyC8mIOnYvjzOBaK9V52XMvJc0
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 258
ht-degree: 51%

---

# Fonctions arithmétiques

Les fonctions arithmétiques sont utilisées pour effectuer des calculs de base sur des valeurs dans [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur d’autres fonctions de PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Ajouter

La fonction `+` (addition) est utilisée pour trouver la somme de deux expressions d&#39;argument sous forme de nombre.

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

La fonction `*` (multiplication) est utilisée pour trouver le produit de deux expressions d&#39;argument sous forme de nombre.

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

La fonction `-` (soustraction) est utilisée pour trouver la différence de deux expressions d&#39;argument sous forme de nombre.

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

La fonction `/` (division) est utilisée pour trouver le quotient de deux expressions d&#39;argument en tant que nombre.

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

La fonction `%` (modulo/reste) est utilisée pour trouver le reste après la division des deux expressions d&#39;argument en un nombre.

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

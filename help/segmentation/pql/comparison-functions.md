---
keywords: Experience Platform;accueil;rubriques populaires;segmentation;Segmentation;Segmentation Service;pql;PQL;Profil Requête Language;comparaison fonctions;comparaison ;
solution: Experience Platform
title: Fonctions de comparaison
topic: developer guide
description: Fonctions de comparaison sont utilisées pour comparer différentes expressions et valeurs, renvoyant "true" ou "false" en conséquence.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 86%

---


# Fonctions de comparaison

Les fonctions de comparaison sont utilisées pour comparer les différentes expressions et valeurs, renvoyant `true` ou `false` en conséquence. Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans le [[!DNL Profile Query Language] overview](./overview.md).

## Est égal à

La fonction `=` (est égal) vérifie si une valeur ou expression est égale à une autre valeur ou expression.

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**Exemple**

La requête PQL suivante vérifie si le pays de l’adresse du domicile est le Canada.

```sql
homeAddress.countryISO = "CA"
```

## Différent de

La fonction `!=` (différent de) vérifie si une valeur ou expression est **différente** d’une autre valeur ou expression.

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**Exemple**

La requête PQL suivante vérifie si le pays de l’adresse du domicile n’est pas le Canada.

```sql
homeAddress.countryISO != "CA"
```

## Supérieur à

La fonction `>` (supérieur à) permet de vérifier si la première valeur est supérieure à la seconde.

**Format**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire ne tombe ni en janvier ni en février.

```sql
person.birthMonth > 2
```

## Supérieur ou égal à

La fonction `>=` (supérieur ou égal à) permet de vérifier si la première valeur est supérieure ou égale à la seconde.

**Format**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire ne tombe ni en janvier ni en février.

```sql
person.birthMonth >= 3
```

## Inférieur à

La fonction `<` (inférieur à) permet de vérifier si la première valeur est inférieure à la seconde.

**Format**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire tombe en janvier.

```sql
person.birthMonth < 2
```

## Inférieur ou égal à

La fonction `<=` (inférieur ou égal à) permet de vérifier si la première valeur est inférieure ou égale à la seconde.

**Format**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire tombe en janvier ou en février.

```sql
person.birthMonth <= 2
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions de comparaison, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).

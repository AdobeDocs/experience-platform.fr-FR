---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de comparaison
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Fonctions de comparaison

Les fonctions de comparaison sont utilisées pour comparer les différents  et valeurs, renvoyant `true` ou `false` en conséquence. Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Est égal

La fonction `=` (est égal à) vérifie si une valeur ou   est égale à une autre valeur ou à un .

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**Exemple**

Le PQL suivant vérifie si le pays d’adresse d’origine est au Canada.

```sql
homeAddress.countryISO = "CA"
```

## Différent de

La fonction `!=` (différent) vérifie si une valeur ou   est **différente** d’une autre valeur ou d’un  de .

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**Exemple**

Le PQL suivant vérifie si le pays d’adresse d’origine n’est pas au Canada.

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

Le PQL suivant définit les personnes dont les anniversaires ne tombent ni en janvier ni en février.

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

Le PQL suivant définit les personnes dont les anniversaires ne tombent ni en janvier ni en février.

```sql
person.birthMonth >= 3
```

## Inférieur à

La fonction de comparaison `<` (inférieur à) permet de vérifier si la première valeur est inférieure à la seconde.

**Format**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Exemple**

Le PQL suivant définit les personnes dont l’anniversaire a lieu en janvier.

```sql
person.birthMonth < 2
```

## Inférieur ou égal à

La fonction de comparaison `<=` (inférieure ou égale à) permet de vérifier si la première valeur est inférieure ou égale à la seconde.

**Format**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Exemple**

Le PQL suivant définit les personnes dont l’anniversaire est en janvier ou février.

```sql
person.birthMonth <= 2
```

## Étapes suivantes

Maintenant que vous avez appris les fonctions de comparaison, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).

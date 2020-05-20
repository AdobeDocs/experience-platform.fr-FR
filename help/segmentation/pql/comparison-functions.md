---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de comparaison
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 10%

---


# Fonctions de comparaison

Les fonctions de comparaison sont utilisées pour comparer différentes expressions et valeurs, renvoyant `true` ou `false` en conséquence. Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## Est égal

La fonction `=` (est égal à) vérifie si une valeur ou une expression est égale à une autre valeur ou expression.

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**Exemple**

La requête PQL suivante vérifie si le pays d&#39;adresse d&#39;origine est au Canada.

```sql
homeAddress.countryISO = "CA"
```

## Différent de

La fonction `!=` (pas égale) vérifie si une valeur ou une expression **n’est pas** égale à une autre valeur ou expression.

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**Exemple**

La requête PQL suivante vérifie si le pays d&#39;adresse d&#39;origine n&#39;est pas au Canada.

```sql
homeAddress.countryISO != "CA"
```

## Supérieur à

La fonction `>` (supérieur à) est utilisée pour vérifier si la première valeur est supérieure à la seconde.

**Format**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont les anniversaires ne tombent pas en janvier ou février.

```sql
person.birthMonth > 2
```

## Supérieur ou égal à

La fonction `>=` (supérieure ou égale à) est utilisée pour vérifier si la première valeur est supérieure ou égale à la seconde.

**Format**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont les anniversaires ne tombent pas en janvier ou février.

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

La requête PQL suivante définit les personnes dont l&#39;anniversaire a lieu en janvier.

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

La requête PQL suivante définit les personnes dont l&#39;anniversaire est en janvier ou février.

```sql
person.birthMonth <= 2
```

## Étapes suivantes

Maintenant que vous avez pris connaissance des fonctions de comparaison, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.

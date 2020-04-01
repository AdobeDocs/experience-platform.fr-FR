---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions booléennes
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Fonctions booléennes

Les fonctions booléennes sont utilisées pour exécuter une logique booléenne sur différents éléments dans le langage  de (PQL).  Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Et

La `and` fonction sert à créer une conjonction logique.

**Format**

```sql
{QUERY} and {QUERY}
```

**Exemple**

Le suivant de la LPQ reviendra à toutes les personnes avec le pays d&#39;origine comme Canada et année de naissance de 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## OU

La `or` fonction est utilisée pour créer une disjonction logique.

**Format**

```sql
{QUERY} or {QUERY}
```

**Exemple**

Le suivant de la LPQ reviendra à toutes les personnes avec le pays d&#39;origine comme Canada ou année de naissance de 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Pas

La fonction `not` (ou `!`) est utilisée pour créer une négation logique.

**Format**

```sql
not ({QUERY})
!({QUERY})
```

**Exemple**

Le suivant de PQL  retournera tous ceux qui n&#39;ont pas leur pays d&#39;origine comme Canada.

```sql
not (homeAddress.countryISO = "CA")
```

## Si la variable

La `if` fonction est utilisée pour résoudre un   selon qu’une condition spécifiée est vraie ou non.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Description |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | booléen  qui est en cours de test. |
| `{TRUE_EXPRESSION}` |   dont la valeur sera utilisée si `{TEST_EXPRESSION}` est true. |
| `{FALSE_EXPRESSION}` | Le   dont la valeur sera utilisée si `{TEST_EXPRESSION}` est false. |

**Exemple**

Le de PQL suivant définit la valeur comme `1` si le pays d&#39;origine est le Canada et `2` si le pays d&#39;origine n&#39;est pas le Canada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Étapes suivantes

Maintenant que vous avez appris les fonctions booléennes, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).

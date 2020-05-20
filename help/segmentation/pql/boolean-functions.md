---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions booléennes
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 6%

---


# Fonctions booléennes

Les fonctions booléennes sont utilisées pour exécuter une logique booléenne sur différents éléments dans le langage PQL (Profil Requête Language).  Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## Et

La `and` fonction est utilisée pour créer une conjonction logique.

**Format**

```sql
{QUERY} and {QUERY}
```

**Exemple**

La requête suivante de la LPQ remettra à toutes les personnes ayant le pays d&#39;origine le Canada et l&#39;année de naissance de 1985.

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

La requête suivante de la LPQ remettra à toutes les personnes ayant le pays d&#39;origine le Canada ou l&#39;année de naissance de 1985.

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

La requête suivante de la LPQ rendra au Canada toutes les personnes qui n&#39;ont pas leur pays d&#39;origine.

```sql
not (homeAddress.countryISO = "CA")
```

## Si la variable

La `if` fonction est utilisée pour résoudre une expression selon si une condition spécifiée est vraie.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Description |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | expression booléenne qui est en cours de test. |
| `{TRUE_EXPRESSION}` | expression dont la valeur sera utilisée si `{TEST_EXPRESSION}` la valeur est true. |
| `{FALSE_EXPRESSION}` | expression dont la valeur sera utilisée si elle `{TEST_EXPRESSION}` est fausse. |

**Exemple**

La requête suivante de la LPQ établira la valeur comme `1` si le pays d&#39;origine est le Canada et `2` si le pays d&#39;origine n&#39;est pas le Canada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Étapes suivantes

Maintenant que vous connaissez les fonctions booléennes, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.

---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;boolean functions;boolean;
solution: Experience Platform
title: Fonctions booléennes
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 88%

---


# Fonctions booléennes

Boolean functions are used to perform boolean logic on different elements in [!DNL Profile Query Language] (PQL).  More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

## And

La fonction `and` sert à créer une conjonction logique.

**Format**

```sql
{QUERY} and {QUERY}
```

**Exemple**

La requête suivante PQL renverra toutes les personnes ayant pour pays d’origine le Canada et pour année de naissance 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Or

La fonction `or` est utilisée pour créer une disjonction logique.

**Format**

```sql
{QUERY} or {QUERY}
```

**Exemple**

La requête suivante PQL renverra toutes les personnes ayant pour pays d’origine le Canada ou pour année de naissance 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Not

La fonction `not` (ou `!`) est utilisée pour créer une négation logique.

**Format**

```sql
not ({QUERY})
!({QUERY})
```

**Exemple**

La requête suivante PQL renverra toutes les personnes qui n’ont pas pour pays d’origine le Canada.

```sql
not (homeAddress.countryISO = "CA")
```

## If

La fonction `if` est utilisée pour résoudre une expression selon qu’une condition spécifiée est vraie ou non.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Description |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | L’expression booléenne en cours de test. |
| `{TRUE_EXPRESSION}` | L’expression dont la valeur sera utilisée si `{TEST_EXPRESSION}` est vraie. |
| `{FALSE_EXPRESSION}` | L’expression dont la valeur sera utilisée si `{TEST_EXPRESSION}` est fausse. |

**Exemple**

La requête PQL suivante définit la valeur sur `1` si le pays d’origine est le Canada et sur `2` si le pays d’origine n’est pas le Canada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions booléennes, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).

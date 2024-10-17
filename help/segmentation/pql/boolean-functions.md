---
solution: Experience Platform
title: Fonctions booléennes PQL
description: Les fonctions booléennes sont utilisées pour exécuter une logique booléenne sur différents éléments dans Profile Query Language (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 64%

---

# Fonctions booléennes

Les fonctions booléennes sont utilisées pour exécuter une logique booléenne sur différents éléments dans [!DNL Profile Query Language] (PQL).  Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Et

La fonction `and` est utilisée pour créer une conjonction logique en tant que valeur booléenne.

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

La fonction `or` est utilisée pour créer une disjonction logique en tant que valeur booléenne.

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

La fonction `if` est utilisée pour résoudre une expression selon qu’une condition spécifiée est vraie ou non en tant que valeur booléenne.

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

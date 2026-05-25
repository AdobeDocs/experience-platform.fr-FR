---
solution: Experience Platform
title: Fonctions booléennes de PQL
description: Les fonctions booléennes sont utilisées pour exécuter une logique booléenne sur différents éléments dans Profile Query Language (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
TQID: https://experienceleague.adobe.com/WI-Px2TXL7OOALs-xl-nBlKMYrCadfSRuh6PEw-6TF0
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
source-wordcount: 248
ht-degree: 64%

---

# Fonctions booléennes

Les fonctions booléennes sont utilisées pour exécuter une logique booléenne sur différents éléments dans [!DNL Profile Query Language] (PQL).  Vous trouverez plus d’informations sur d’autres fonctions de PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Et

La fonction `and` est utilisée pour créer une conjonction logique sous la forme d’une valeur booléenne.

**Format**

```sql
{QUERY} and {QUERY}
```

**Exemple**

La requête suivante PQL renverra toutes les personnes ayant pour pays d’origine le Canada et pour année de naissance 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Ou

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

## Si

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

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Déclarations préparées
topic: prepared statements
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 8%

---


# Déclarations préparées

Dans SQL, les instructions préparées sont utilisées pour modéliser des requêtes ou des mises à jour similaires. Adobe Experience Platform Requête Service prend en charge les instructions préparées à l’aide d’une requête paramétrée. Vous pouvez l’utiliser pour optimiser les performances, car vous n’aurez plus besoin de réanalyser une requête encore et encore.

## Utilisation de déclarations préparées

Lorsque vous utilisez des instructions préparées, les syntaxes suivantes sont prises en charge :

- [PRÉPARATION](#prepare)
- [EXÉCUTER](#execute)
- [DÉALLOUER](#deallocate)

### Préparer une déclaration préparée {#prepare}

Cette requête SQL enregistre la requête SELECT écrite avec le nom donné comme `PLAN_NAME`. Vous pouvez utiliser des variables, par exemple `$1` au lieu de valeurs réelles. Cette déclaration préparée sera enregistrée pendant la session en cours. Veuillez noter que les noms des plans **ne sont pas** sensibles à la casse.

#### Format SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### Exemple de SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Exécuter une instruction préparée {#execute}

Cette requête SQL utilise l&#39;instruction préparée qui a été créée précédemment.

#### Format SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### Exemple de SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### Dédistribuer une instruction préparée {#deallocate}

Cette requête SQL est utilisée pour supprimer l&#39;instruction préparée nommée.

#### Format SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### Exemple de SQL

```sql
DEALLOCATE test;
```

## Exemple de flux utilisant des instructions préparées

Au départ, vous pouvez avoir une requête SQL, telle que celle ci-dessous :

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

La requête SQL ci-dessus renvoie la réponse suivante :

| id | firstname | lastname | date de naissance | email | city | pays |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoine | dubois | 1967-03-14 | example2@example.com | Paris | France |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Japon |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stockholm | Suède |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chili |

Cette requête SQL peut être paramétrée à l&#39;aide de l&#39;instruction préparée suivante :

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Désormais, l&#39;instruction préparée peut être exécutée à l&#39;aide de l&#39;appel suivant :

```sql
EXECUTE getIdRange(10000, 10005);
```

Lors de l’appel, les résultats sont identiques à ceux d’avant :

| id | firstname | lastname | date de naissance | email | city | pays |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoine | dubois | 1967-03-14 | example2@example.com | Paris | France |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Japon |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stockholm | Suède |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chili |

Une fois que vous avez fini d’utiliser l’instruction préparée, vous pouvez la délocaliser en utilisant l’appel suivant :

```sql
DEALLOCATE getIdRange;
```

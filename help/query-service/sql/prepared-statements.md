---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Déclarations préparées
topic: prepared statements
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Déclarations préparées

Dans SQL, les instructions préparées sont utilisées pour modéliser des  ou des mises à jour similaires. Le service de Adobe Experience Platform prend en charge les instructions préparées à l’aide d’un  de paramétré. Vous pouvez l’utiliser pour optimiser les performances, car vous n’aurez plus besoin de réanalyser un  encore et encore.

## Utilisation de déclarations préparées

Lorsque vous utilisez des instructions préparées, les syntaxes suivantes sont prises en charge :

- [PRÉPARER](#prepare)
- [EXÉCUTER](#execute)
- [DÉALLOCALISER](#deallocate)

### Préparer une déclaration préparée {#prepare}

Ce SQL enregistre le SELECT écrit  avec le nom donné comme `PLAN_NAME`. Vous pouvez utiliser des variables, telles que `$1` des valeurs réelles. Cette déclaration préparée sera enregistrée pendant la session en cours. Veuillez noter que les noms des plans **ne sont pas** sensibles à la casse.

#### Format SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### Exemple de code SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Exécuter une instruction préparée {#execute}

Ce SQL utilise l&#39;instruction préparée qui a été créée précédemment.

#### Format SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### Exemple de code SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### Déallouer une instruction préparée {#deallocate}

Ce SQL est utilisé pour supprimer l&#39;instruction préparée nommée.

#### Format SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### Exemple de code SQL

```sql
DEALLOCATE test;
```

## Exemple de flux à l’aide d’instructions préparées

Au départ, vous pouvez disposer d’un  SQL, tel que celui ci-dessous :

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

Le SQL ci-dessus renvoie la réponse suivante :

| id | firstname | lastname | date de naissance | email | city | pays |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoine | dubois | 1967-03-14 | example2@example.com | Paris | France |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Japon |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stockholm | Suède |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chili |

Ce SQL peut être paramétré à l&#39;aide de l&#39;instruction préparée suivante :

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Désormais, l’instruction préparée peut être exécutée à l’aide de l’appel suivant :

```sql
EXECUTE getIdRange(10000, 10005);
```

Lors de l’appel, les résultats sont exactement les mêmes que précédemment :

| id | firstname | lastname | date de naissance | email | city | pays |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoine | dubois | 1967-03-14 | example2@example.com | Paris | France |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Japon |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stockholm | Suède |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chili |

Une fois l’instruction préparée terminée, vous pouvez la délocaliser à l’aide de l’appel suivant :

```sql
DEALLOCATE getIdRange;
```

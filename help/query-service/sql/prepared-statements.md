---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;instructions préparées;préparé;sql;
solution: Experience Platform
title: Instructions préparées dans Query Service
description: Dans SQL, les instructions préparées sont utilisées pour modéliser des requêtes ou des mises à jour similaires. Adobe Experience Platform Query Service prend en charge les instructions préparées à l’aide d’une requête paramétrée.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
TQID: https://experienceleague.adobe.com/yWxTkcuUryzJnlBOR4llYpRo4tgepvRnOH-h22PNtvw
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 401
ht-degree: 79%

---

# Instructions préparées

Dans SQL, les instructions préparées sont utilisées pour modéliser des requêtes ou des mises à jour similaires. Adobe Experience Platform prend [!DNL Query Service] en charge les instructions préparées à l’aide d’une requête paramétrée. Cela peut optimiser les performances, car vous n’avez plus besoin d’analyser à nouveau une requête de manière répétitive.

## Utilisation d’instructions préparées

Lorsque vous utilisez des instructions préparées, les syntaxes suivantes sont prises en charge :

- [PREPARE](#prepare)
- [EXECUTE](#execute)
- [DEALLOCATE](#deallocate)

### Préparer une instruction préparée {#prepare}

Cette requête SQL enregistre la requête SELECT écrite avec le nom donné comme `PLAN_NAME`. Vous pouvez utiliser des variables, telles que `$1` au lieu de valeurs réelles. Cette instruction préparée sera enregistrée pendant la session en cours. Veuillez noter que les noms des formules **ne sont pas** sensibles à la casse.

#### Format SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### Exemple de code SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Exécuter une instruction préparée {#execute}

Cette requête SQL utilise l’instruction préparée qui a été créée précédemment.

#### Format SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### Exemple de code SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### Désallouer une instruction préparée {#deallocate}

Cette requête SQL est utilisée pour supprimer l’instruction préparée nommée.

#### Format SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### Exemple de code SQL

```sql
DEALLOCATE test;
```

## Flux d’exemples d’utilisation d’instructions préparées

Au départ, vous pouvez disposer d’une requête SQL, telle que ci-dessous :

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

La requête SQL ci-dessus renvoie la réponse suivante :

| identifiant | prénom | nom | date de naissance | E-mail | ville | pays |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 15/09/1993 | exemple@exemple.com | Vancouver | Canada |
| 10001 | antoine | dubois | 14/03/1967 | exemple2@exemple.com | Paris | France |
| 10002 | kyoko | sakura | 26/11/1999 | exemple3@exemple.com | Tokyo | Japon |
| 10003 | linus | pettersson | 03/06/1982 | exemple4@exemple.com | Stockholm | Suède |
| 10004 | aasir | waithaka | 17/12/1976 | exemple5@exemple.com | Nairobi | Kenya |
| 10005 | fernando | rios | 30/07/2002 | exemple6@exemple.com | Santiago | Chili |

Cette requête SQL peut être paramétrée à l’aide de l’instruction préparée suivante :

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Désormais, l’instruction préparée peut être exécutée à l’aide de l’appel suivant :

```sql
EXECUTE getIdRange(10000, 10005);
```

Lors de l’appel, les résultats sont exactement les mêmes que précédemment :

| identifiant | prénom | nom | date de naissance | E-mail | ville | pays |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 15/09/1993 | exemple@exemple.com | Vancouver | Canada |
| 10001 | antoine | dubois | 14/03/1967 | exemple2@exemple.com | Paris | France |
| 10002 | kyoko | sakura | 26/11/1999 | exemple3@exemple.com | Tokyo | Japon |
| 10003 | linus | pettersson | 03/06/1982 | exemple4@exemple.com | Stockholm | Suède |
| 10004 | aasir | waithaka | 17/12/1976 | exemple5@exemple.com | Nairobi | Kenya |
| 10005 | fernando | rios | 30/07/2002 | exemple6@exemple.com | Santiago | Chili |

Une fois l’instruction préparée terminée, vous pouvez procéder à sa désallocation à l’aide de l’appel suivant :

```sql
DEALLOCATE getIdRange;
```

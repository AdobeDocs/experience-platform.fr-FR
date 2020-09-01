---
keywords: Experience Platform;home;popular topics;query service;Query service;writing queries;writing query;
solution: Experience Platform
title: Rédaction de requêtes
topic: queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 78%

---


# General guidance for query execution in [!DNL Query Service]

Ce document détaille les informations importantes à connaître pour la rédaction de requêtes dans Adobe Experience Platform [!DNL Query Service].

For detailed information on the SQL syntax used in [!DNL Query Service], please read the [SQL syntax documentation](../sql/syntax.md).

## Modèles d’exécution de requêtes

Adobe Experience Platform [!DNL Query Service] has two models of query execution: interactive and non-interactive. L’exécution interactive est utilisée pour le développement de requêtes et la génération de rapports dans les outils de Business Intelligence, tandis que l’exécution non interactive est utilisée pour les tâches plus importantes et les requêtes opérationnelles dans le cadre d’un workflow de traitement des données.

### Exécution de requête interactive

Queries can be executed interactively by submitting them through the [!DNL Query Service] UI or [through a connected client](../clients/overview.md). When running [!DNL Query Service] through a connected client, an active session runs between the client and [!DNL Query Service] until either the submitted query returns or times out.

L’exécution de requête interactive présente les limites suivantes :

| Paramètre | Limite |
| --------- | ---------- |
| Délai d’expiration de la requête | 10 minutes |
| Nombre maximal de lignes renvoyées | 50 000 |
| Nombre maximal de requêtes simultanées | 5 |

>[!NOTE]
>
>Pour contourner la limite de lignes maximale, incluez `LIMIT 0` dans votre requête. Le délai d’expiration de 10 minutes s’applique toujours.

Par défaut, les résultats des requêtes interactives sont renvoyés au client et **ne sont pas** conservés. In order to persist the results as a dataset in [!DNL Experience Platform], the query must use the `CREATE TABLE AS SELECT` syntax.

### Exécution de requête non interactive

Queries submitted through the [!DNL Query Service] API are run non-interactively. Non-interactive execution means that [!DNL Query Service] receives the API call and executes the query in the order it is received. Non-interactive queries always result in either the generation of a new dataset in [!DNL Experience Platform] to receive the results, or the insertion of new rows into an existing dataset.

## Accès à un champ spécifique dans un objet

Pour accéder à un champ dans un objet de votre requête, vous pouvez utiliser soit la notation par points (`.`), soit la notation par crochets (`[]`). L’instruction SQL suivante utilise la notation par points pour parcourir l’objet `endUserIds` jusqu’à l’objet `mcid`.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriété | Description |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nom de votre tableau d’analyse. |

L’instruction SQL suivante utilise la notation par crochets pour parcourir l’objet `endUserIds` jusqu’à l’objet `mcid`.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriété | Description |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nom de votre tableau d’analyse. |

>[!NOTE]
>
>Puisque chaque type de notation renvoie les mêmes résultats, celui que vous choisissez d’utiliser est à votre convenance.

Les deux exemples de requête ci-dessus renvoient un objet aplati, plutôt qu’une seule valeur :

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

L’objet `endUserIds._experience.mcid` renvoyé contient les valeurs correspondantes pour les paramètres suivants :

- `id`
- `namespace`
- `primary`

Lorsque la colonne est déclarée uniquement à l’objet, elle renvoie l’objet entier sous forme de chaîne. Pour afficher uniquement l’identifiant, utilisez :

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Utilisation des guillemets simples, des guillemets doubles ou des accents graves

Cette section explique à quel moment utiliser des guillemets simples, des guillemets doubles et des accents graves.

### Guillemets simples

Le guillemet simple (`'`) est utilisé pour créer des chaînes de texte. Par exemple, il peut être utilisé dans l’instruction `SELECT` pour renvoyer une valeur de texte statique dans le résultat, et dans la clause `WHERE` pour évaluer le contenu d’une colonne.

La requête suivante déclare une valeur de texte statique (`'datasetA'`) pour une colonne :

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

La requête suivante utilise une chaîne entre guillemets simples (`'homepage'`) dans sa clause WHERE pour renvoyer des événements pour une page spécifique.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Guillemets doubles

Le guillemet double (`"`) est utilisé pour déclarer un identifiant avec des espaces.

La requête suivante utilise des guillemets doubles pour renvoyer des valeurs de colonnes spécifiées lorsqu’une colonne contient une espace dans son identifiant :

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Les guillemets doubles **ne peuvent pas** être utilisés avec l’accès au champ avec notation par points.

### Accents graves

L’accent grave `` ` `` permet d’ignorer les noms de colonne réservés **uniquement** avec l’utilisation de la syntaxe de notation par points. Par exemple, comme `order` est un mot réservé dans SQL, vous devez utiliser des accents graves pour accéder au champ `commerce.order` :

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Les accents graves sont également utilisés pour accéder à un champ qui commence avec un nombre. Par exemple, pour accéder au champ `30_day_value`, vous devez utiliser la notation avec accents graves.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Les accents graves **ne sont pas** nécessaires si vous utilisez la notation par crochets.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Étapes suivantes

La lecture de ce document vous a permis de vous initier à certaines considérations importantes lors de la rédaction d’une requête avec [!DNL Query Service]. Pour plus d’informations sur l’utilisation de la syntaxe SQL pour la rédaction de vos propres requêtes, veuillez lire la [documentation sur la syntaxe SQL](../sql/syntax.md).
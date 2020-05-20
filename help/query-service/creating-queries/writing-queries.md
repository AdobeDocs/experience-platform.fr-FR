---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ecriture de requêtes
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 1%

---


# Directives générales pour l&#39;exécution des requêtes dans le Service des Requêtes

Ce document détaille les détails importants à connaître lors de l’écriture de requêtes dans Adobe Experience Platform Requête Service.

Pour plus d&#39;informations sur la syntaxe SQL utilisée dans Requête Service, consultez la documentation [sur la syntaxe](../sql/syntax.md)SQL.

## Modèles d’exécution de Requête

Adobe Experience Platform Requête Service comporte deux modèles d’exécution de requête : interactif et non interactif. L’exécution interactive est utilisée pour le développement de requêtes et la génération de rapports dans les outils de veille stratégique, tandis que l’exécution non interactive est utilisée pour les tâches plus importantes et les requêtes opérationnelles dans le cadre d’un processus de traitement des données.

### Exécution de requête interactive

Les Requêtes peuvent être exécutées de manière interactive en les envoyant via l’interface utilisateur de Requête Service ou [via un client](../clients/overview.md)connecté. Lors de l’exécution de Requête Service par l’intermédiaire d’un client connecté, une session active s’exécute entre le client et Requête Service jusqu’à ce que la requête envoyée soit renvoyée ou expire.

L’exécution de requête interactive présente les limites suivantes :

| Paramètre | Limite |
| --------- | ---------- |
| Délai d’expiration de la Requête | 10 minutes |
| Nombre maximal de lignes renvoyées | 50,000 |
| Nombre maximal de requêtes simultanées | 5 |

>[!NOTE] Pour remplacer la limite de lignes maximale, incluez `LIMIT 0` dans votre requête. Le délai de requête de 10 minutes s’applique toujours.

Par défaut, les résultats des requêtes interactives sont renvoyés au client et **ne sont pas** conservés. Pour conserver les résultats en tant que jeu de données dans la plateforme d’expérience, la requête doit utiliser la `CREATE TABLE AS SELECT` syntaxe.

### Exécution de requêtes non interactives

Les Requêtes envoyées via l’API Requête Service sont exécutées de manière non interactive. L’exécution non interactive signifie que Requête Service reçoit l’appel d’API et exécute la requête dans l’ordre dans lequel elle est reçue. Les requêtes non interactives entraînent toujours la génération d’un nouveau jeu de données dans la plateforme d’expérience pour recevoir les résultats ou l’insertion de nouvelles lignes dans un jeu de données existant.

## Accès à un champ spécifique dans un objet

Pour accéder à un champ d’un objet dans votre requête, vous pouvez utiliser soit la notation point (`.`), soit la notation crochet (`[]`). L&#39;instruction SQL suivante utilise la notation point pour traverser l&#39; `endUserIds` objet jusqu&#39;à l&#39; `mcid` objet.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriété | Description |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nom de votre tableau d’analyses. |

L&#39;instruction SQL suivante utilise la notation crochet pour traverser l&#39; `endUserIds` objet vers le bas jusqu&#39;à l&#39; `mcid` objet.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriété | Description |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nom de votre tableau d’analyses. |

>[!NOTE] Puisque chaque type de notation renvoie les mêmes résultats, celui que vous choisissez d’utiliser est à votre convenance.

Les deux exemples de requêtes ci-dessus renvoient un objet aplati, plutôt qu’une seule valeur :

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

L’objet renvoyé `endUserIds._experience.mcid` contient les valeurs correspondantes pour les paramètres suivants :

- `id`
- `namespace`
- `primary`

Lorsque la colonne est déclarée uniquement à l’objet, elle renvoie l’objet entier sous la forme d’une chaîne. Pour ne vue que l’identifiant, utilisez :

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

## Utilisation de guillemets simples, de guillemets de doublon et de guillemets arrière

Cette section explique quand utiliser des guillemets simples, des guillemets de doublon et des guillemets arrière dans les requêtes.

### Guillemets simples

Le guillemet simple (`'`) est utilisé pour créer des chaînes de texte. Par exemple, il peut être utilisé dans l’ `SELECT` instruction pour renvoyer une valeur de texte statique dans le résultat et dans la `WHERE` clause pour évaluer le contenu d’une colonne.

La requête suivante déclare une valeur de texte statique (`'datasetA'`) pour une colonne :

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

### Guillemets de Doublon

Le guillemet doublon (`"`) est utilisé pour déclarer un identifiant avec des espaces.

La requête suivante utilise des guillemets de doublon pour renvoyer des valeurs de colonnes spécifiées lorsqu’une colonne contient un espace dans son identifiant :

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

>[!NOTE] Les guillemets de Doublon **ne peuvent pas** être utilisés avec l’accès au champ de notation par point.

### Guillemets arrière

Le guillemet arrière `` ` `` est utilisé pour enregistrer les noms de colonnes réservés **uniquement** lors de l’utilisation de la syntaxe de notation par point. Par exemple, comme `order` il s’agit d’un mot réservé dans SQL, vous devez utiliser des guillemets arrière pour accéder au champ `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Les guillemets arrière sont également utilisés pour accéder à un champ qui début avec un nombre. Par exemple, pour accéder au champ `30_day_value`, vous devez utiliser la notation de guillemet arrière.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Les guillemets arrière **ne sont pas** nécessaires si vous utilisez la notation entre crochets.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Étapes suivantes

En lisant ce document, vous avez pris connaissance de certaines considérations importantes lors de l&#39;écriture de requêtes à l&#39;aide de Requête Service. Pour plus d&#39;informations sur l&#39;utilisation de la syntaxe SQL pour écrire vos propres requêtes, consultez la documentation [sur la syntaxe](../sql/syntax.md)SQL.
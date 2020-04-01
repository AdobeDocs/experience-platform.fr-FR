---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ecriture de
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Directives générales pour l&#39;exécution des  par les dans le service 

Ce  des détails importants à connaître lors de l’écriture de  de dans Adobe Experience Platform  Service.

Pour plus d&#39;informations sur la syntaxe SQL utilisée dans le service , veuillez lire la documentation [sur la syntaxe](../sql/syntax.md)SQL.

## Modèles d’exécution de 

Le service de Adobe Experience Platform  deux modèles d’exécution de  : interactive et non interactive. L’exécution interactive est utilisée pour le développement de  de et la génération de rapports dans les outils de Business Intelligence, tandis que l’exécution non interactive est utilisée pour les tâches plus importantes et les  opérationnelles dans le cadre d’un processus de traitement des données.

### Exécution de  de interactif

Les  de peuvent être exécutées de manière interactive en les envoyant via l’interface utilisateur de  Service ou [via un client](../clients/overview.md)connecté. Lors de l’exécution du service  par l’intermédiaire d’un client connecté, une session active s’exécute entre le client et le service  jusqu’à ce que leservice envoyé soit renvoyé, soit expire.

L’exécution de  interactif présente les limites suivantes :

| Paramètre | Limite |
| --------- | ---------- |
| Délai d’ | 10 minutes |
| Nombre maximal de lignes renvoyées | 50,000 |
|  de simultané maximum | 5 |

>[!NOTE] Pour contourner la limite de lignes maximale, incluez `LIMIT 0` dans votre  de. Le délai d’ de 10 minutes s’applique toujours.

Par défaut, les résultats des  interactives sont renvoyés au client et **ne sont pas** conservés. Pour conserver les résultats sous forme d’un jeu de données dans la plateforme d’expérience, le doit utiliser la `CREATE TABLE AS SELECT` syntaxe.

### Exécution de  non interactives

Les  envoyées par le biais de l’API du service  sont exécutées de manière non interactive. L’exécution non interactive signifie que le service  reçoit l’appel d’API et exécute le  dans l’ordre dans lequel il est reçu. Les  non interactives entraînent toujours la génération d’un nouveau jeu de données dans la plateforme d’expérience pour recevoir les résultats ou l’insertion de nouvelles lignes dans un jeu de données existant.

## Accès à un champ spécifique dans un objet

Pour accéder à un champ d’un objet dans votre  de, vous pouvez utiliser soit la notation par point (`.`), soit la notation par crochet (`[]`). L’instruction SQL suivante utilise la notation point pour parcourir l’ `endUserIds` objet jusqu’à l’ `mcid` objet.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriété | Description |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nom de votre tableau d’analyse. |

L’instruction SQL suivante utilise la notation entre crochets pour parcourir l’ `endUserIds` objet jusqu’à l’ `mcid` objet.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriété | Description |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nom de votre tableau d’analyse. |

>[!NOTE] Puisque chaque type de notation renvoie les mêmes résultats, celui que vous choisissez d’utiliser est à votre convenance.

Les deux exemples de ci-dessus renvoient un objet aplati, plutôt qu’une seule valeur :

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

L’ `endUserIds._experience.mcid` objet renvoyé contient les valeurs correspondantes pour les paramètres suivants :

- `id`
- `namespace`
- `primary`

Lorsque la colonne est déclarée uniquement à l’objet, elle renvoie l’objet entier sous forme de chaîne. Pour  uniquement l’ID, utilisez :

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

## Quand utiliser des guillemets simples, des guillemets  et des guillemets arrière

Cette section explique à quel moment utiliser des guillemets simples, des guillemets  et des guillemets arrière dans les .

### Guillemets simples

Le guillemet simple (`'`) est utilisé pour créer des chaînes de texte. Par exemple, il peut être utilisé dans l’ `SELECT` instruction pour renvoyer une valeur de texte statique dans le résultat, et dans la `WHERE` clause pour évaluer le contenu d’une colonne.

Le suivant déclare une valeur de texte statique (`'datasetA'`) pour une colonne :

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Le suivant utilise une chaîne entre guillemets simples (`'homepage'`) dans sa clause WHERE pour renvoyer des  de pour une page spécifique.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

###  de

Le  guillemet (`"`) est utilisé pour déclarer un identifiant avec des espaces.

Le suivant utilise des guillemets  pour renvoyer des valeurs de colonnes spécifiées lorsqu’une colonne contient un espace dans son identificateur :

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

>[!NOTE] Les guillemets  **ne peuvent pas** être utilisés avec l’accès au champ de notation par point.

### Guillemets arrière

Le guillemet arrière `` ` `` permet d’ignorer les noms de colonne réservés **uniquement** lors de l’utilisation de la syntaxe de notation par point. Par exemple, comme `order` il s’agit d’un mot réservé dans SQL, vous devez utiliser des guillemets arrière pour accéder au champ `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Les guillemets arrière sont également utilisés pour accéder à un champ qui  avec un nombre. Par exemple, pour accéder au champ `30_day_value`, vous devez utiliser la notation de guillemet arrière.

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

En lisant ce , vous avez été initié à certaines considérations importantes lors de l&#39;écriture de  à l&#39;aide du service de. Pour plus d&#39;informations sur l&#39;utilisation de la syntaxe SQL pour écrire votre propre  de, veuillez lire la documentation [sur la syntaxe](../sql/syntax.md)SQL.
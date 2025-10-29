---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;écriture de requêtes;écriture de requête;
solution: Experience Platform
title: Directives générales pour l’exécution de requêtes dans Query Service
type: Tutorial
description: Ce document décrit les détails importants à connaître lors de la rédaction de requêtes dans Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 40%

---

# Directives générales pour l’exécution des requêtes dans [!DNL Query Service]

Ce document détaille les informations importantes à connaître lors de la rédaction de requêtes dans Adobe Experience Platform [!DNL Query Service].

Pour plus d’informations sur la syntaxe SQL utilisée dans [!DNL Query Service], consultez la documentation sur la syntaxe [SQL](../sql/syntax.md).

## Modèles d’exécution de requêtes

Adobe Experience Platform [!DNL Query Service] propose deux modes d’exécution des requêtes : interactive et non interactive. L’exécution interactive est utilisée pour le développement de requêtes et la génération de rapports dans les outils de Business Intelligence, tandis que l’exécution non interactive est utilisée pour les tâches plus importantes et les requêtes opérationnelles dans le cadre d’un workflow de traitement des données.

### Exécution de requête interactive

Les requêtes peuvent être exécutées de manière interactive en les envoyant via l’interface utilisateur [!DNL Query Service] ou [via un client connecté](../clients/overview.md). Lors de l’exécution de [!DNL Query Service] via un client connecté, une session active s’exécute entre le client et [!DNL Query Service] jusqu’à ce que la requête envoyée soit renvoyée ou qu’elle expire.

L’exécution de requête interactive présente les limites suivantes :

| Paramètre | Limite |
| --------- | ---------- |
| Délai d’expiration de la requête | 10 minutes |
| Nombre maximal de lignes renvoyées | 50 000 |
| Nombre maximal de requêtes simultanées | 5 |

>[!NOTE]
>
>Pour remplacer la limitation du nombre maximal de lignes, incluez `LIMIT 0` dans votre requête. Le délai d’expiration de 10 minutes s’applique toujours.

Par défaut, les résultats des requêtes interactives sont renvoyés au client et **ne sont pas** conservés. Pour conserver les résultats sous forme d’un jeu de données dans [!DNL Experience Platform], la requête doit utiliser la syntaxe `CREATE TABLE AS SELECT`.

### Exécution de requête non interactive

Les requêtes envoyées via l’API [!DNL Query Service] sont exécutées de manière non interactive. L’exécution non interactive signifie que [!DNL Query Service] reçoit l’appel API et exécute la requête dans l’ordre dans lequel elle est reçue. Les requêtes non interactives entraînent toujours la génération d’un nouveau jeu de données en [!DNL Experience Platform] de recevoir les résultats, ou l’insertion de nouvelles lignes dans un jeu de données existant.

## Accès à un champ spécifique dans un objet

Pour accéder à un champ dans un objet de votre requête, vous pouvez utiliser soit la notation par points (`.`), soit la notation par crochets (`[]`). L’instruction SQL suivante utilise la notation par points pour parcourir l’objet `endUserIds` jusqu’à l’objet `mcid`.

>[!NOTE]
>
>L’Experience Cloud ID (ECID) est également appelé MCID et continue à être utilisé dans les espaces de noms.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Propriété | Description |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nom de votre tableau d’analyse. |

>[!NOTE]
>
>Comme chaque type de notation renvoie les mêmes résultats, celui que vous choisissez d’utiliser dépend de vos préférences.

Les deux exemples de requête ci-dessus renvoient un objet aplati, plutôt qu’une seule valeur :

```console
              endUserIds._experience.mcid   
|--------------------------------------------------------
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
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
|----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Citations

Les guillemets simples, les guillemets doubles et les guillemets inverses ont des utilisations différentes dans les requêtes Query Service.

### Guillemets simples

Le guillemet simple (`'`) est utilisé pour créer des chaînes de texte. Par exemple, il peut être utilisé dans l’instruction `SELECT` pour renvoyer une valeur de texte statique dans le résultat, et dans la clause `WHERE` pour évaluer le contenu d’une colonne.

La requête suivante déclare une valeur de texte statique (`'datasetA'`) pour une colonne :

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

La requête suivante utilise une chaîne entre guillemets simples (`'homepage'`) dans sa clause WHERE pour renvoyer des événements pour une page spécifique.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
>Les guillemets doubles **impossible** peuvent être utilisés avec l’accès aux champs de notation par points.

### Accents graves

L’accent grave `` ` `` permet d’ignorer les noms de colonne réservés **uniquement** avec l’utilisation de la syntaxe de notation par points. Par exemple, comme `order` est un mot réservé dans SQL, vous devez utiliser des accents graves pour accéder au champ `commerce.order` :

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Les accents graves sont également utilisés pour accéder à un champ qui commence avec un nombre. Par exemple, pour accéder au champ `30_day_value`, vous devez utiliser la notation avec accents graves.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Les accents graves **ne sont pas** nécessaires si vous utilisez la notation par crochets.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Affichage des informations du tableau

Après vous être connecté à Query Service, vous pouvez afficher tous les tableaux disponibles sur Experience Platform à l’aide des commandes `\d` ou `SHOW TABLES`.

### Mode Tableau standard

La commande `\d` affiche la vue [!DNL PostgreSQL] standard pour répertorier les tableaux. Vous trouverez ci-dessous un exemple de sortie de cette commande :

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
|--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Vue détaillée du tableau

`SHOW TABLES` commande est une commande personnalisée qui fournit des informations plus détaillées sur les tableaux. Vous trouverez ci-dessous un exemple de sortie de cette commande :

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
|-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Informations sur le schéma

Pour afficher des informations plus détaillées sur les schémas du tableau, vous pouvez utiliser la commande `\d {TABLE_NAME}`, où `{TABLE_NAME}` est le nom du tableau dont vous souhaitez afficher les informations de schéma.

L’exemple suivant illustre les informations de schéma de la table `luma_midvalues`, qui s’affichent à l’aide de `\d luma_midvalues` :

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
|-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

De plus, vous pouvez obtenir des informations supplémentaires sur une colonne spécifique en ajoutant le nom de la colonne au nom du tableau. Cela serait écrit dans le format `\d {TABLE_NAME}_{COLUMN}`.

L’exemple suivant montre des informations supplémentaires pour la colonne `web` et sera appelé à l’aide de la commande suivante : `\d luma_midvalues_web` :

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
|----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Association de jeux de données

Vous pouvez joindre plusieurs jeux de données pour inclure des données provenant d’autres jeux de données dans votre requête.

L’exemple suivant joint les deux jeux de données suivants (`your_analytics_table` et `custom_operating_system_lookup`) et crée une instruction `SELECT` pour les 50 premiers systèmes d’exploitation en fonction du nombre de pages vues.

**Requête**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Résultats**

| Système d’exploitation | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
| Windows Vista | 173566,0 |
| Mobile iOS 6.1.3 | 119069,0 |
| Linux | 56516,0 |
| OSX 10.6.8 | 53652,0 |
| Android 4.0.4 | 46167,0 |
| Android 4.0.3 | 31852,0 |
| Windows Server 2003 et XP Édition x64 | 28883,0 |
| Android 4.1.1 | 24336,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 13357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Déduplication

Query Service prend en charge la déduplication des données ou la suppression des lignes en double des données. Pour plus d’informations sur la déduplication, consultez le [guide de déduplication de Query Service](../key-concepts/deduplication.md).

## Calculs de fuseau horaire dans Query Service

Query Service normalise les données persistantes dans Adobe Experience Platform à l’aide du format d’horodatage UTC. Pour plus d’informations sur la traduction de vos exigences en matière de fuseau horaire vers et depuis un horodatage UTC, reportez-vous à la section [FAQ sur la modification du fuseau horaire en et depuis un horodatage UTC](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Étapes suivantes

En lisant ce document, vous avez pris connaissance de certaines considérations importantes lors de la rédaction de requêtes à l’aide de [!DNL Query Service]. Pour plus d’informations sur l’utilisation de la syntaxe SQL pour la rédaction de vos propres requêtes, veuillez lire la [documentation sur la syntaxe SQL](../sql/syntax.md).

Pour plus d’exemples de requêtes pouvant être utilisées dans Query Service, veuillez lire la documentation de cas d’utilisation suivante :

- [Informations sur Analytics](../use-cases/analytics-insights.md)
- [Créer un rapport de tendance d’événements](../use-cases/trended-report-of-events.md)
- [Afficher un rapport de cumul d’un visiteur ou d’une visiteuse](../use-cases/roll-up-report-of-a-visitor.md)
- [Répertorier les pages vues d’un utilisateur ou d’une utilisatrice](../use-cases/list-visitor-sessions.md)
- [Répertorier les visiteurs et visiteuses selon leur nombre de pages vues](../use-cases/visitors-by-number-of-page-views.md)

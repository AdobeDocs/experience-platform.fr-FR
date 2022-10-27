---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;service de requête;écriture de requêtes;écriture de requêtes;
solution: Experience Platform
title: Directives générales pour l’exécution de requête dans Query Service
topic-legacy: queries
type: Tutorial
description: Ce document présente les détails importants à connaître lors de l’écriture de requêtes dans Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 47%

---

# Instructions générales pour l’exécution de requêtes dans [!DNL Query Service]

Ce document détaille les informations importantes à connaître pour la rédaction de requêtes dans Adobe Experience Platform [!DNL Query Service].

Pour plus d’informations sur la syntaxe SQL utilisée dans [!DNL Query Service], veuillez lire la [Documentation sur la syntaxe SQL](../sql/syntax.md).

## Modèles d’exécution de requêtes

Adobe Experience Platform [!DNL Query Service] comporte deux modèles d’exécution de requête : interactive et non interactive. L’exécution interactive est utilisée pour le développement de requêtes et la génération de rapports dans les outils de Business Intelligence, tandis que l’exécution non interactive est utilisée pour les tâches plus importantes et les requêtes opérationnelles dans le cadre d’un workflow de traitement des données.

### Exécution de requête interactive

Les requêtes peuvent être exécutées de manière interactive en les envoyant via l’ [!DNL Query Service] Interface utilisateur ou [par l’intermédiaire d’un client connecté](../clients/overview.md). En cours d’exécution [!DNL Query Service] via un client connecté, une session principale s’exécute entre le client et [!DNL Query Service] jusqu’à ce que la requête envoyée soit renvoyée ou expire.

L’exécution de requête interactive présente les limites suivantes :

| Paramètre | Limite |
| --------- | ---------- |
| Délai d’expiration de la requête | 10 minutes |
| Nombre maximal de lignes renvoyées | 50 000 |
| Nombre maximal de requêtes simultanées | 5 |

>[!NOTE]
>
>Pour contourner la limite de lignes maximale, incluez `LIMIT 0` dans votre requête. Le délai d’expiration de 10 minutes s’applique toujours.

Par défaut, les résultats des requêtes interactives sont renvoyés au client et **ne sont pas** conservés. Pour conserver les résultats sous la forme d’un jeu de données dans [!DNL Experience Platform], la requête doit utiliser la variable `CREATE TABLE AS SELECT` syntaxe.

### Exécution de requête non interactive

Requêtes envoyées via [!DNL Query Service] Les API sont exécutées de manière non interactive. L’exécution non interactive signifie que [!DNL Query Service] reçoit l’appel API et exécute la requête dans l’ordre dans lequel elle est reçue. Les requêtes non interactives entraînent toujours la génération d’un nouveau jeu de données dans [!DNL Experience Platform] pour recevoir les résultats ou l’insertion de nouvelles lignes dans un jeu de données existant.

## Accès à un champ spécifique dans un objet

Pour accéder à un champ dans un objet de votre requête, vous pouvez utiliser soit la notation par points (`.`), soit la notation par crochets (`[]`). L’instruction SQL suivante utilise la notation par points pour parcourir l’objet `endUserIds` jusqu’à l’objet `mcid`.

>[!NOTE]
>
>L’identifiant Experience Cloud (ECID) est également connu sous le nom de MCID et continue à être utilisé dans les espaces de noms.

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
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Guillemets

Les guillemets simples, les guillemets doubles et les accents graves ont des utilisations différentes dans les requêtes Query Service.

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
>Les guillemets doubles **ne peuvent pas** être utilisés avec l’accès au champ avec notation par points.

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

## Affichage des informations relatives aux tableaux

Après la connexion à Query Service, vous pouvez voir toutes vos tables disponibles sur Platform à l’aide de l’une des fonctionnalités suivantes : `\d` ou `SHOW TABLES` des commandes.

### Affichage de tableau standard

Le `\d` affiche la commande standard [!DNL PostgreSQL] pour répertorier les tables. Vous trouverez ci-dessous un exemple de sortie de cette commande :

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Affichage détaillé du tableau

`SHOW TABLES` est une commande personnalisée qui fournit des informations plus détaillées sur les tables. Vous trouverez ci-dessous un exemple de sortie de cette commande :

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Informations du schéma

Pour afficher des informations plus détaillées sur les schémas du tableau, vous pouvez utiliser la variable `\d {TABLE_NAME}` où `{TABLE_NAME}` est le nom de la table dont vous souhaitez afficher les informations sur le schéma.

L’exemple suivant illustre les informations de schéma pour la variable `luma_midvalues` tableau, qui s’affiche à l’aide de `\d luma_midvalues`:

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
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

De plus, vous pouvez obtenir des informations supplémentaires sur une colonne spécifique en ajoutant le nom de la colonne au nom de la table. Il serait écrit au format `\d {TABLE_NAME}_{COLUMN}`.

L’exemple suivant illustre des informations supplémentaires pour la variable `web` et sont appelés à l’aide de la commande suivante : `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Association de jeux de données

Vous pouvez joindre plusieurs jeux de données pour inclure des données d’autres jeux de données dans votre requête.

L’exemple suivant rejoint les deux jeux de données suivants (`your_analytics_table` et `custom_operating_system_lookup`) et crée une `SELECT` pour les 50 premiers systèmes d’exploitation par nombre de pages vues.

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

| OperatingSystem | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 315032.0 |
| Windows Vista | 173566.0 |
| Mobile iOS 6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003 et XP Edition x64 | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## Déduplication

Query Service prend en charge le dédoublonnage des données ou la suppression des doublons de lignes des données. Pour plus d’informations sur la déduplication, veuillez lire la section [Guide de déduplication de Query Service](./deduplication.md).

## Calcul des fuseaux horaires dans Query Service

Query Service normalise les données persistantes dans Adobe Experience Platform à l’aide du format d’horodatage UTC. Pour plus d’informations sur la façon de traduire vos exigences de fuseau horaire en et depuis un horodatage UTC, consultez la section [Section FAQ sur la modification du fuseau horaire en UTC](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Étapes suivantes

La lecture de ce document vous a permis de vous initier à certaines considérations importantes lors de la rédaction d’une requête avec [!DNL Query Service]. Pour plus d’informations sur l’utilisation de la syntaxe SQL pour la rédaction de vos propres requêtes, veuillez lire la [documentation sur la syntaxe SQL](../sql/syntax.md).

Pour plus d’exemples de requêtes pouvant être utilisées dans Query Service, veuillez lire la documentation de cas d’utilisation suivante :

- [Analytics insights](../use-cases/analytics-insights.md)
- [Analyse des activités avec Adobe Target](../use-cases/activity-analysis-with-adobe-target.md)
- [Exemples de requêtes ExperienceEvent](../sample-queries/experience-event.md).

---
keywords: Experience Platform;home;popular topics;query service;Query service;sql syntax;sql;ctas;CTAS;Create table as select
solution: Experience Platform
title: Syntaxe SQL
topic: syntax
description: Ce document présente la syntaxe SQL compatible avec Query Service.
translation-type: tm+mt
source-git-commit: 2672d0bdf1f34deb715415e7b660a35076edb06b
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 94%

---


# Syntaxe SQL

[!DNL Query Service] permet d’utiliser le langage SQL ANSI standard pour les instructions `SELECT` et autres commandes limitées. This document shows SQL syntax supported by [!DNL Query Service].

## Définition d’une requête SELECT

La syntaxe suivante définit une requête `SELECT` compatible avec [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

où `from_item` peut correspondre à l’un des éléments suivants :

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

et `grouping_element` peut correspondre à l’un des suivants :

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

et `with_query` correspond à :

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### Clause WHERE ILIKE

Le mot-clé ILIKE peut être utilisé à la place de LIKE pour obtenir des correspondances sur la clause WHERE de la requête SELECT insensible à la casse.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La logique des clauses LIKE et ILIKE est la suivante :
- ```WHERE condition LIKE pattern```, ```~~``` équivaut au modèle
- ```WHERE condition NOT LIKE pattern```, ```!~~``` équivaut au modèle
- ```WHERE condition ILIKE pattern```, ```~~*``` équivaut au modèle
- ```WHERE condition NOT ILIKE pattern```, ```!~~*``` équivaut au modèle


#### Exemple

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Renvoie les clients dont le nom commence par « A » ou « a ».

## JOINS

Une requête `SELECT` utilisant des jointures présente la syntaxe suivante :

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNION, INTERSECT et EXCEPT

Les clauses `UNION`, `INTERSECT` et `EXCEPT` permettent de combiner ou d’exclure des lignes similaires de deux ou plusieurs tables :

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## CREATE TABLE AS SELECT

La syntaxe suivante définit une requête `CREATE TABLE AS SELECT` (CTAS) compatible avec [!DNL Query Service]:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

where,
`target_schema_title` is the title of XDM schema. N&#39;utilisez cette clause que si vous souhaitez utiliser un schéma XDM existant pour le nouveau jeu de données créé par la requête`rowvalidation` CTAS indique si l&#39;utilisateur souhaite une validation au niveau des lignes de tous les nouveaux lots ingérés pour le nouveau jeu de données créé. La valeur par défaut est &quot;false&quot;

et `select_query` correspond à une instruction `SELECT`, dont la syntaxe est définie ci-dessus dans le présent document.


### Exemple

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Notez que pour une requête CTAS donnée :

1. L’instruction `SELECT` doit posséder un alias pour les fonctions d’agrégation telles que `COUNT`, `SUM`, `MIN`, etc.
2. L’instruction `SELECT` peut être fournie avec ou sans parenthèses ().

## INSERT INTO

La syntaxe suivante définit une requête `INSERT INTO` compatible avec [!DNL Query Service]:

```sql
INSERT INTO table_name select_query
```

où `select_query` correspond à une instruction `SELECT`, dont la syntaxe est définie ci-dessus dans le présent document.

### Exemple

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Notez que pour une requête INSERT INTO donnée :

1. L’instruction `SELECT` ne doit pas être mise entre parenthèses ().
2. Le schéma du résultat de l’instruction `SELECT` doit être conforme à celui de la table définie dans l’instruction `INSERT INTO`.

### DROP TABLE

Supprimez une table et le répertoire associé à la table dans le système de fichiers s’il ne s’agit pas d’une table externe. Si la table à supprimer n’existe pas, une exception se produit.

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Paramètres

- `IF EXISTS` : si la table n’existe pas, rien ne se passe
- `TEMP` : table temporaire

## CREATE VIEW

La syntaxe suivante définit une requête `CREATE VIEW` compatible avec [!DNL Query Service]:

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

Où `view_name` correspond au nom de la vue à créer
et `select_query` correspond à une instruction `SELECT`, dont la syntaxe est définie ci-dessus dans le présent document.

Exemple :

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### DROP VIEW

La syntaxe suivante définit une requête `DROP VIEW` compatible avec [!DNL Query Service]:

```sql
DROP VIEW [IF EXISTS] view_name
```

Où `view_name` correspond au nom de la vue à supprimer

Exemple :

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] Commandes SQL

### SET

Définissez une propriété, renvoyez la valeur d’une propriété existante ou répertoriez toutes les propriétés existantes. Si une valeur est fournie pour une clé de propriété existante, l’ancienne valeur est remplacée.

```sql
SET property_key [ To | =] property_value
```

Pour renvoyer la valeur d’un paramètre, utilisez `SHOW [setting name]`.

## Commandes PostgreSQL

### BEGIN

Cette commande est analysée et la commande effectuée est renvoyée au client. Elle est identique à la commande `START TRANSACTION`.

```sql
BEGIN [ TRANSACTION ]
```

#### Paramètres

- `TRANSACTION` : mots-clés optionnels. Elle écoute, aucune action n’est nécessaire.

### CLOSE

`CLOSE` libère les ressources associées à un curseur ouvert. Une fois le curseur fermé, aucune opération n’est autorisée sur celui-ci. Un curseur doit être fermé lorsqu’il n’est plus nécessaire.

```sql
CLOSE { name }
```

#### Paramètres

- `name` : le nom du curseur ouvert à fermer.

### COMMIT

No action is taken in [!DNL Query Service] as a response to the commit transaction statement.

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### Paramètres

- `WORK`
- `TRANSACTION` : mots-clés optionnels. Ils sont sans effet.

### DEALLOCATE

Utilisez `DEALLOCATE` pour désaffecter une instruction SQL préparée précédemment. Si vous ne désaffectez pas explicitement une instruction préparée, elle est désaffectée en fin de session.

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Paramètres

- `Prepare` : ce mot-clé est ignoré.
- `name` : le nom de l’instruction préparée à désaffecter.
- `ALL` : désaffectez toutes les instructions préparées.

### DECLARE

`DECLARE` permet à un utilisateur de créer des curseurs. Ils peuvent être utilisés pour récupérer un petit nombre de lignes à la fois à partir d’une requête plus importante. Une fois le curseur créé, les lignes sont récupérées à l’aide de `FETCH`.

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Paramètres

- `name` : le nom du curseur à créer.
- `WITH HOLD` : indique une utilisation possible du curseur après la validation de la transaction qui l’a créé.
- `query` : une commande `SELECT` ou `VALUES` qui fournit les lignes à renvoyer par le curseur.

### EXECUTE

`EXECUTE` sert à exécuter une instruction préparée au préalable. Comme les instructions préparées existent seulement pour la durée d’une session, l’instruction préparée doit avoir été créée par une instruction `PREPARE` exécutée plus tôt dans la session en cours.

Si l’instruction `PREPARE` qui crée l’instruction spécifie certains paramètres, un ensemble compatible de paramètres doit être transmis à l’instruction `EXECUTE`, sinon une erreur se produit. Notez que les instructions préparées, contrairement aux fonctions, ne sont pas surchargées en fonction du type ou du nombre de paramètres. Le nom d’une instruction préparée doit être unique au sein d’une session de base de données.

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Paramètres

- `name` : le nom de l’instruction préparée à exécuter.
- `parameter` : la valeur réelle du paramètre d’une instruction préparée. Ce paramètre doit être une expression donnant une valeur compatible avec le type de données de ce paramètre, tel que déterminé lors de la création de l’instruction préparée.

### EXPLAIN

Cette commande affiche le plan d’exécution que le planificateur de PostgreSQL génère pour l’instruction fournie. Le plan d’exécution indique la manière dont les tables référencées par l’instruction sont analysées, par analyse séquentielle ordinaire, analyse d’index, etc. Si plusieurs tables sont référencées, il présente également les algorithmes de jointures utilisés pour rassembler les lignes issues des différentes tables d’entrée.

La partie la plus importante de l’affichage concerne l’affichage des coûts estimés d’exécution de l’instruction. Ils représentent l’estimation réalisée par le planificateur du temps d’exécution de l’instruction (mesuré en une unité de coût arbitraire, bien que conventionnellement ce sont des récupérations de page disque). Deux nombres sont affichés : le coût de démarrage, avant que la première ligne soit renvoyée, et le coût total, nécessaire au renvoi de toutes les lignes. Pour la plupart des requêtes, le coût total est celui qui importe. Mais dans certains cas, comme pour une sous-requête dans la clause EXISTS, le planificateur choisit le coût de démarrage le plus faible au lieu du coût total le plus faible (parce que l’exécuteur s’arrête après la récupération d’une ligne, de toute façon). De même, si vous limitez le nombre de lignes à renvoyer avec une clause `LIMIT`, le planificateur effectue une interpolation appropriée entre les coûts limites pour choisir le plan réellement moins coûteux.

L’option `ANALYZE` impose l’exécution de l’instruction en plus de sa planification. Ensuite, les statistiques d’exécution réelle sont ajoutées à l’affichage, y compris le temps total écoulé dans chaque nœud du plan (en millisecondes) et le nombre total de lignes renvoyées. Cela est utile pour vérifier la véracité des estimations fournies par le planificateur.

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Paramètres

- `ANALYZE` : exécutez la commande et affichez les temps d’exécution réels et d’autres statistiques. Ce paramètre est défini par défaut sur `FALSE`.
- `FORMAT` : spécifiez le format de sortie, qui peut être TEXT, XML, JSON ou YAML. Les sorties autres que text contiennent les mêmes informations que le format de sortie text, mais les programmes pourront plus facilement les analyser. Ce paramètre est défini par défaut sur `TEXT`.
- `statement` : toute instruction `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` ou `CREATE MATERIALIZED VIEW AS`, dont vous souhaitez afficher le plan d’exécution.

>[!IMPORTANT]
>
>Gardez à l’esprit que l’instruction est réellement exécutée lorsque l’option `ANALYZE` est utilisée. Même si `EXPLAIN` ignore les sorties renvoyées par `SELECT`, les autres effets de l’instruction se produisent comme d’habitude.

#### Exemple

Pour afficher le plan d’une requête simple sur une table d’une seule colonne `integer` et 10 000 lignes :

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` récupère les lignes à l’aide d’un curseur créé précédemment.

La position associée du curseur est utilisée par `FETCH`. Le curseur peut être positionné avant la première ligne du résultat de la requête, sur une ligne particulière du résultat ou après la dernière ligne du résultat. Une fois créé, le curseur est positionné avant la première ligne. Après avoir récupéré certaines lignes, le curseur est positionné sur la ligne la plus récemment récupérée. Si `FETCH` atteint la fin des lignes disponibles, le curseur est positionné après la dernière ligne. Si cette ligne n’existe pas, un résultat vide est renvoyé et le curseur est positionné avant la première ligne ou après la dernière ligne, selon le cas.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Paramètres

- `num_of_rows` : une constante de type entier probablement signée, qui précise l’emplacement ou le nombre de lignes à récupérer.
- `cursor_name` : le nom d’un curseur ouvert.

### PREPARE

`PREPARE` crée une instruction préparée. Une instruction préparée est un objet côté serveur qui peut être utilisé pour optimiser les performances. Lorsque l’instruction `PREPARE` est exécutée, l’instruction spécifiée est analysée et réécrite. Lorsqu’une commande `EXECUTE` est ensuite lancée, l’instruction préparée est planifiée et exécutée. Cette division du travail évite une analyse répétitive tout en permettant au plan d’exécution de dépendre des valeurs spécifiques du paramètre fournies.

Les instructions préparées peuvent prendre des paramètres, des valeurs qui sont remplacées dans l’instruction lors de son exécution. Lors de la création de l’instruction préparée, consultez les paramètres en fonction de leur position, à l’aide de $1, $2, etc. Une liste correspondante des types de données des paramètres peut être spécifiée. Lorsque le type de données d’un paramètre n’est pas spécifié ou est déclaré comme inconnu, le type est inféré à partir du contexte dans lequel le paramètre est référencé pour la première fois, si possible. Lors de l’exécution de l’instruction, spécifiez les valeurs réelles de ces paramètres dans l’instruction `EXECUTE`.

Les instructions préparées sont seulement stockées pour la durée de la session de base de données en cours. Lorsque la session se termine, l’instruction préparée est oubliée. Elle doit donc être recréée avant d’être réutilisée. Cela signifie également qu’une seule instruction préparée ne peut pas être utilisée par plusieurs clients de bases de données simultanément. Cependant, chaque client peut créer sa propre instruction préparée à utiliser. Les instructions préparées peuvent être supprimées manuellement à l’aide de la commande `DEALLOCATE`.

Les instructions préparées sont principalement intéressantes en termes de performances lorsqu’une seule session est utilisée pour exécuter un grand nombre d’instructions similaires. La différence de performances est particulièrement importante si la planification ou la réécriture des instructions est complexe, par exemple, si la requête implique la jointure de nombreuses tables ou l’application de plusieurs règles. Si l’instruction est relativement simple à planifier et à réécrire, mais assez coûteuse à exécuter, l’avantage en termes de performances des instructions préparées est moins perceptible.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Paramètres

- `name` : un nom arbitraire donné à cette instruction préparée particulière. Il doit être unique dans une seule session et est ensuite utilisé pour exécuter ou désaffecter une instruction préparée au préalable.
- `data-type` : le type de données d’un paramètre de l’instruction préparée. Si le type de données d’un paramètre particulier n’est pas spécifié ou est spécifié comme étant inconnu, il est inféré à partir du contexte dans lequel le paramètre est référencé pour la première fois. Pour référencer les paramètres de l’instruction préparée, utilisez $1, $2, etc.


### ROLLBACK

`ROLLBACK` annule la transaction en cours et toutes les mises à jour effectuées lors de cette transaction.

```sql
ROLLBACK [ WORK ]
```

#### Paramètres

- `WORK`

### SELECT INTO

`SELECT INTO` crée une nouvelle table en la remplissant avec des données récupérées par une requête. Les données ne sont pas renvoyées au client comme le fait habituellement l’instruction `SELECT`. Les noms et les types de données des colonnes de la nouvelle table sont associés aux colonnes de sortie de l’instruction `SELECT`.

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

#### Paramètres

- `TEMPORARAY` ou `TEMP` : si spécifié, la table est créée comme une table temporaire.
- `UNLOGGED:` si spécifié, la table est créée sous la forme d’une table non enregistrée.
- `new_table` Le nom de la table à créer (pouvant être qualifié par le nom du schéma).

#### Exemple

Créer une nouvelle table `films_recent` ne contenant que les entrées récentes de la table `films` :

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

`SHOW` affiche la configuration actuelle des paramètres d’exécution. Ces variables peuvent être définies à l’aide de l’instruction `SET`, en modifiant le fichier de configuration postgresql.conf, par l’intermédiaire de la variable d’environnement `PGOPTIONS` (lors de l’utilisation de libpq ou d’une application basée sur libpq) ou à l’aide des indicateurs de ligne de commande lors du démarrage du serveur postgres.

```sql
SHOW name
```

#### Paramètres

- `name` :
   - `SERVER_VERSION` : affiche le numéro de version du serveur.
   - `SERVER_ENCODING` : affiche l’encodage des caractères côté serveur. Actuellement, ce paramètre peut être affiché mais pas défini, car l’encodage est déterminé lors de la création de la base de données.
   - `LC_COLLATE` : affiche le paramètre régional de la base de données pour le classement (tri de texte). Actuellement, ce paramètre peut être affiché mais pas défini, car la configuration est déterminée lors de la création de la base de données.
   - `LC_CTYPE` : affiche le paramètre régional de la base de données pour la classification des caractères. Actuellement, ce paramètre peut être affiché mais pas défini, car la configuration est déterminée lors de la création de la base de données.
      `IS_SUPERUSER` : vrai si le rôle actuel possède des droits de super utilisateur.
- `ALL` : affiche les valeurs de tous les paramètres de configuration avec des descriptions.

#### Exemple

Afficher la configuration actuelle du paramètre `DateStyle`

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### START TRANSACTION

Cette commande est analysée et renvoie la commande effectuée au client. Elle est identique à la commande `BEGIN`.

```sql
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### COPIER

Cette commande permet de vider la sortie de toute requête SELECT vers un emplacement spécifié. L&#39;utilisateur doit avoir accès à cet emplacement pour que cette commande réussisse.

```sql
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>Le chemin de sortie complet sera `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`
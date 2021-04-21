---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de Requête;syntaxe sql;sql;ctas;CTAS;Créer une table comme sélectionner
solution: Experience Platform
title: Syntaxe SQL dans Requête Service
topic-legacy: syntax
description: Ce document affiche la syntaxe SQL prise en charge par Adobe Experience Platform Requête Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 14%

---

# Syntaxe SQL dans Requête Service

Adobe Experience Platform Requête Service permet d&#39;utiliser un SQL ANSI standard pour les instructions `SELECT` et d&#39;autres commandes limitées. Ce document couvre la syntaxe SQL prise en charge par [!DNL Query Service].

## SELECT requêtes {#select-queries}

La syntaxe suivante définit une requête `SELECT` compatible avec [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

où `from_item` peut être l&#39;une des options suivantes :

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

et `grouping_element` peut être l&#39;une des options suivantes :

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

et `with_query` correspond à :

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

Les sous-sections suivantes fournissent des détails sur les clauses supplémentaires que vous pouvez utiliser dans vos requêtes, à condition qu’elles suivent le format décrit ci-dessus.

### Clause SNAPSHOT

Cette clause peut être utilisée pour lire de manière incrémentielle les données d&#39;une table en fonction des ID d&#39;instantané. Un ID d&#39;instantané est un marqueur de point de contrôle représenté par un numéro de type Long appliqué à une table de lac de données chaque fois que des données y sont écrites. La clause `SNAPSHOT` s&#39;attache à la relation de table à laquelle elle est utilisée.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Exemple

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Notez qu&#39;une clause `SNAPSHOT` fonctionne avec un alias de table ou de table mais pas au-dessus d&#39;une sous-requête ou d&#39;une vue. Une clause `SNAPSHOT` fonctionnera partout où une requête `SELECT` peut être appliquée à une table.

De plus, vous pouvez utiliser `HEAD` et `TAIL` comme valeurs de décalage spéciales pour les clauses d&#39;instantané. L&#39;utilisation de `HEAD` fait référence à un décalage avant le premier instantané, tandis que `TAIL` fait référence à un décalage après le dernier instantané.

### Clause WHERE

Par défaut, les correspondances produites par une clause `WHERE` sur une requête `SELECT` sont sensibles à la casse. Si vous souhaitez que les correspondances ne soient pas sensibles à la casse, vous pouvez utiliser le mot-clé `ILIKE` au lieu de `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La logique des clauses LIKE et ILIKE est expliquée dans le tableau suivant :

| Clause | Opérateur |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**Exemple**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Cette requête renvoie les clients dont les noms commencent par &quot;A&quot; ou &quot;a&quot;.

### REJOINDRE

Une requête `SELECT` qui utilise des jointures a la syntaxe suivante :

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT et EXCEPT

Les clauses `UNION`, `INTERSECT` et `EXCEPT` sont utilisées pour combiner ou exclure des lignes similaires de plusieurs tables :

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREATE TABLE AS SELECT

La syntaxe suivante définit une requête `CREATE TABLE AS SELECT` (CTAS) :

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**Paramètres**

- `schema`: Titre du schéma XDM. Utilisez cette clause uniquement si vous souhaitez utiliser un schéma XDM existant pour le nouveau jeu de données créé par la requête CTAS.
- `rowvalidation`: (Facultatif) Indique si l’utilisateur souhaite la validation au niveau de la ligne de tous les nouveaux lots ingérés pour le jeu de données nouvellement créé. La valeur par défaut est `true`.
- `select_query`: Une  `SELECT` déclaration. La syntaxe de la requête `SELECT` se trouve dans la section [requêtes SELECT](#select-queries).

**Exemple**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>L’instruction `SELECT` doit posséder un alias pour les fonctions d’agrégation telles que `COUNT`, `SUM`, `MIN`, etc. De plus, l&#39;instruction `SELECT` peut être fournie avec ou sans parenthèses (). Vous pouvez fournir une clause `SNAPSHOT` pour lire les deltas incrémentiels dans la table de cible.

## INSERT INTO

La commande `INSERT INTO` est définie comme suit :

```sql
INSERT INTO table_name select_query
```

**Paramètres**

- `table_name`: Nom du tableau dans lequel vous souhaitez insérer la requête.
- `select_query`: Une  `SELECT` déclaration. La syntaxe de la requête `SELECT` se trouve dans la section [requêtes SELECT](#select-queries).

**Exemple**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> L&#39;instruction `SELECT` **ne doit pas** être placée entre parenthèses (). De plus, le schéma du résultat de l&#39;instruction `SELECT` doit être conforme à celui de la table définie dans l&#39;instruction `INSERT INTO`. Vous pouvez fournir une clause `SNAPSHOT` pour lire les deltas incrémentiels dans la table de cible.

## DROP TABLE

La commande `DROP TABLE` supprime une table existante et supprime le répertoire associé à la table du système de fichiers s&#39;il ne s&#39;agit pas d&#39;une table externe. Si la table n&#39;existe pas, une exception se produit.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Paramètres**

- `IF EXISTS`: Si ce paramètre est spécifié, aucune exception n’est générée si le tableau n’ **** existe pas.

## CREATE VIEW

La syntaxe suivante définit une requête `CREATE VIEW` :

```sql
CREATE VIEW view_name AS select_query
```

**Paramètres**

- `view_name`: Nom de la vue à créer.
- `select_query`: Une  `SELECT` déclaration. La syntaxe de la requête `SELECT` se trouve dans la section [requêtes SELECT](#select-queries).

**Exemple**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

La syntaxe suivante définit une requête `DROP VIEW` :

```sql
DROP VIEW [IF EXISTS] view_name
```

**Paramètre**

- `IF EXISTS`: Si cette valeur est spécifiée, aucune exception n’est générée si la vue  **** n’existe pas.
- `view_name`: Nom de la vue à supprimer.

**Exemple**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] Commandes SQL

La sous-section ci-dessous couvre les commandes Spark SQL prises en charge par Requête Service.

### SET

La commande `SET` définit une propriété et renvoie la valeur d&#39;une propriété existante ou liste toutes les propriétés existantes. Si une valeur est fournie pour une clé de propriété existante, l’ancienne valeur est remplacée.

```sql
SET property_key = property_value
```

**Paramètres**

- `property_key`: Nom de la propriété que vous souhaitez liste ou modifier.
- `property_value`: Valeur sous laquelle la propriété doit être définie.

Pour renvoyer la valeur d&#39;un paramètre, utilisez `SET [property key]` sans `property_value`.

## Commandes PostgreSQL

Les sous-sections ci-dessous couvrent les commandes PostgreSQL prises en charge par Requête Service.

### BEGIN

La commande `BEGIN`, ou la commande `BEGIN WORK` ou `BEGIN TRANSACTION`, initie un bloc de transaction. Les instructions saisies après la commande begin sont exécutées dans une seule transaction jusqu&#39;à ce qu&#39;une commande COMMIT ou ROLLBACK explicite soit donnée. Cette commande est identique à `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CLOSE

La commande `CLOSE` libère les ressources associées à un curseur ouvert. Une fois le curseur fermé, aucune opération n’est autorisée sur celui-ci. Un curseur doit être fermé lorsqu’il n’est plus nécessaire.

```sql
CLOSE name
CLOSE ALL
```

Si `CLOSE name` est utilisé, `name` représente le nom d&#39;un curseur ouvert qui doit être fermé. Si `CLOSE ALL` est utilisé, tous les curseurs ouverts seront fermés.

### DEALLOCATE

La commande `DEALLOCATE` vous permet de délocaliser une instruction SQL précédemment préparée. Si vous ne désaffectez pas explicitement une instruction préparée, elle est désaffectée en fin de session. Pour plus d&#39;informations sur les instructions préparées, consultez la section [Commande PREPARE](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Si `DEALLOCATE name` est utilisé, `name` représente le nom de l&#39;instruction préparée qui doit être délocalisée. Si `DEALLOCATE ALL` est utilisé, toutes les instructions préparées seront cédées.

### DECLARE

La commande `DECLARE` permet à un utilisateur de créer un curseur, qui peut être utilisé pour récupérer un petit nombre de lignes d&#39;une requête plus grande. Une fois le curseur créé, les lignes sont récupérées à l’aide de `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

**Paramètres**

- `name` : le nom du curseur à créer.
- `query` : une commande `SELECT` ou `VALUES` qui fournit les lignes à renvoyer par le curseur.

### EXECUTE

La commande `EXECUTE` est utilisée pour exécuter une instruction préparée précédemment. Étant donné que les instructions préparées n&#39;existent que pour la durée d&#39;une session, l&#39;instruction préparée doit avoir été créée par une instruction `PREPARE` exécutée plus tôt au cours de la session en cours. Pour plus d&#39;informations sur l&#39;utilisation des instructions préparées, consultez la section [`PREPARE` commande](#prepare).

Si l&#39;instruction `PREPARE` qui a créé l&#39;instruction a spécifié certains paramètres, un ensemble compatible de paramètres doit être transmis à l&#39;instruction `EXECUTE`. Si ces paramètres ne sont pas transmis, une erreur est générée.

```sql
EXECUTE name [ ( parameter ) ]
```

**Paramètres**

- `name` : le nom de l’instruction préparée à exécuter.
- `parameter` : la valeur réelle du paramètre d’une instruction préparée. Ce paramètre doit être une expression donnant une valeur compatible avec le type de données de ce paramètre, tel que déterminé lors de la création de l’instruction préparée.  S&#39;il existe plusieurs paramètres pour l&#39;instruction préparée, ils sont séparés par des virgules.

### EXPLAIN

La commande `EXPLAIN` affiche le plan d&#39;exécution de l&#39;instruction fournie. Le plan d&#39;exécution montre comment les tables référencées par l&#39;instruction seront analysées.  Si plusieurs tables sont référencées, elles indiquent les algorithmes de jointure utilisés pour rassembler les lignes requises de chaque tableau d’entrée.

```sql
EXPLAIN option statement
```

Où `option` peut être l&#39;un des suivants :

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Paramètres**

- `ANALYZE`: Si le  `option` contient  `ANALYZE`, les heures d’exécution et d’autres statistiques s’affichent.
- `FORMAT`: Si le  `option` contient  `FORMAT`, il spécifie le format de sortie, qui peut être  `TEXT` ou  `JSON`ou. Les sorties autres que text contiennent les mêmes informations que le format de sortie text, mais les programmes pourront plus facilement les analyser. Ce paramètre est défini par défaut sur `TEXT`.
- `statement` : toute instruction `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` ou `CREATE MATERIALIZED VIEW AS`, dont vous souhaitez afficher le plan d’exécution.

>[!IMPORTANT]
>
>Gardez à l’esprit que l’instruction est réellement exécutée lorsque l’option `ANALYZE` est utilisée. Même si `EXPLAIN` ignore les sorties renvoyées par `SELECT`, les autres effets de l’instruction se produisent comme d’habitude.

**Exemple**

L&#39;exemple suivant montre le plan d&#39;une requête simple sur un tableau avec une seule colonne `integer` et 1 000 lignes :

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

La commande `FETCH` récupère les lignes à l&#39;aide d&#39;un curseur créé précédemment.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Paramètres**

- `num_of_rows`: Nombre de lignes à récupérer.
- `cursor_name`: Nom du curseur à partir duquel vous récupérez des informations.

### PREPARE {#prepare}

La commande `PREPARE` permet de créer une instruction préparée. Une instruction préparée est un objet côté serveur qui peut être utilisé pour modéliser des instructions SQL similaires.

Les instructions préparées peuvent prendre des paramètres, c&#39;est-à-dire des valeurs qui sont substituées dans l&#39;instruction lors de son exécution. Les paramètres sont référencés par position, en utilisant $1, $2, etc., lors de l&#39;utilisation d&#39;instructions préparées.

Vous pouvez éventuellement spécifier une liste de types de données de paramètre. Si le type de données d&#39;un paramètre n&#39;est pas répertorié, le type peut être déduit du contexte.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Paramètres**

- `name`: Nom de l&#39;instruction préparée.
- `data_type`: Types de données des paramètres de l&#39;instruction préparée. Si le type de données d&#39;un paramètre n&#39;est pas répertorié, le type peut être déduit du contexte. Si vous devez ajouter plusieurs types de données, vous pouvez les ajouter dans une liste séparée par des virgules.

### ROLLBACK

La commande `ROLLBACK` annule la transaction actuelle et ignore toutes les mises à jour effectuées par la transaction.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

La commande `SELECT INTO` crée une table et la remplit avec des données calculées par une requête. Les données ne sont pas renvoyées au client, comme c&#39;est le cas avec une commande normale `SELECT`. Les colonnes de la nouvelle table ont les noms et les types de données associés aux colonnes de sortie de la commande `SELECT`.

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

**Paramètres**

Pour plus d&#39;informations sur les paramètres de requête standard SELECT, consultez la section [requête SELECT](#select-queries). Cette section ne liste que les paramètres exclusifs à la commande `SELECT INTO`.

- `TEMPORARY` ou  `TEMP`: Paramètre facultatif. Le cas échéant, la table créée sera une table temporaire.
- `UNLOGGED`: Paramètre facultatif. Si spécifié, la table créée sera une table non enregistrée. Pour plus d&#39;informations sur les tables non enregistrées, consultez la [documentation PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: Nom de la table à créer.

**Exemple**

La requête suivante crée une nouvelle table `films_recent` composée uniquement des entrées récentes de la table `films` :

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

La commande `SHOW` affiche le paramètre actuel des paramètres d&#39;exécution. Ces variables peuvent être définies à l&#39;aide de l&#39;instruction `SET`, en modifiant le fichier de configuration `postgresql.conf`, par l&#39;intermédiaire de la variable environnementale `PGOPTIONS` (lors de l&#39;utilisation de libpq ou d&#39;une application basée sur libpq), ou par l&#39;intermédiaire des indicateurs de ligne de commande lors du démarrage du serveur Postgres.

```sql
SHOW name
SHOW ALL
```

**Paramètres**

- `name`: Nom du paramètre d’exécution dont vous souhaitez obtenir des informations. Les valeurs possibles du paramètre d’exécution sont les suivantes :
   - `SERVER_VERSION`: Ce paramètre affiche le numéro de version du serveur.
   - `SERVER_ENCODING`: Ce paramètre affiche le codage du jeu de caractères côté serveur.
   - `LC_COLLATE`: Ce paramètre affiche les paramètres régionaux de la base de données pour l’assemblage (ordre de texte).
   - `LC_CTYPE`: Ce paramètre affiche les paramètres régionaux de la base de données pour la classification des caractères.
      `IS_SUPERUSER`: Ce paramètre indique si le rôle actif dispose de privilèges de super-utilisateur.
- `ALL` : affiche les valeurs de tous les paramètres de configuration avec des descriptions.

**Exemple**

La requête suivante présente le paramètre actuel `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### COPIER

La commande `COPY` vide la sortie de toute requête `SELECT` vers un emplacement spécifié. L&#39;utilisateur doit avoir accès à cet emplacement pour que cette commande réussisse.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Paramètres**

- `query`: Requête à copier.
- `format_name`: Format dans lequel vous souhaitez copier la requête. `format_name` peut être l&#39;un des `parquet`, `csv` ou `json`. Par défaut, la valeur est `parquet`.

>[!NOTE]
>
>Le chemin de sortie complet sera `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

La commande `ALTER TABLE` vous permet d&#39;ajouter ou de supprimer des contraintes de clé Principale ou étrangère, ainsi que d&#39;ajouter des colonnes au tableau.

#### AJOUTER ou DÉPOSER UNE CONTRAINTE

Les requêtes SQL suivantes montrent des exemples d&#39;ajout ou de suppression de contraintes à une table.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Paramètres**

- `table_name`: Nom de la table que vous modifiez.
- `constraint_name`: Nom de la contrainte à ajouter ou à supprimer.
- `column_name`: Nom de la colonne à laquelle vous ajoutez une contrainte.
- `referenced_table_name`: Nom de la table référencée par la clé étrangère.
- `primary_column_name`: Nom de la colonne référencée par la clé étrangère.

>[!NOTE]
>
>Le schéma du tableau doit être unique et ne pas être partagé entre plusieurs tables. En outre, l&#39;espace de nommage est obligatoire pour les contraintes Principales.

#### COLONNE AJOUTER

Les requêtes SQL suivantes montrent des exemples d&#39;ajout de colonnes à une table.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Paramètres**

- `table_name`: Nom de la table que vous modifiez.
- `column_name`: Nom de la colonne à ajouter.
- `data_type`: Type de données de la colonne à ajouter. Les types de données pris en charge sont les suivants : bigint, char, string, date, datetime, doublon, précision du doublon, integer, small int, tinyint, varchar.

### AFFICHER LES CLÉS PRINCIPAL

La commande `SHOW PRIMARY KEYS` liste toutes les contraintes de clé Principales pour la base de données donnée.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### AFFICHER LES CLÉS ÉTRANGÈRES

La commande `SHOW FOREIGN KEYS` liste toutes les contraintes de clé étrangère pour la base de données donnée.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```

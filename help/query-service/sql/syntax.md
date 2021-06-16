---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query service;syntaxe sql;sql;ctas;CTAS;Créer une table comme sélection
solution: Experience Platform
title: Syntaxe SQL dans Query Service
topic-legacy: syntax
description: Ce document présente la syntaxe SQL prise en charge par Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 26bd2abc998320245091b0917fb6f236ed09b95c
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 13%

---

# Syntaxe SQL dans Query Service

Adobe Experience Platform Query Service permet d’utiliser le langage SQL ANSI standard pour les instructions `SELECT` et d’autres commandes limitées. Ce document couvre la syntaxe SQL supportée par [!DNL Query Service].

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

où `from_item` peut être l’une des options suivantes :

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

et `grouping_element` peut être l’une des options suivantes :

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

Les sous-sections suivantes fournissent des détails sur les clauses supplémentaires que vous pouvez utiliser dans vos requêtes, à condition qu’elles suivent le format indiqué ci-dessus.

### Clause SNAPSHOT

Cette clause peut être utilisée pour lire de manière incrémentielle les données d’une table en fonction des ID d’instantané. Un ID d’instantané est un marqueur de point de contrôle représenté par un nombre de type Long appliqué à un tableau de lac de données chaque fois que des données y sont écrites. La clause `SNAPSHOT` s’attache à la relation de table à laquelle elle est utilisée.

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

Notez qu’une clause `SNAPSHOT` fonctionne avec un alias de table ou de table, mais pas sur une sous-requête ou une vue. Une clause `SNAPSHOT` fonctionnera partout où une requête `SELECT` sur une table peut être appliquée.

De plus, vous pouvez utiliser `HEAD` et `TAIL` comme valeurs de décalage spéciales pour les clauses d’instantané. L’utilisation de `HEAD` fait référence à un décalage avant le premier instantané, tandis que `TAIL` fait référence à un décalage après le dernier instantané.

### Clause WHERE

Par défaut, les correspondances générées par une clause `WHERE` sur une requête `SELECT` sont sensibles à la casse. Si vous souhaitez que les correspondances ne soient pas sensibles à la casse, vous pouvez utiliser le mot-clé `ILIKE` au lieu de `LIKE`.

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

Cette requête renvoie les clients dont le nom commence par &quot;A&quot; ou &quot;a&quot;.

### JOINDRE

Une requête `SELECT` qui utilise des jointures présente la syntaxe suivante :

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
- `rowvalidation`: (Facultatif) Indique si l’utilisateur souhaite une validation au niveau des lignes de tous les nouveaux lots ingérés pour le jeu de données nouvellement créé. La valeur par défaut est `true`.
- `select_query`: Une  `SELECT` déclaration. La syntaxe de la requête `SELECT` se trouve dans la section [Requêtes SELECT](#select-queries).

**Exemple**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>L’instruction `SELECT` doit posséder un alias pour les fonctions d’agrégation telles que `COUNT`, `SUM`, `MIN`, etc. De plus, l’instruction `SELECT` peut être fournie avec ou sans parenthèses (). Vous pouvez fournir une clause `SNAPSHOT` pour lire les deltas incrémentiels dans la table cible.

## INSERT INTO

La commande `INSERT INTO` est définie comme suit :

```sql
INSERT INTO table_name select_query
```

**Paramètres**

- `table_name`: Nom de la table dans laquelle vous souhaitez insérer la requête.
- `select_query`: Une  `SELECT` déclaration. La syntaxe de la requête `SELECT` se trouve dans la section [Requêtes SELECT](#select-queries).

**Exemple**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> L’instruction `SELECT` **ne doit pas** être mise entre parenthèses (). De plus, le schéma du résultat de l’instruction `SELECT` doit être conforme à celui de la table définie dans l’instruction `INSERT INTO`. Vous pouvez fournir une clause `SNAPSHOT` pour lire les deltas incrémentiels dans la table cible.

## DROP TABLE

La commande `DROP TABLE` supprime une table existante et supprime le répertoire associé à la table du système de fichiers s&#39;il ne s&#39;agit pas d&#39;une table externe. Si la table n’existe pas, une exception se produit.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Paramètres**

- `IF EXISTS`: Si cette valeur est spécifiée, aucune exception n’est générée si la table n’existe  **** pas.

## DROP DABASE

La commande `DROP DATABASE` supprime une base de données existante.

```sql
DROP DATABASE [IF EXISTS] db_name
```

**Paramètres**

- `IF EXISTS`: Si cette valeur est spécifiée, aucune exception n’est générée si la base de données n’existe  **** pas.

## DÉPOSER LE SCHÉMA

La commande `DROP SCHEMA` supprime un schéma existant.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

**Paramètres**

- `IF EXISTS`: Si cette valeur est spécifiée, aucune exception n’est générée si le schéma n’existe  **** pas.

- `RESTRICT`: Valeur par défaut du mode. Si cela est spécifié, le schéma ne sera déposé que s’il **ne contient aucune table.**

- `CASCADE`: Si celle-ci est spécifiée, le schéma sera déposé avec toutes les tables présentes dans le schéma.

## CREATE VIEW

La syntaxe suivante définit une requête `CREATE VIEW` :

```sql
CREATE VIEW view_name AS select_query
```

**Paramètres**

- `view_name`: Nom de la vue à créer.
- `select_query`: Une  `SELECT` déclaration. La syntaxe de la requête `SELECT` se trouve dans la section [Requêtes SELECT](#select-queries).

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

La sous-section ci-dessous couvre les commandes Spark SQL prises en charge par Query Service.

### SET

La commande `SET` définit une propriété et renvoie la valeur d’une propriété existante ou liste toutes les propriétés existantes. Si une valeur est fournie pour une clé de propriété existante, l’ancienne valeur est remplacée.

```sql
SET property_key = property_value
```

**Paramètres**

- `property_key`: Nom de la propriété que vous souhaitez répertorier ou modifier.
- `property_value`: La valeur sous laquelle vous souhaitez que la propriété soit définie.

Pour renvoyer la valeur d’un paramètre, utilisez `SET [property key]` sans `property_value`.

## Commandes PostgreSQL

Les sous-sections ci-dessous couvrent les commandes PostgreSQL prises en charge par Query Service.

### BEGIN

La commande `BEGIN`, ou la commande `BEGIN WORK` ou `BEGIN TRANSACTION`, lance un bloc de transaction. Toutes les instructions saisies après la commande de début sont exécutées dans une seule transaction jusqu’à ce qu’une commande de COMMIT ou ROLLBACK explicite soit donnée. Cette commande est identique à `START TRANSACTION`.

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

Si `CLOSE name` est utilisé, `name` représente le nom d’un curseur ouvert qui doit être fermé. Si `CLOSE ALL` est utilisé, tous les curseurs ouverts sont fermés.

### DEALLOCATE

La commande `DEALLOCATE` vous permet de désaffecter une instruction SQL préparée précédemment. Si vous ne désaffectez pas explicitement une instruction préparée, elle est désaffectée en fin de session. Vous trouverez plus d’informations sur les instructions préparées dans la section [Commande PREPARE](#prepare) .

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Si `DEALLOCATE name` est utilisé, `name` représente le nom de l’instruction préparée qui doit être désaffectée. Si `DEALLOCATE ALL` est utilisé, toutes les instructions préparées seront désaffectées.

### DECLARE

La commande `DECLARE` permet à un utilisateur de créer un curseur qui peut être utilisé pour récupérer un petit nombre de lignes à partir d’une requête plus grande. Une fois le curseur créé, les lignes sont récupérées à l’aide de `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

**Paramètres**

- `name` : le nom du curseur à créer.
- `query` : une commande `SELECT` ou `VALUES` qui fournit les lignes à renvoyer par le curseur.

### EXECUTE

La commande `EXECUTE` permet d’exécuter une instruction préparée au préalable. Comme les instructions préparées existent uniquement pour la durée d’une session, l’instruction préparée doit avoir été créée par une instruction `PREPARE` exécutée plus tôt dans la session en cours. Vous trouverez plus d’informations sur l’utilisation des instructions préparées dans la section [`PREPARE` command](#prepare) .

Si l’instruction `PREPARE` qui a créé l’instruction spécifie certains paramètres, un ensemble compatible de paramètres doit être transmis à l’instruction `EXECUTE`. Si ces paramètres ne sont pas transmis, une erreur s’affiche.

```sql
EXECUTE name [ ( parameter ) ]
```

**Paramètres**

- `name` : le nom de l’instruction préparée à exécuter.
- `parameter` : la valeur réelle du paramètre d’une instruction préparée. Ce paramètre doit être une expression donnant une valeur compatible avec le type de données de ce paramètre, tel que déterminé lors de la création de l’instruction préparée.  S’il existe plusieurs paramètres pour l’instruction préparée, ils sont séparés par des virgules.

### EXPLAIN

La commande `EXPLAIN` affiche le plan d’exécution de l’instruction fournie. Le plan d’exécution indique comment les tables référencées par l’instruction seront analysées.  Si plusieurs tableaux sont référencés, les algorithmes de jointure utilisés pour rassembler les lignes requises de chaque tableau d’entrée s’affichent.

```sql
EXPLAIN option statement
```

Où `option` peut être l’un des suivants :

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Paramètres**

- `ANALYZE`: Si le  `option` contient  `ANALYZE`, les heures d’exécution et d’autres statistiques s’affichent.
- `FORMAT`: Si le  `option` contient  `FORMAT`, il indique le format de sortie, qui peut être  `TEXT` ou  `JSON`. Les sorties autres que text contiennent les mêmes informations que le format de sortie text, mais les programmes pourront plus facilement les analyser. Ce paramètre est défini par défaut sur `TEXT`.
- `statement` : toute instruction `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` ou `CREATE MATERIALIZED VIEW AS`, dont vous souhaitez afficher le plan d’exécution.

>[!IMPORTANT]
>
>Gardez à l’esprit que l’instruction est réellement exécutée lorsque l’option `ANALYZE` est utilisée. Même si `EXPLAIN` ignore les sorties renvoyées par `SELECT`, les autres effets de l’instruction se produisent comme d’habitude.

**Exemple**

L’exemple suivant montre le plan d’une requête simple sur une table avec une seule colonne `integer` et 10 000 lignes :

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

La commande `FETCH` récupère les lignes à l’aide d’un curseur créé précédemment.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Paramètres**

- `num_of_rows`: Nombre de lignes à récupérer.
- `cursor_name`: Le nom du curseur à partir duquel vous récupérez des informations.

### PREPARE {#prepare}

La commande `PREPARE` permet de créer une instruction préparée. Une instruction préparée est un objet côté serveur qui peut être utilisé pour modéliser des instructions SQL similaires.

Les instructions préparées peuvent prendre des paramètres, qui sont des valeurs qui sont substituées dans l’instruction lors de son exécution. Les paramètres sont référencés par position, à l’aide de $1, $2, etc., lors de l’utilisation d’instructions préparées.

Vous pouvez éventuellement spécifier une liste de types de données de paramètre. Si le type de données d’un paramètre n’est pas répertorié, le type peut être déduit du contexte.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Paramètres**

- `name`: Nom de l’instruction préparée.
- `data_type`: Types de données des paramètres de l’instruction préparée. Si le type de données d’un paramètre n’est pas répertorié, le type peut être déduit du contexte. Si vous devez ajouter plusieurs types de données, vous pouvez les ajouter dans une liste séparée par des virgules.

### ROLLBACK

La commande `ROLLBACK` annule la transaction en cours et ignore toutes les mises à jour effectuées par la transaction.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

La commande `SELECT INTO` crée une nouvelle table et la remplit avec des données calculées par une requête. Les données ne sont pas renvoyées au client, comme c’est le cas avec une commande `SELECT` normale. Les noms et les types de données des colonnes de la nouvelle table sont associés aux colonnes de sortie de la commande `SELECT`.

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

Vous trouverez plus d’informations sur les paramètres de requête SELECT standard dans la [section Requête SELECT](#select-queries). Cette section répertorie uniquement les paramètres qui sont exclusifs à la commande `SELECT INTO`.

- `TEMPORARY` ou  `TEMP`: Paramètre facultatif. Si spécifié, la table créée sera une table temporaire.
- `UNLOGGED`: Paramètre facultatif. Si spécifié, la table créée sera une table non enregistrée. Vous trouverez plus d’informations sur les tables non enregistrées dans la [documentation PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: Nom de la table à créer.

**Exemple**

La requête suivante crée une nouvelle table `films_recent` composée uniquement des entrées récentes de la table `films` :

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

La commande `SHOW` affiche le paramètre actuel des paramètres d’exécution. Ces variables peuvent être définies à l’aide de l’instruction `SET`, en modifiant le fichier de configuration `postgresql.conf`, par l’intermédiaire de la variable d’environnement `PGOPTIONS` (lors de l’utilisation de libpq ou d’une application basée sur libpq) ou par des indicateurs de ligne de commande lors du démarrage du serveur Postgres.

```sql
SHOW name
SHOW ALL
```

**Paramètres**

- `name`: Nom du paramètre d’exécution dont vous souhaitez obtenir des informations. Les valeurs possibles du paramètre d’exécution sont les suivantes :
   - `SERVER_VERSION`: Ce paramètre affiche le numéro de version du serveur.
   - `SERVER_ENCODING`: Ce paramètre affiche le codage du jeu de caractères côté serveur.
   - `LC_COLLATE`: Ce paramètre affiche les paramètres régionaux de la base de données pour le classement (tri de texte).
   - `LC_CTYPE`: Ce paramètre affiche le paramètre régional de la base de données pour la classification des caractères.
      `IS_SUPERUSER`: Ce paramètre indique si le rôle actuel possède des privilèges de super-utilisateur.
- `ALL` : affiche les valeurs de tous les paramètres de configuration avec des descriptions.

**Exemple**

La requête suivante affiche le paramètre actuel `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### COPY

La commande `COPY` vide la sortie de toute requête `SELECT` vers un emplacement spécifié. L’utilisateur doit avoir accès à cet emplacement pour que cette commande réussisse.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Paramètres**

- `query`: La requête que vous souhaitez copier.
- `format_name`: Format dans lequel vous souhaitez copier la requête. `format_name` peut être l’un des `parquet`, `csv` ou `json`. Par défaut, la valeur est `parquet`.

>[!NOTE]
>
>Le chemin de sortie complet sera `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

La commande `ALTER TABLE` permet d&#39;ajouter ou de déposer des contraintes de clé Principale ou étrangère ainsi que d&#39;ajouter des colonnes dans le tableau.

#### AJOUTER OU DÉPOSER UNE CONTRAINTE

Les requêtes SQL suivantes montrent des exemples d’ajout ou de suppression de contraintes dans un tableau.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Paramètres**

- `table_name`: Nom de la table que vous modifiez.
- `constraint_name`: Nom de la contrainte que vous souhaitez ajouter ou supprimer.
- `column_name`: Nom de la colonne à laquelle vous ajoutez une contrainte.
- `referenced_table_name`: Nom de la table référencée par la clé étrangère.
- `primary_column_name`: Nom de la colonne référencée par la clé étrangère.

>[!NOTE]
>
>Le schéma de la table doit être unique et ne pas être partagé entre plusieurs tables. En outre, l’espace de noms est obligatoire pour les Principales contraintes de clé.

#### AJOUTER UNE COLONNE

Les requêtes SQL suivantes présentent des exemples d’ajout de colonnes à un tableau.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Paramètres**

- `table_name`: Nom de la table que vous modifiez.
- `column_name`: Nom de la colonne à ajouter.
- `data_type`: Type de données de la colonne à ajouter. Les types de données pris en charge sont les suivants : bigint, char, chaîne, date, datetime, double, double précision, entier, petit, minuscule, minuscule, varchar.

### AFFICHER LES CLÉS PRINCIPAL

La commande `SHOW PRIMARY KEYS` répertorie toutes les Principales contraintes de clé pour la base de données donnée.

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

La commande `SHOW FOREIGN KEYS` répertorie toutes les contraintes de clé étrangère pour la base de données donnée.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```

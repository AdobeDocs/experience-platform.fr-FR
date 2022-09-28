---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query service;syntaxe sql;sql;ctas;CTAS;Créer une table comme sélection
solution: Experience Platform
title: Syntaxe SQL dans Query Service
topic-legacy: syntax
description: Ce document présente la syntaxe SQL prise en charge par Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 5ec37ee797ec297b2e5c275dc0e6091e4ee8ecae
workflow-type: tm+mt
source-wordcount: '3160'
ht-degree: 8%

---

# Syntaxe SQL dans Query Service

Adobe Experience Platform Query Service permet d’utiliser le langage SQL ANSI standard pour `SELECT` et autres commandes limitées. Ce document couvre la syntaxe SQL prise en charge par [!DNL Query Service].

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

where `from_item` peut être l’une des options suivantes :

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

Cette clause peut être utilisée pour lire de manière incrémentielle les données d’une table en fonction des ID d’instantané. Un ID d’instantané est un marqueur de point de contrôle représenté par un nombre de type Long appliqué à un tableau de lac de données chaque fois que des données y sont écrites. Le `SNAPSHOT` se lie à la relation de table à laquelle elle est utilisée.

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

Veuillez noter qu’une `SNAPSHOT` fonctionne avec un alias de table ou de table, mais pas sur une sous-requête ou une vue. A `SNAPSHOT` fonctionne partout où une clause `SELECT` sur une table peut être appliquée.

En outre, vous pouvez utiliser `HEAD` et `TAIL` comme valeurs de décalage spéciales pour les clauses d’instantané. Utilisation `HEAD` fait référence à un décalage avant le premier instantané, tandis que `TAIL` fait référence à un décalage après le dernier instantané.

>[!NOTE]
>
>Si vous interrogez entre deux ID d’instantané et que l’instantané de début a expiré, les deux scénarios suivants peuvent se produire, selon que l’indicateur de comportement de secours facultatif (`resolve_fallback_snapshot_on_failure`) est défini :
>
>- Si l’indicateur facultatif de comportement de secours est défini, Query Service choisit l’instantané disponible le plus ancien, le définit comme instantané de début et renvoie les données entre l’instantané disponible le plus ancien et l’instantané de fin spécifié. Ces données sont **inclusif** de l’instantané disponible le plus ancien.
>
>- Si l’indicateur de comportement de secours facultatif n’est pas défini, une erreur est renvoyée.


### Clause WHERE

Par défaut, les correspondances générées par un `WHERE` sur une clause `SELECT` les requêtes sont sensibles à la casse. Si vous souhaitez que les correspondances ne soient pas sensibles à la casse, vous pouvez utiliser le mot-clé `ILIKE` au lieu de `LIKE`.

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

A `SELECT` La requête qui utilise des jointures présente la syntaxe suivante :

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT et EXCEPT

Le `UNION`, `INTERSECT`, et `EXCEPT` des clauses sont utilisées pour combiner ou exclure des lignes similaires de plusieurs tables :

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREATE TABLE AS SELECT

La syntaxe suivante définit une `CREATE TABLE AS SELECT` Requête (CTAS) :

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

| Paramètres | Description |
| ----- | ----- |
| `schema` | Titre du schéma XDM. Utilisez cette clause uniquement si vous souhaitez utiliser un schéma XDM existant pour le nouveau jeu de données créé par la requête CTAS. |
| `rowvalidation` | (Facultatif) Indique si l’utilisateur souhaite une validation au niveau des lignes de tous les nouveaux lots ingérés pour le jeu de données nouvellement créé. La valeur par défaut est `true`. |
| `select_query` | A `SELECT` . La syntaxe de la variable `SELECT` La requête se trouve dans la variable [Section SELECT query](#select-queries). |

**Exemple**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>L’instruction `SELECT` doit posséder un alias pour les fonctions d’agrégation telles que `COUNT`, `SUM`, `MIN`, etc. En outre, la variable `SELECT` peut être fournie avec ou sans parenthèses (). Vous pouvez fournir un `SNAPSHOT` pour lire les deltas incrémentiels dans la table cible.

## INSERT INTO

Le `INSERT INTO` est définie comme suit :

```sql
INSERT INTO table_name select_query
```

| Paramètres | Description |
| ----- | ----- |
| `table_name` | Nom de la table dans laquelle vous souhaitez insérer la requête. |
| `select_query` | A `SELECT` . La syntaxe de la variable `SELECT` La requête se trouve dans la variable [Section SELECT query](#select-queries). |

**Exemple**

>[!NOTE]
>
>L&#39;exemple suivant est un exemple concret et se résume à des fins pédagogiques.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> Le `SELECT` statement **must not** entre parenthèses (). En outre, le schéma du résultat de la variable `SELECT` doit être conforme à celle de la table définie dans la variable `INSERT INTO` . Vous pouvez fournir un `SNAPSHOT` pour lire les deltas incrémentiels dans la table cible.

La plupart des champs d’un schéma XDM réel sont introuvables au niveau racine et SQL n’autorise pas l’utilisation de la notation par points. Pour obtenir un résultat réaliste en utilisant des champs imbriqués, vous devez mapper chaque champ de votre `INSERT INTO` chemin d’accès.

À `INSERT INTO` chemins imbriqués, utilisez la syntaxe suivante :

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**Exemple**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## DROP TABLE

Le `DROP TABLE` supprime du système de fichiers une table existante et supprime le répertoire associé à la table s’il ne s’agit pas d’une table externe. Si la table n’existe pas, une exception se produit.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Paramètres | Description |
| ------ | ------ |
| `IF EXISTS` | Si cette valeur est spécifiée, aucune exception n’est générée si la table **not** existent. |

## CRÉER UNE BASE DE DONNÉES

Le `CREATE DATABASE` crée une base de données ADLS.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## DROP DABASE

Le `DROP DATABASE` supprime la base de données d’une instance.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Paramètres | Description |
| ------ | ------ |
| `IF EXISTS` | Si cette valeur est spécifiée, aucune exception n’est générée si la base de données **not** existent. |

## DÉPOSER LE SCHÉMA

Le `DROP SCHEMA` supprime un schéma existant.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Paramètres | Description |
| ------ | ------ |
| `IF EXISTS` | Si celle-ci est spécifiée, aucune exception n’est générée si le schéma le fait **not** existent. |
| `RESTRICT` | Valeur par défaut du mode. Si celle-ci est spécifiée, le schéma ne sera supprimé que s’il **ne** contiennent tous les tableaux. |
| `CASCADE` | Si celle-ci est spécifiée, le schéma sera déposé avec toutes les tables présentes dans le schéma. |

## CREATE VIEW

La syntaxe suivante définit une `CREATE VIEW` query :

```sql
CREATE VIEW view_name AS select_query
```

| Paramètres | Description |
| ------ | ------ |
| `view_name` | Nom de la vue à créer. |
| `select_query` | A `SELECT` . La syntaxe de la variable `SELECT` La requête se trouve dans la variable [Section SELECT query](#select-queries). |

**Exemple**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

La syntaxe suivante définit une `DROP VIEW` query :

```sql
DROP VIEW [IF EXISTS] view_name
```

| Paramètres | Description |
| ------ | ------ |
| `IF EXISTS` | Si cette valeur est spécifiée, aucune exception n’est générée si la vue **not** existent. |
| `view_name` | Nom de la vue à supprimer. |

**Exemple**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Bloc anonyme

Un bloc anonyme se compose de deux sections : sections exécutables et de gestion des exceptions. Dans un bloc anonyme, la section exécutable est obligatoire. Toutefois, la section de gestion des exceptions est facultative.

L&#39;exemple suivant montre comment créer un bloc avec une ou plusieurs instructions à exécuter ensemble :

```sql
BEGIN
  statementList
[EXCEPTION exceptionHandler]
END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Voici un exemple utilisant un bloc anonyme.

```sql
BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
END;
```

## Organisation des ressources de données

Il est important d’organiser logiquement vos ressources de données dans le lac de données Adobe Experience Platform au fur et à mesure de leur croissance. Query Service étend les constructions SQL qui vous permettent de regrouper logiquement les ressources de données dans un environnement de test. Cette méthode d’organisation permet le partage de ressources de données entre les schémas sans avoir à les déplacer physiquement.

Les constructions SQL suivantes utilisant la syntaxe SQL standard sont prises en charge pour que vous puissiez organiser vos données de manière logique.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Consultez le guide sur la [organisation logique des ressources de données](../best-practices/organize-data-assets.md) pour plus d’informations sur les bonnes pratiques de Query Service.

## La table existe

Le `table_exists` La commande SQL permet de confirmer si une table existe actuellement dans le système. La commande renvoie une valeur booléenne : `true` si le tableau **existe** et `false` si le tableau **n’existe pas.**

En validant l’existence d’un tableau avant d’exécuter les instructions, la variable `table_exists` Cette fonctionnalité simplifie le processus d’écriture d’un bloc anonyme pour couvrir à la fois les `CREATE` et `INSERT INTO` cas d’utilisation.

La syntaxe suivante définit la variable `table_exists` command :

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## En ligne {#inline}

Le `inline` sépare les éléments d’un tableau de structs et génère les valeurs dans un tableau. Il ne peut être placé que dans la variable `SELECT` ou une liste `LATERAL VIEW`.

Le `inline` function **cannot** être placés dans une liste sélectionnée, là où il existe d’autres fonctions de générateur.

Par défaut, les colonnes générées sont nommées &quot;col1&quot;, &quot;col2&quot;, etc. Si l’expression est `NULL` alors aucune ligne n’est générée.

>[!TIP]
>
>Les noms de colonne peuvent être renommés à l’aide de la variable `RENAME` .

**Exemple**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

L’exemple renvoie les éléments suivants :

```text
1  a Spark SQL
2  b Spark SQL
```

Ce deuxième exemple illustre le concept et l&#39;application de la `inline` fonction . Le modèle de données de l’exemple est illustré dans l’image ci-dessous.

![Schéma de productListItems](../images/sql/productListItems.png)

**Exemple**

```sql
select inline(productListItems) from source_dataset limit 10;
```

Les valeurs provenant de la variable `source_dataset` sont utilisés pour remplir la table cible.

| SKU | _experience | quantity | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot;) | 5 | 10,5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;)&quot;) |  |  |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D, NULL)&quot;)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA,NULL)&quot;)&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] Commandes SQL

La sous-section ci-dessous couvre les commandes Spark SQL prises en charge par Query Service.

### SET

Le `SET` définit une propriété et renvoie la valeur d’une propriété existante ou répertorie toutes les propriétés existantes. Si une valeur est fournie pour une clé de propriété existante, l’ancienne valeur est remplacée.

```sql
SET property_key = property_value
```

| Paramètres | Description |
| ------ | ------ |
| `property_key` | Nom de la propriété que vous souhaitez répertorier ou modifier. |
| `property_value` | La valeur sous laquelle vous souhaitez que la propriété soit définie. |

Pour renvoyer la valeur d’un paramètre, utilisez `SET [property key]` sans `property_value`.

## Commandes PostgreSQL

Les sous-sections ci-dessous couvrent les commandes PostgreSQL prises en charge par Query Service.

### ANALYSER LE TABLEAU

Le `ANALYZE TABLE` calcule les statistiques pour une table sur l’entrepôt accéléré. Les statistiques sont calculées sur les requêtes CTAS ou ITAS exécutées pour un tableau donné sur la boutique accélérée.

**Exemple**

```sql
ANALYZE TABLE <original_table_name>
```

Vous trouverez ci-dessous une liste de calculs statistiques disponibles après l’utilisation de la variable `ANALYZE TABLE` command:-

| Valeurs calculées | Description |
|---|---|
| `field` | Nom de la colonne d’un tableau. |
| `data-type` | Type de données acceptable pour chaque colonne. |
| `count` | Nombre de lignes contenant une valeur non nulle pour ce champ. |
| `distinct-count` | Nombre de valeurs uniques ou distinctes pour ce champ. |
| `missing` | Nombre de lignes dont la valeur de ce champ est nulle. |
| `max` | Valeur maximale du tableau analysé. |
| `min` | Valeur minimale du tableau analysé. |
| `mean` | Valeur moyenne du tableau analysé. |
| `stdev` | Écart type du tableau analysé. |

### BEGIN

Le `BEGIN` ou le `BEGIN WORK` ou `BEGIN TRANSACTION` lance un bloc de transaction. Toutes les instructions saisies après la commande de début sont exécutées dans une seule transaction jusqu’à ce qu’une commande de COMMIT ou ROLLBACK explicite soit donnée. Cette commande est identique à `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CLOSE

Le `CLOSE` libère les ressources associées à un curseur ouvert. Une fois le curseur fermé, aucune opération n’est autorisée sur celui-ci. Un curseur doit être fermé lorsqu’il n’est plus nécessaire.

```sql
CLOSE name
CLOSE ALL
```

If `CLOSE name` est utilisé, `name` représente le nom d’un curseur ouvert qui doit être fermé. If `CLOSE ALL` est utilisée, tous les curseurs ouverts seront fermés.

### DEALLOCATE

Le `DEALLOCATE` vous permet de désaffecter une instruction SQL préparée précédemment. Si vous ne désaffectez pas explicitement une instruction préparée, elle est désaffectée en fin de session. Vous trouverez plus d’informations sur les instructions préparées dans la section [PREPARE, commande](#prepare) .

```sql
DEALLOCATE name
DEALLOCATE ALL
```

If `DEALLOCATE name` est utilisé, `name` représente le nom de l’instruction préparée qui doit être désaffectée. If `DEALLOCATE ALL` est utilisée, toutes les instructions préparées seront désaffectées.

### DECLARE

Le `DECLARE` permet à un utilisateur de créer un curseur qui peut être utilisé pour récupérer un petit nombre de lignes à partir d’une requête plus grande. Une fois le curseur créé, les lignes sont récupérées à l’aide de `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Paramètres | Description |
| ------ | ------ |
| `name` | Le nom du curseur à créer. |
| `query` | A `SELECT` ou `VALUES` qui fournit les lignes à renvoyer par le curseur. |

### EXECUTE

Le `EXECUTE` sert à exécuter une instruction préparée au préalable. Comme les instructions préparées existent uniquement pour la durée d’une session, l’instruction préparée doit avoir été créée par une `PREPARE` exécutée plus tôt dans la session en cours. Vous trouverez plus d’informations sur l’utilisation des instructions préparées dans la section [`PREPARE` command](#prepare) .

Si la variable `PREPARE` qui a créé l’instruction spécifie certains paramètres, un ensemble compatible de paramètres doit être transmis à l’instruction `EXECUTE` . Si ces paramètres ne sont pas transmis, une erreur s’affiche.

```sql
EXECUTE name [ ( parameter ) ]
```

| Paramètres | Description |
| ------ | ------ |
| `name` | Nom de l’instruction préparée à exécuter. |
| `parameter` | La valeur réelle d’un paramètre de l’instruction préparée. Ce paramètre doit être une expression donnant une valeur compatible avec le type de données de ce paramètre, tel que déterminé lors de la création de l’instruction préparée.  S’il existe plusieurs paramètres pour l’instruction préparée, ils sont séparés par des virgules. |

### EXPLAIN

Le `EXPLAIN` affiche le plan d’exécution de l’instruction fournie. Le plan d’exécution indique comment les tables référencées par l’instruction seront analysées.  Si plusieurs tableaux sont référencés, les algorithmes de jointure utilisés pour rassembler les lignes requises de chaque tableau d’entrée s’affichent.

```sql
EXPLAIN statement
```

Utilisez la variable `FORMAT` avec le mot-clé `EXPLAIN` pour définir le format de la réponse.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Paramètres | Description |
| ------ | ------ |
| `FORMAT` | Utilisez la variable `FORMAT` pour spécifier le format de sortie. Les options disponibles sont les suivantes : `TEXT` ou `JSON`. Les sorties autres que text contiennent les mêmes informations que le format de sortie text, mais les programmes pourront plus facilement les analyser. Ce paramètre est défini par défaut sur `TEXT`. |
| `statement` | Quelconque `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`ou `CREATE MATERIALIZED VIEW AS` dont vous souhaitez afficher le plan d’exécution. |

>[!IMPORTANT]
>
>Toute sortie qui `SELECT` L’instruction peut renvoyer est ignorée lors de l’exécution avec la variable `EXPLAIN` mot-clé. D&#39;autres effets secondaires de l&#39;instruction se produisent comme d&#39;habitude.

**Exemple**

L’exemple suivant montre le plan d’une requête simple sur une table avec une seule `integer` et 1 000 lignes :

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### FETCH

Le `FETCH` récupère les lignes à l’aide d’un curseur créé précédemment.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Paramètres | Description |
| ------ | ------ |
| `num_of_rows` | Nombre de lignes à récupérer. |
| `cursor_name` | Le nom du curseur à partir duquel vous récupérez des informations. |

### PREPARE {#prepare}

Le `PREPARE` permet de créer une instruction préparée. Une instruction préparée est un objet côté serveur qui peut être utilisé pour modéliser des instructions SQL similaires.

Les instructions préparées peuvent prendre des paramètres, qui sont des valeurs qui sont substituées dans l’instruction lors de son exécution. Les paramètres sont référencés par position, à l’aide de $1, $2, etc., lors de l’utilisation d’instructions préparées.

Vous pouvez éventuellement spécifier une liste de types de données de paramètre. Si le type de données d’un paramètre n’est pas répertorié, le type peut être déduit du contexte.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Paramètres | Description |
| ------ | ------ |
| `name` | Nom de l’instruction préparée. |
| `data_type` | Types de données des paramètres de l’instruction préparée. Si le type de données d’un paramètre n’est pas répertorié, le type peut être déduit du contexte. Si vous devez ajouter plusieurs types de données, vous pouvez les ajouter dans une liste séparée par des virgules. |

### ROLLBACK

Le `ROLLBACK` annule la transaction en cours et ignore toutes les mises à jour effectuées par la transaction.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

Le `SELECT INTO` crée une nouvelle table et la remplit avec des données calculées par une requête. Les données ne sont pas renvoyées au client, comme c’est le cas avec une `SELECT` . Les noms et les types de données des colonnes de la nouvelle table sont associés aux colonnes de sortie de la colonne `SELECT` .

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

Vous trouverez plus d’informations sur les paramètres de requête SELECT standard dans la section [Section de requête SELECT](#select-queries). Cette section répertorie uniquement les paramètres qui sont exclusifs à la variable `SELECT INTO` .

| Paramètres | Description |
| ------ | ------ |
| `TEMPORARY` ou `TEMP`. | Paramètre facultatif. Si spécifié, la table créée sera une table temporaire. |
| `UNLOGGED` | Paramètre facultatif. Si spécifié, la table créée sera une table non enregistrée. Vous trouverez plus d’informations sur les tables non enregistrées dans la section [Documentation PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | Nom de la table à créer. |

**Exemple**

La requête suivante crée une nouvelle table. `films_recent` constitué uniquement des entrées récentes de la table `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

Le `SHOW` affiche la configuration actuelle des paramètres d’exécution. Ces variables peuvent être définies à l’aide de la variable `SET` en modifiant l’instruction `postgresql.conf` fichier de configuration, via le `PGOPTIONS` Variable d’environnement (lors de l’utilisation de libpq ou d’une application basée sur libpq) ou par le biais d’indicateurs de ligne de commande lors du démarrage du serveur Postgres.

```sql
SHOW name
SHOW ALL
```

| Paramètres | Description |
| ------ | ------ |
| `name` | Nom du paramètre d’exécution dont vous souhaitez obtenir des informations. Les valeurs possibles du paramètre d’exécution sont les suivantes :<br>`SERVER_VERSION`: Ce paramètre affiche le numéro de version du serveur.<br>`SERVER_ENCODING`: Ce paramètre affiche le codage du jeu de caractères côté serveur.<br>`LC_COLLATE`: Ce paramètre affiche les paramètres régionaux de la base de données pour le classement (tri de texte).<br>`LC_CTYPE`: Ce paramètre affiche le paramètre régional de la base de données pour la classification des caractères.<br>`IS_SUPERUSER`: Ce paramètre indique si le rôle actuel possède des privilèges de super-utilisateur. |
| `ALL` | Affichez les valeurs de tous les paramètres de configuration avec des descriptions. |

**Exemple**

La requête suivante affiche la configuration actuelle du paramètre . `DateStyle`.

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

Le `COPY` duplique la sortie de tout `SELECT` à un emplacement spécifié. L’utilisateur doit avoir accès à cet emplacement pour que cette commande réussisse.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Paramètres | Description |
| ------ | ------ |
| `query` | La requête que vous souhaitez copier. |
| `format_name` | Format dans lequel vous souhaitez copier la requête. Le `format_name` peut être l’un des `parquet`, `csv`ou `json`. Par défaut, la valeur est `parquet`. |

>[!NOTE]
>
>Le chemin de sortie complet sera : `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE {#alter-table}

Le `ALTER TABLE` vous permet d&#39;ajouter ou de déposer des contraintes de clé Principale ou étrangère, ainsi que d&#39;ajouter des colonnes dans le tableau.


#### AJOUTER OU DÉPOSER UNE CONTRAINTE

Les requêtes SQL suivantes montrent des exemples d’ajout ou de suppression de contraintes dans un tableau.

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| Paramètres | Description |
| ------ | ------ |
| `table_name` | Nom de la table que vous modifiez. |
| `column_name` | Nom de la colonne à laquelle vous ajoutez une contrainte. |
| `referenced_table_name` | Nom de la table référencée par la clé étrangère. |
| `primary_column_name` | Nom de la colonne référencée par la clé étrangère. |


>[!NOTE]
>
>Le schéma de la table doit être unique et ne pas être partagé entre plusieurs tables. En outre, l’espace de noms est obligatoire pour les contraintes de clé Principale, d’identité Principale et d’identité.

#### Ajout ou suppression d’identités Principales et secondaires

Le `ALTER TABLE` vous permet d’ajouter ou de supprimer des contraintes pour les colonnes des tables d’identités Principales et secondaires directement via SQL.

Les exemples suivants ajoutent une identité Principale et une identité secondaire en ajoutant des contraintes.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Les identités peuvent également être supprimées en supprimant des contraintes, comme illustré dans l’exemple ci-dessous.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Consultez le document sur [définition des identités dans des jeux de données ad hoc](../data-governance/ad-hoc-schema-identities.md) pour plus d’informations.

#### AJOUTER UNE COLONNE

Les requêtes SQL suivantes présentent des exemples d’ajout de colonnes à un tableau.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Types de données pris en charge

Le tableau suivant répertorie les types de données acceptés pour l’ajout de colonnes à un tableau avec [!DNL Postgres SQL], XDM et la variable [!DNL Accelerated Database Recovery] (MARC) dans Azure SQL.

| --- | Client PSQL | XDM | MARC | Description |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Type de données numérique utilisé pour stocker des entiers volumineux allant de -9 223 372 036 854 775 807 à 9 223 372 036 854 775 807 en 8 octets. |
| 2 | `integer` | `int4` | `integer` | Type de données numérique utilisé pour stocker des entiers compris entre -2 147 483 648 et 2 147 483 647 en 4 octets. |
| 3 | `smallint` | `int2` | `smallint` | Type de données numérique utilisé pour stocker des entiers compris entre -32 768 et 215-1 32 767 en 2 octets. |
| 4 | `tinyint` | `int1` | `tinyint` | Type de données numérique utilisé pour stocker des entiers compris entre 0 et 255 sur 1 octet. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Type de données de caractère de taille variable. `varchar` est mieux utilisée lorsque les tailles des entrées de données de colonne varient considérablement. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` et `FLOAT` sont des synonymes valides pour `DOUBLE PRECISION`. `double precision` est un type de données à virgule flottante. Les valeurs de points flottants sont stockées dans 8 octets. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` est un synonyme valide pour `double precision`.`double precision` est un type de données à virgule flottante. Les valeurs de points flottants sont stockées dans 8 octets. |
| 8 | `date` | `date` | `date` | Le `date` Les types de données sont des valeurs de date de calendrier stockées sur 4 octets, sans informations d’horodatage. La plage de dates valides va de 01-01-0001 à 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Type de données utilisé pour stocker un instant dans le temps exprimé sous la forme d’une date et d’une heure calendaires. `datetime` inclut les qualificateurs de : année, mois, jour, heure, seconde et fraction. A `datetime` La déclaration peut inclure n’importe quel sous-ensemble de ces unités temporelles qui sont jointes dans cette séquence, ou même ne comprendre qu’une seule unité temporelle. |
| 10 | `char(len)` | `string` | `char(len)` | Le `char(len)` Le mot-clé est utilisé pour indiquer que l’élément est un caractère de longueur fixe. |

#### AJOUT D’UN SCHÉMA

La requête SQL suivante montre un exemple d&#39;ajout d&#39;une table à une base de données/un schéma.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Il n’est pas possible d’ajouter des tableaux et des vues ADLS aux bases de données/schémas DWH.


#### SUPPRESSION DU SCHÉMA

La requête SQL suivante illustre un exemple de suppression d’une table d’une base de données/d’un schéma.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Les tables et vues DWH ne peuvent pas être supprimées des bases de données/schémas DWH liés physiquement.


**Paramètres**

| Paramètres | Description |
| ------ | ------ |
| `table_name` | Nom de la table que vous modifiez. |
| `column_name` | Nom de la colonne à ajouter. |
| `data_type` | Type de données de la colonne à ajouter. Les types de données pris en charge sont les suivants : bigint, char, chaîne, date, datetime, double, double précision, entier, petit, minuscule, minuscule, varchar. |

### AFFICHER LES CLÉS PRINCIPAL

Le `SHOW PRIMARY KEYS` liste toutes les Principales contraintes de clé pour la base de données donnée.

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

Le `SHOW FOREIGN KEYS` liste toutes les contraintes de clé étrangère pour la base de données donnée.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### AFFICHER LES GROUPES DE DONNÉES

Le `SHOW DATAGROUPS` renvoie une table de toutes les bases de données associées. Pour chaque base de données, le tableau comprend le schéma, le type de groupe, le type enfant, le nom enfant et l’ID enfant.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### AFFICHER LES GROUPES DE DONNÉES POUR LE tableau

Le `SHOW DATAGROUPS FOR` La commande &#39;table_name&#39; renvoie une table de toutes les bases de données associées contenant le paramètre comme son enfant. Pour chaque base de données, le tableau comprend le schéma, le type de groupe, le type enfant, le nom enfant et l’ID enfant.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Paramètres**

- `table_name`: Nom de la table pour laquelle vous souhaitez trouver les bases de données associées.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```

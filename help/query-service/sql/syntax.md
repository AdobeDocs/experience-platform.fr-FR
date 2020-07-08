---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: syntaxe SQL
topic: syntax
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 1%

---


# syntaxe SQL

Requête Service permet d&#39;utiliser le SQL ANSI standard pour `SELECT` les instructions et autres commandes limitées. Ce document présente la syntaxe SQL prise en charge par Requête Service.

## Définir une requête SELECT

La syntaxe suivante définit une `SELECT` requête prise en charge par Requête Service :

```
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

où `from_item` peut être l&#39;un des :

```
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

et `grouping_element` peut être l&#39;un des suivants :

```
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

et `with_query` est :

```
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### clause WHERE ILIKE

Le mot clé ILIKE peut être utilisé à la place de LIKE pour faire des correspondances sur la clause WHERE de la requête SELECT sans distinction de la casse.

```
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La logique des clauses LIKE et ILIKE est la suivante :
- ```WHERE condition LIKE pattern```, ```~~``` est équivalent à pattern
- ```WHERE condition NOT LIKE pattern```, ```!~~``` est équivalent à pattern
- ```WHERE condition ILIKE pattern```, ```~~*``` équivalent au modèle
- ```WHERE condition NOT ILIKE pattern```, ```!~~*``` équivalent au modèle


#### Exemple

```
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Renvoie les clients dont les noms commencent par &quot;A&quot; ou &quot;a&quot;.

## JOINS

Une `SELECT` requête utilisant des jointures a la syntaxe suivante :

```
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNION, INTERSECT et EXCEPT

Les clauses `UNION`, `INTERSECT`et `EXCEPT` sont prises en charge pour combiner ou exclure des lignes similaires de plusieurs tables :

```
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## CRÉER UN TABLEAU COMME SÉLECTIONNÉ

La syntaxe suivante définit une requête `CREATE TABLE AS SELECT` (CTAS) prise en charge par Requête Service :

```
CREATE TABLE table_name [ WITH (schema='target_schema_title') ] AS (select_query)
```

où `target_schema_title` est le titre du schéma XDM. Utilisez cette clause uniquement si vous souhaitez utiliser un schéma XDM existant pour le nouveau jeu de données créé par la requête CTAS.

et `select_query` est une `SELECT` instruction dont la syntaxe est définie ci-dessus dans ce document.


### Exemple

```
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Veuillez noter que pour une requête donnée de l&#39;ATPC :

1. L&#39; `SELECT` instruction doit avoir un alias pour les fonctions d&#39;agrégat telles que `COUNT`, `SUM`, `MIN`, etc.
2. L&#39; `SELECT` instruction peut être fournie avec ou sans parenthèses ().

## INSÉRER DANS

La syntaxe suivante définit une `INSERT INTO` requête prise en charge par Requête Service :

```
INSERT INTO table_name select_query
```

où `select_query` est une `SELECT` instruction dont la syntaxe est définie ci-dessus dans ce document.

### Exemple

```
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Veuillez noter que pour un INSERTION EN requête donné :

1. L&#39; `SELECT` instruction NE DOIT PAS être placée entre parenthèses ().
2. Le schéma du résultat de l&#39; `SELECT` instruction doit être conforme à celui du tableau défini dans l&#39; `INSERT INTO` instruction.

### TABLEAU DROP

Déposez une table et supprimez le répertoire associé à la table du système de fichiers s&#39;il ne s&#39;agit pas d&#39;une table EXTERNE. Si la table à déposer n&#39;existe pas, une exception se produit.

```
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Paramètres

- `IF EXISTS`: Si la table n&#39;existe pas, rien ne se passe
- `TEMP`: Table temporaire

## CREATE VUE

La syntaxe suivante définit une `CREATE VIEW` requête prise en charge par Requête Service :

```
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

Où `view_name` est le nom de la vue à créer et `select_query` est une `SELECT` instruction, dont la syntaxe est définie ci-dessus dans ce document.

Exemple :

```
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### VUE DROP

La syntaxe suivante définit une `DROP VIEW` requête prise en charge par Requête Service :

```
DROP VIEW [IF EXISTS] view_name
```

Où `view_name` est le nom de la vue à supprimer

Exemple :

```
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Commandes Spark SQL

### DÉFINIR

Définissez une propriété, renvoyez la valeur d’une propriété existante ou liste toutes les propriétés existantes. Si une valeur est fournie pour une clé de propriété existante, l’ancienne valeur est remplacée.

```
SET property_key [ To | =] property_value
```

Pour renvoyer la valeur de n’importe quel paramètre, utilisez `SHOW [setting name]`.

## PostgreSQL, commande

### COMMENCER

Cette commande est analysée et la commande terminée est renvoyée au client. Il s’agit de la même commande que la `START TRANSACTION` commande.

```
BEGIN [ TRANSACTION ]
```

#### Paramètres

- `TRANSACTION`: Mots-clés facultatifs. Écoute-le, aucune action n&#39;est entreprise à ce sujet.

### CLOSE

`CLOSE` libère les ressources associées à un curseur ouvert. Une fois le curseur fermé, aucune opération ultérieure n’est autorisée. Un curseur doit être fermé lorsqu’il n’est plus nécessaire.

```
CLOSE { name }
```

#### Paramètres

- `name`: nom d’un curseur ouvert à fermer.

### COMMIT

Aucune action n&#39;est effectuée dans Requête Service en réponse à la déclaration de transaction de validation.

```
COMMIT [ WORK | TRANSACTION ]
```

#### Paramètres

- `WORK`
- `TRANSACTION`: Mots-clés facultatifs. Ils n&#39;ont aucun effet.

### DÉALLOUER

Permet `DEALLOCATE` de délocaliser une instruction SQL préparée précédemment. Si vous ne délocalisez pas explicitement une instruction préparée, elle est délocalisée à la fin de la session.

```
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Paramètres

- `Prepare`: Ce mot-clé est ignoré.
- `name`: Nom de l&#39;instruction préparée à délocaliser.
- `ALL`: Dédiez tous les états préparés.

### DÉCLARER

`DECLARE` permet à un utilisateur de créer des curseurs, qui peuvent être utilisés pour récupérer un petit nombre de rangées à la fois à l’extérieur d’une requête plus grande. Une fois le curseur créé, les lignes sont extraites à partir de celui-ci à l’aide `FETCH`.

```
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Paramètres

- `name`: Nom du curseur à créer.
- `WITH HOLD`: Indique que le curseur peut continuer à être utilisé une fois la transaction qui l’a créée validée.
- `query`: Commande `SELECT` ou `VALUES` qui fournit les lignes à renvoyer par le curseur.

### EXÉCUTER

`EXECUTE` sert à exécuter une instruction préparée précédemment. Étant donné que les instructions préparées n&#39;existent que pour la durée d&#39;une session, l&#39;instruction préparée doit avoir été créée par une `PREPARE` instruction exécutée plus tôt dans la session en cours.

Si l&#39; `PREPARE` instruction qui a créé l&#39;instruction spécifiait certains paramètres, un ensemble de paramètres compatible doit être transmis à l&#39; `EXECUTE` instruction, sinon une erreur est levée. Notez que les instructions préparées (contrairement aux fonctions) ne sont pas surchargées en fonction du type ou du nombre de leurs paramètres. Le nom d&#39;une instruction préparée doit être unique au sein d&#39;une session de base de données.

```
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Paramètres

- `name`: Nom de l&#39;instruction préparée à exécuter.
- `parameter`: Valeur réelle d&#39;un paramètre à l&#39;instruction préparée. Il doit s&#39;agir d&#39;une expression qui produit une valeur compatible avec le type de données de ce paramètre, comme déterminé lors de la création de l&#39;instruction préparée.

### EXPLIQUER

Cette commande affiche le plan d&#39;exécution généré par le planificateur PostgreSQL pour l&#39;instruction fournie. Le plan d&#39;exécution montre comment les tables référencées par l&#39;instruction seront analysées — par analyse séquentielle simple, analyse d&#39;index, etc. — et si plusieurs tables sont référencées, quels algorithmes de jointure sont utilisés pour rassembler les lignes requises de chaque table d&#39;entrée.

La partie la plus critique de l&#39;affichage est l&#39;estimation du coût d&#39;exécution des instructions, qui est l&#39;estimation du planificateur quant au temps nécessaire à l&#39;exécution de la déclaration (mesuré en unités de coût arbitraires, mais habituellement moyennes récupérations de pages de disque). En fait, deux nombres sont affichés : le coût de début avant la première ligne peut être renvoyé et le coût total pour renvoyer toutes les lignes. Pour la plupart des requêtes, c&#39;est le coût total qui importe, mais dans les contextes tels qu&#39;une sous-requête dans EXISTS, le planificateur choisit le coût de début le plus faible au lieu du coût total le plus faible (parce que l&#39;exécuteur s&#39;arrête après avoir obtenu une ligne, de toute façon). En outre, si vous limitez le nombre de lignes à renvoyer avec une `LIMIT` clause, le planificateur effectue une interpolation appropriée entre les coûts du point de terminaison pour estimer quel plan est vraiment le moins cher.

L&#39; `ANALYZE` option entraîne l&#39;exécution de l&#39;instruction, et non pas seulement la planification. Ensuite, des statistiques d&#39;exécution réelles sont ajoutées à l&#39;affichage, y compris le temps total passé en revue dans chaque noeud de plan (en millisecondes) et le nombre total de lignes renvoyées. Cela est utile pour voir si les estimations du planificateur sont proches de la réalité.

```
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Paramètres

- `ANALYZE`: Exécutez la commande et affichez les heures d&#39;exécution réelles et d&#39;autres statistiques. Ce paramètre est défini par défaut sur `FALSE`.
- `FORMAT`: Spécifiez le format de sortie, qui peut être TEXT, XML, JSON ou YAML. La sortie non textuelle contient les mêmes informations que le format de sortie textuelle, mais est plus facile à analyser pour les programmes. Ce paramètre est défini par défaut sur `TEXT`.
- `statement`: Toute `SELECT`instruction, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`,  ou  dont vous souhaitez afficher le plan d’exécution.`CREATE TABLE AS``CREATE MATERIALIZED VIEW AS`

>[!IMPORTANT]
>
>Gardez à l’esprit que l’instruction est réellement exécutée lorsque l’ `ANALYZE` option est utilisée. Bien que `EXPLAIN` ignore toute sortie qu&#39;un `SELECT` utilisateur renvoie, d&#39;autres effets secondaires de l&#39;instruction se produisent comme d&#39;habitude.

#### Exemple

Pour afficher le plan d&#39;une requête simple sur un tableau avec une seule `integer` colonne et 1 000 lignes :

```
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` récupère les lignes à l’aide d’un curseur créé précédemment.

Un curseur est associé à une position, qui est utilisée par `FETCH`. La position du curseur peut être antérieure à la première ligne du résultat de la requête, à une ligne particulière du résultat ou à la dernière ligne du résultat. Une fois créé, un curseur est placé avant la première rangée. Après avoir récupéré certaines lignes, le curseur est placé sur la ligne la plus récemment récupérée. Si `FETCH` s’exécute à partir de la fin des lignes disponibles, le curseur est placé à gauche après la dernière ligne. S’il n’existe aucune ligne de ce type, un résultat vide est renvoyé et les curseurs sont positionnés avant la première ou après la dernière ligne, selon le cas.

```
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Paramètres

- `num_of_rows`: Constante entière pouvant être signée, déterminant l’emplacement ou le nombre de lignes à récupérer.
- `cursor_name`: Nom du curseur ouvert.

### PRÉPARATION

`PREPARE` crée une instruction préparée. Une instruction préparée est un objet côté serveur qui peut être utilisé pour optimiser les performances. Lorsque l&#39; `PREPARE` instruction est exécutée, l&#39;instruction spécifiée est analysée, analysée et réécrite. Lorsqu&#39;une `EXECUTE` commande est émise par la suite, l&#39;instruction préparée est planifiée et exécutée. Cette division du travail évite le travail répétitif d&#39;analyse d&#39;analyse, tout en permettant au plan d&#39;exécution de dépendre des valeurs de paramètres spécifiques fournies.

Les instructions préparées peuvent prendre des paramètres, des valeurs qui sont substituées dans l&#39;instruction lors de son exécution. Lors de la création de l&#39;instruction préparée, reportez-vous aux paramètres par position, en utilisant $1, $2, etc. Une liste correspondante de types de données de paramètre peut éventuellement être spécifiée. Lorsque le type de données d&#39;un paramètre n&#39;est pas spécifié ou déclaré inconnu, le type est déduit du contexte dans lequel le paramètre est référencé pour la première fois, si possible. Lors de l&#39;exécution de l&#39;instruction, spécifiez les valeurs réelles de ces paramètres dans l&#39; `EXECUTE` instruction.

Les instructions préparées ne durent que pendant la durée de la session de base de données en cours. Lorsque la session se termine, l&#39;instruction préparée est oubliée, elle doit donc être recréée avant d&#39;être réutilisée. Cela signifie également qu&#39;une seule instruction préparée ne peut pas être utilisée par plusieurs clients de base de données simultanés. Cependant, chaque client peut créer sa propre instruction préparée à utiliser. Les instructions préparées peuvent être nettoyées manuellement à l&#39;aide de la `DEALLOCATE` commande.

Les instructions préparées présentent potentiellement le plus grand avantage en termes de performances lorsqu’une seule session est utilisée pour exécuter un grand nombre d’instructions similaires. La différence de performance est particulièrement importante si les instructions sont complexes à planifier ou à réécrire, par exemple si la requête implique une jointure de plusieurs tables ou requiert l&#39;application de plusieurs règles. Si l&#39;instruction est relativement simple à planifier et à réécrire mais relativement coûteuse à exécuter, l&#39;avantage de performance des instructions préparées est moins visible.

```
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Paramètres

- `name`: Un nom arbitraire donné à cette déclaration préparée en particulier. Il doit être unique au cours d&#39;une seule session et est ensuite utilisé pour exécuter ou délocaliser une instruction préparée précédemment.
- `data-type`: Type de données d&#39;un paramètre à l&#39;instruction préparée. Si le type de données d’un paramètre particulier n’est pas spécifié ou est spécifié comme inconnu, il est déduit du contexte dans lequel le paramètre est référencé pour la première fois. Pour faire référence aux paramètres de l&#39;instruction préparée elle-même, utilisez $1, $2, etc.


### RETOUR

`ROLLBACK` annule la transaction en cours et annule toutes les mises à jour effectuées par la transaction.

```
ROLLBACK [ WORK ]
```

#### Paramètres

- `WORK`

### SÉLECTIONNER DANS

`SELECT INTO` crée un tableau et le remplit avec des données calculées par une requête. Les données ne sont pas renvoyées au client, comme c&#39;est le cas avec une `SELECT`valeur normale. Les colonnes de la nouvelle table ont les noms et les types de données associés aux colonnes de sortie du `SELECT`.

```
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

- `TEMPORARAY` ou `TEMP`: Le cas échéant, la table est créée en tant que table temporaire.
- `UNLOGGED:` si elle est spécifiée, la table est créée en tant que table non enregistrée.
- `new_table` Nom (éventuellement qualifié par schéma) de la table à créer.

#### Exemple

Créez un nouveau tableau `films_recent` composé uniquement des entrées récentes du tableau `films`:

```
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### AFFICHER

`SHOW` affiche le paramètre actuel des paramètres d’exécution. Ces variables peuvent être définies à l&#39;aide de l&#39; `SET` instruction, en modifiant le fichier de configuration postgresql.conf, par l&#39;intermédiaire de la variable `PGOPTIONS` environnementale (lors de l&#39;utilisation de libpq ou d&#39;une application libpq), ou par l&#39;intermédiaire des indicateurs de ligne de commande lors du démarrage du serveur postgres.

```
SHOW name
```

#### Paramètres

- `name` :
   - `SERVER_VERSION`: Affiche le numéro de version du serveur.
   - `SERVER_ENCODING`: Affiche le codage du jeu de caractères côté serveur. Actuellement, ce paramètre peut être affiché mais pas défini, car le codage est déterminé au moment de la création de la base de données.
   - `LC_COLLATE`: Affiche le paramètre régional de la base de données pour l’assemblage (ordre de texte). Actuellement, ce paramètre peut être affiché mais pas défini, car il est déterminé au moment de la création de la base de données.
   - `LC_CTYPE`: Affiche les paramètres régionaux de la base de données pour la classification des caractères. Actuellement, ce paramètre peut être affiché mais pas défini, car il est déterminé au moment de la création de la base de données.
      `IS_SUPERUSER`: True si le rôle actuel possède des privilèges de super-utilisateur.
- `ALL`: Affichez les valeurs de tous les paramètres de configuration avec des descriptions.

#### Exemple

Afficher le paramètre actuel `DateStyle`

```
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### TRANSACTION DÉBUT

Cette commande est analysée et renvoie la commande terminée au client. Il s’agit de la même commande que la `BEGIN` commande.

```
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

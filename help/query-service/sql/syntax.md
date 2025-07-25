---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;syntaxe sql;sql;ctas;CTAS;Créer une table comme sélectionner
solution: Experience Platform
title: Syntaxe SQL dans Query Service
description: Ce document détaille et explique la syntaxe SQL prise en charge par Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: cd4734b2d837bc04e1de015771a74a48ff37173f
workflow-type: tm+mt
source-wordcount: '4686'
ht-degree: 4%

---

# Syntaxe SQL dans Query Service

Vous pouvez utiliser le langage SQL ANSI standard pour les instructions `SELECT` et d’autres commandes limitées dans Adobe Experience Platform Query Service. Ce document couvre la syntaxe SQL prise en charge par [!DNL Query Service].

## Requêtes SELECT {#select-queries}

La syntaxe suivante définit une requête `SELECT` prise en charge par [!DNL Query Service] :

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

La section Onglets ci-dessous présente les options disponibles pour les mots-clés FROM, GROUP et WITH.

>[!BEGINTABS]

>[!TAB `from_item`]

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

>[!TAB `grouping_element`]

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

>[!TAB `with_query`]

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

>[!ENDTABS]

Les sous-sections suivantes fournissent des détails sur les clauses supplémentaires que vous pouvez utiliser dans vos requêtes, à condition qu’elles respectent le format décrit ci-dessus.

### Clause SNAPSHOT

Cette clause peut être utilisée pour lire de manière incrémentielle les données d’une table en fonction des ID d’instantané. Un ID d’instantané est un marqueur de point de contrôle représenté par un nombre de type Long appliqué à une table de lac de données chaque fois que des données y sont écrites. La clause `SNAPSHOT` s&#39;attache à la relation de table en regard de laquelle elle est utilisée.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Exemple

```sql
SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT AS OF end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN 'HEAD' AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND 'TAIL';

SELECT * FROM (SELECT id FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id) C;

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

>[!NOTE]
>
>Lors de l’utilisation de `HEAD` ou `TAIL` dans une clause de `SNAPSHOT`, vous devez les placer entre guillemets simples (par exemple, « HEAD », « TAIL »). Leur utilisation sans guillemets génère une erreur de syntaxe.

Le tableau ci-dessous explique la signification de chaque option de syntaxe dans la clause SNAPSHOT.

| Syntaxe | Signification |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | Lit les données à partir de l’ID d’instantané spécifié (exclusif). |
| `AS OF end_snapshot_id` | Lit les données telles qu’elles étaient à l’ID d’instantané spécifié (inclus). |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | Lit les données comprises entre les ID d’instantané de début et de fin spécifiés. Il est exclusif de la `start_snapshot_id` et inclusif de la `end_snapshot_id`. |
| `BETWEEN HEAD AND start_snapshot_id` | Lit les données du début (avant le premier instantané) à l’ID d’instantané de début spécifié (inclus). Notez que cette opération renvoie uniquement des lignes dans `start_snapshot_id`. |
| `BETWEEN end_snapshot_id AND TAIL` | Lit les données juste après la `end_snapshot_id` spécifiée jusqu’à la fin du jeu de données (à l’exclusion de l’ID d’instantané). Cela signifie que si `end_snapshot_id` est le dernier instantané du jeu de données, la requête ne renvoie aucune ligne, car il n’existe aucun instantané au-delà de ce dernier. |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | Lit les données à partir de l’ID d’instantané spécifié à partir de `table_to_be_queried` et le joint avec les données de `table_to_be_joined` telles qu’elles étaient au `your_chosen_snapshot_id`. La jointure est basée sur les identifiants correspondants des colonnes d&#39;identifiants des deux tables jointes. |

Une clause `SNAPSHOT` fonctionne avec une table ou un alias de table, mais pas au-dessus d&#39;une sous-requête ou d&#39;une vue. Une clause `SNAPSHOT` fonctionne partout où une requête `SELECT` sur une table peut être appliquée.

En outre, vous pouvez utiliser `HEAD` et `TAIL` comme valeurs de décalage spéciales pour les clauses de cliché. L&#39;utilisation de `HEAD` fait référence à un décalage avant le premier instantané, tandis que `TAIL` fait référence à un décalage après le dernier instantané.

>[!NOTE]
>
>Si vous effectuez une requête entre deux identifiants d’instantané, les deux scénarios suivants peuvent se produire si l’instantané de début a expiré et que l’indicateur de comportement de secours facultatif (`resolve_fallback_snapshot_on_failure`) est défini :
>
>- Si l’indicateur de comportement de secours facultatif est défini, Query Service choisit l’instantané disponible le plus ancien, le définit comme instantané de début et renvoie les données comprises entre l’instantané disponible le plus ancien et l’instantané de fin spécifié. Ces données **inclues** de l’instantané disponible le plus ancien.

### Clause WHERE

Par défaut, les correspondances générées par une clause `WHERE` sur une requête `SELECT` sont sensibles à la casse. Si vous souhaitez que les correspondances ne respectent pas la casse, vous pouvez utiliser le mot-clé `ILIKE` au lieu de `LIKE`.

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

Cette requête renvoie des clients dont le nom commence par « A » ou « a ».

### JOINTURE

Une requête `SELECT` qui utilise des jointures possède la syntaxe suivante :

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT et EXCEPT

Les clauses `UNION`, `INTERSECT` et `EXCEPT` sont utilisées pour combiner ou exclure des lignes similaires de deux tableaux ou plus :

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREATE TABLE AS SELECT {#create-table-as-select}

Utilisez la commande `CREATE TABLE AS SELECT` (CTAS) pour matérialiser les résultats d’une requête `SELECT` dans une nouvelle table. Cela s’avère utile pour créer des jeux de données transformés, effectuer des agrégations ou prévisualiser des données issues de l’ingénierie des fonctionnalités avant de les utiliser dans un modèle.

Si vous êtes prêt à entraîner un modèle à l&#39;aide de fonctions transformées, consultez la [documentation Modèles](../advanced-statistics/models.md) pour obtenir des conseils sur l&#39;utilisation de `CREATE MODEL` avec la clause `TRANSFORM`.

Vous pouvez éventuellement inclure une clause `TRANSFORM` pour appliquer une ou plusieurs fonctions d’ingénierie des fonctionnalités directement dans l’instruction CTAS. Utilisez `TRANSFORM` pour examiner les résultats de votre logique de transformation avant l’entraînement du modèle.

Cette syntaxe s&#39;applique à la fois aux tables permanentes et temporaires.

```sql
CREATE TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

```sql
CREATE TEMP TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

| Paramètre | Description |
| ----- | ----- |
| `schema` | Titre du schéma XDM. N’utilisez cette clause que si vous souhaitez associer la nouvelle table à un schéma XDM existant. |
| `rowvalidation` | (Facultatif) Active la validation au niveau des lignes pour chaque lot ingéré dans le jeu de données. La valeur par défaut est « true ». |
| `label` | (Facultatif) Utilisez la valeur `PROFILE` pour étiqueter le jeu de données comme étant activé pour l’ingestion de profils. |
| `transform` | (Facultatif) Applique des transformations d’ingénierie des fonctionnalités (telles que l’indexation de chaîne, l’encodage à chaud ou TF-IDF) avant de matérialiser le jeu de données. Cette clause est utilisée pour prévisualiser les fonctions transformées. Pour plus d’informations[&#128279;](#transform) consultez la documentation de la clause `TRANSFORM` . |
| `select_query` | Instruction `SELECT` standard qui définit le jeu de données. Pour plus d’informations[&#128279;](#select-queries) consultez la section `SELECT` des requêtes . |

>[!NOTE]
>
>L&#39;instruction `SELECT` doit inclure un alias pour les fonctions d&#39;agrégat telles que `COUNT`, `SUM` ou `MIN`. Vous pouvez fournir la requête `SELECT` avec ou sans parenthèses. Ceci s&#39;applique que la clause `TRANSFORM` soit utilisée ou non.

**Exemples**

Exemple de base utilisant une clause `TRANSFORM` pour prévisualiser quelques fonctionnalités techniques :

```sql
CREATE TABLE ctas_transform_table_vp14 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review_e2e_DND;
```

Exemple plus avancé avec plusieurs étapes de transformation :

```sql
CREATE TABLE ctas_transform_table 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

Exemple de table temporaire :

```sql
CREATE TEMP TABLE ctas_transform_table 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

#### Limites et comportement {#limitations-and-behavior}

Gardez à l’esprit les restrictions suivantes lors de l’utilisation de la clause `TRANSFORM` avec `CREATE TABLE` ou `CREATE TEMP TABLE` :

- Si une fonction de transformation génère une sortie vectorielle, elle est automatiquement convertie en tableau.
- Par conséquent, les tableaux créés à l’aide de `TRANSFORM` ne peuvent pas être utilisés directement dans les instructions `CREATE MODEL`. Vous devez redéfinir la logique de transformation lors de la création du modèle pour générer les vecteurs de fonction appropriés.
- Les transformations ne sont appliquées que lors de la création de la table. Les nouvelles données insérées dans la table avec `INSERT INTO` ne sont **pas automatiquement transformées**. Pour appliquer des transformations à de nouvelles données, vous devez recréer la table à l’aide de `CREATE TABLE AS SELECT` avec la clause `TRANSFORM`.
- Cette méthode est destinée à prévisualiser et valider les transformations à un moment donné, et non à créer des pipelines de transformation réutilisables.

>[!NOTE]
>
>Pour plus d’informations sur les fonctions de transformation disponibles et leurs types de sortie, consultez [Types de données de sortie de transformation de fonction](../advanced-statistics/feature-transformation.md#available-transformations).


### Clause TRANSFORM {#transform}

Utilisez la clause `TRANSFORM` pour appliquer une ou plusieurs fonctions d&#39;ingénierie des fonctionnalités à un jeu de données avant la formation du modèle ou la création de la table. Cette clause vous permet de prévisualiser, valider ou définir la forme exacte de vos fonctions d&#39;entrée.

La clause `TRANSFORM` peut être utilisée dans les instructions suivantes :

- `CREATE MODEL`
- `CREATE TABLE`
- `CREATE TEMP TABLE`

Consultez la [documentation des modèles](../advanced-statistics/models.md) pour obtenir des instructions détaillées sur l’utilisation de CREATE MODEL, notamment sur la définition des transformations, la définition des options de modèle et la configuration des données d’identification.

Pour une utilisation avec `CREATE TABLE`, consultez la section [CREATE TABLE AS SELECT](#create-table-as-select).

#### EXEMPLE DE CRÉATION DE MODÈLE

```sql
CREATE MODEL review_model
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) AS ohe_add_comments,
  tokenizer(comments) AS token_comments,
  stop_words_remover(token_comments, array('and','very','much')) AS stp_token,
  ngram(stp_token, 3) AS ngram_token,
  tf_idf(ngram_token, 20) AS ngram_idf,
  count_vectorizer(stp_token, 13) AS cnt_vec_comments,
  tf_idf(token_comments, 10, 1) AS cmts_idf,
  vector_assembler(array(cmts_idf, viewsgot, ohe_add_comments, ngram_idf, cnt_vec_comments)) AS features
)
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='reviews')
AS SELECT * FROM movie_review_e2e_DND;
```

#### Limites {#limitations}

Les restrictions suivantes s’appliquent lorsque vous utilisez `TRANSFORM` avec `CREATE TABLE`. Consultez `CREATE TABLE AS SELECT` section Limites et comportement pour une explication détaillée de la manière dont les données transformées sont stockées, dont les sorties vectorielles sont traitées et pourquoi les résultats ne peuvent pas être réutilisés directement dans les workflows d’entraînement de modèles.

- Les sorties vectorielles sont automatiquement converties en tableaux, qui ne peuvent pas être utilisés directement dans `CREATE MODEL`.
- La logique de transformation n’est pas conservée en tant que métadonnées et ne peut pas être réutilisée entre les lots.

## INSERT INTO

La commande `INSERT INTO` est définie comme suit :

>[!IMPORTANT]
>
>Query Service prend en charge les **opérations d’ajout uniquement** à l’aide du moteur ITAS. `INSERT INTO` est la seule commande de manipulation de données prise en charge. Les opérations **update** et **delete** ne sont pas disponibles. Pour refléter les modifications apportées à vos données, insérez de nouveaux enregistrements qui représentent l’état souhaité.

```sql
INSERT INTO table_name select_query
```

| Paramètres | Description |
| ----- | ----- |
| `table_name` | Nom de la table dans laquelle vous souhaitez insérer la requête. |
| `select_query` | Une déclaration `SELECT`. La syntaxe de la requête `SELECT` se trouve dans la section [Requêtes SELECT](#select-queries). |

**Exemple**

>[!NOTE]
>
>Ce qui suit est un exemple artificiel et fourni uniquement à titre d’information.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
>Ne placez **pas** l’instruction `SELECT` entre parenthèses (). En outre, le schéma du résultat de l’instruction `SELECT` doit être conforme à celui de la table définie dans l’instruction `INSERT INTO`. Vous pouvez fournir une clause `SNAPSHOT` pour lire des deltas incrémentiels dans la table cible.

La plupart des champs d’un schéma XDM réel sont introuvables au niveau racine et SQL ne permet pas l’utilisation de la notation par points. Pour obtenir un résultat réaliste à l’aide de champs imbriqués, vous devez mapper chaque champ de votre chemin d’accès `INSERT INTO`.

Pour `INSERT INTO` des chemins imbriqués, utilisez la syntaxe suivante :

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

La commande `DROP TABLE` supprime une table existante et le répertoire qui lui est associé du système de fichiers s&#39;il ne s&#39;agit pas d&#39;une table externe. Si la table n’existe pas, une exception se produit.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Paramètres | Description |
| ------ | ------ |
| `IF EXISTS` | Si cette option est spécifiée, aucune exception n&#39;est générée si la table n&#39;existe **pas**. |

## CRÉER UNE BASE DE DONNÉES

La commande `CREATE DATABASE` crée une base de données Azure Data Lake Storage (ADLS).

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## SUPPRIMER LA BASE DE DONNÉES

La commande `DROP DATABASE` supprime la base de données d&#39;une instance.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Paramètres | Description |
| ------ | ------ |
| `IF EXISTS` | Si cette option est spécifiée, aucune exception n&#39;est générée si la base de données n&#39;existe **pas**. |

## DÉPOSER LE SCHÉMA

La commande `DROP SCHEMA` supprime un schéma existant.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Paramètres | Description |
| ------ | ------ |
| `IF EXISTS` | Si ce paramètre est spécifié et que le schéma n’existe **pas** aucune exception n’est générée. |
| `RESTRICT` | Valeur par défaut du mode. S’il est spécifié, le schéma n’est supprimé que s’il ne contient **pas** de tables. |
| `CASCADE` | S’il est spécifié, le schéma est déposé avec toutes les tables qu’il contient. |

## CREATE VIEW {#create-view}

Une vue SQL est une table virtuelle basée sur le jeu de résultats d&#39;une instruction SQL. Créez une vue avec l&#39;instruction `CREATE VIEW` et donnez-lui un nom. Vous pouvez ensuite utiliser ce nom pour faire référence aux résultats de la requête. Cela facilite la réutilisation des requêtes complexes.

La syntaxe suivante définit une requête `CREATE VIEW` pour un jeu de données. Ce jeu de données peut être un jeu de données de magasin ADLS ou accéléré.

```sql
CREATE VIEW view_name AS select_query
```

| Paramètres | Description |
| ------ | ------ |
| `view_name` | Nom de la vue à créer. |
| `select_query` | Une déclaration `SELECT`. La syntaxe de la requête `SELECT` se trouve dans la section [Requêtes SELECT](#select-queries). |

**Exemple**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

La syntaxe suivante définit une requête `CREATE VIEW` qui crée une vue dans le contexte d&#39;une base de données et d&#39;un schéma.

**Exemple**

```sql
CREATE VIEW db_name.schema_name.view_name AS select_query
CREATE OR REPLACE VIEW db_name.schema_name.view_name AS select_query
```

| Paramètres | Description |
| ------ | ------ |
| `db_name` | Nom de la base de données. |
| `schema_name` | Nom du schéma. |
| `view_name` | Nom de la vue à créer. |
| `select_query` | Une déclaration `SELECT`. La syntaxe de la requête `SELECT` se trouve dans la section [Requêtes SELECT](#select-queries). |

**Exemple**

```sql
CREATE VIEW <dbV1 AS SELECT color, type FROM Inventory;

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory;
```

## AFFICHER LES VUES

La requête suivante affiche la liste des vues.

```sql
SHOW VIEWS;
```

```console
 Db Name  | Schema Name | Name  | Id       |  Dataset Dependencies | Views Dependencies | TYPE
----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## DROP VIEW

La syntaxe suivante définit une requête `DROP VIEW` :

```sql
DROP VIEW [IF EXISTS] view_name
```

| Paramètres | Description |
| ------ | ------ |
| `IF EXISTS` | Si cette option est spécifiée, aucune exception n&#39;est générée si la vue n&#39;existe **pas**. |
| `view_name` | Nom de la vue à supprimer. |

**Exemple**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Bloc anonyme {#anonymous-block}

Un bloc anonyme se compose de deux sections : exécutable et gestion des exceptions. Dans un bloc anonyme, la section exécutable est obligatoire. Toutefois, la section de gestion des exceptions est facultative.

L’exemple suivant montre comment créer un bloc avec une ou plusieurs instructions à exécuter ensemble :

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Vous trouverez ci-dessous un exemple d’utilisation du bloc anonyme.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### Instructions conditionnelles dans un bloc anonyme {#conditional-anonymous-block-statements}

La structure de contrôle IF-THEN-ELSE permet l&#39;exécution conditionnelle d&#39;une liste d&#39;instructions lorsqu&#39;une condition est évaluée comme TRUE. Cette structure de contrôle ne s’applique qu’à un bloc anonyme. Si cette structure est utilisée comme commande autonome, une erreur de syntaxe se produit (« Commande non valide en dehors du bloc anonyme »).

Le fragment de code ci-dessous illustre le format correct d’une instruction conditionnelle IF-THEN-ELSE dans un bloc anonyme.

```javascript
IF booleanExpression THEN
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSE
   List of statements;
END IF
```

**Exemple**

L’exemple ci-dessous exécute `SELECT 200;`.

```sql
$$BEGIN
    SET @V = SELECT 2;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;   

 END$$;
```

Cette structure peut être utilisée avec `raise_error();` pour renvoyer un message d’erreur personnalisé. Le bloc de code illustré ci-dessous met fin au bloc anonyme avec « message d’erreur personnalisé ».

**Exemple**

```sql
$$BEGIN
    SET @V = SELECT 5;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT raise_error('custom error message');
    END IF;   

 END$$;
```

#### Instructions IF imbriquées

Les instructions IF imbriquées sont prises en charge dans des blocs anonymes.

**Exemple**

```sql
$$BEGIN
    SET @V = SELECT 1;
    IF @V = 1 THEN
       SELECT 100;
       IF @V > 0 THEN
         SELECT 1000;
       END IF;   
    END IF;   

 END$$; 
```

#### Blocs d’exception

Les blocs d’exception sont pris en charge dans les blocs anonymes.

**Exemple**

```sql
$$BEGIN
    SET @V = SELECT 2;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT raise_error(concat('custom-error for v= ', '@V' ));

    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;  
EXCEPTION WHEN OTHER THEN 
  SELECT 'THERE WAS AN ERROR';    
 END$$;
```

### Auto to JSON {#auto-to-json}

Query Service prend en charge un paramètre facultatif au niveau de la session pour renvoyer les champs complexes de niveau supérieur des requêtes INTERactives SELECT sous forme de chaînes JSON. Le paramètre `auto_to_json` permet de renvoyer les données de champs complexes sous forme de fichier JSON, puis de les analyser dans des objets JSON à l’aide de bibliothèques standard.

DÉFINISSEZ l’indicateur de fonctionnalité `auto_to_json` sur true avant d’exécuter votre requête SELECT qui contient des champs complexes.

```sql
set auto_to_json=true; 
```

#### Avant de définir l’indicateur de `auto_to_json`

Le tableau suivant fournit un exemple de résultat de requête avant l’application du paramètre `auto_to_json` . La même requête SELECT (comme illustré ci-dessous) qui cible une table avec des champs complexes a été utilisée dans les deux scénarios.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

Les résultats sont les suivants :

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### Après avoir défini l’indicateur de `auto_to_json`

Le tableau suivant montre la différence de résultats que le paramètre `auto_to_json` a sur le jeu de données résultant. La même requête SELECT a été utilisée dans les deux scénarios.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Résoudre l’instantané de secours en cas d’échec {#resolve-fallback-snapshot-on-failure}

L’option `resolve_fallback_snapshot_on_failure` permet de résoudre le problème d’un ID d’instantané expiré.

Définissez l’option `resolve_fallback_snapshot_on_failure` sur true pour remplacer un instantané par un ID d’instantané précédent.

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

La ligne de code suivante remplace l’`@from_snapshot_id` par l’`snapshot_id` disponible en premier à partir des métadonnées.

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```


## Organisation des ressources de données

Il est important d’organiser logiquement vos ressources de données dans le lac de données Adobe Experience Platform au fur et à mesure de leur croissance. Query Service étend les constructions SQL qui vous permettent de regrouper logiquement des ressources de données dans un sandbox. Cette méthode d’organisation permet de partager des ressources de données entre les schémas sans avoir à les déplacer physiquement.

Les éléments SQL suivants utilisant la syntaxe SQL standard sont pris en charge pour que vous puissiez organiser logiquement vos données.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Consultez le guide [organisation logique des ressources de données](../best-practices/organize-data-assets.md) pour une explication plus détaillée des bonnes pratiques relatives à Query Service.

## Le tableau existe

La commande SQL `table_exists` est utilisée pour confirmer si une table existe actuellement dans le système. La commande renvoie une valeur booléenne : `true` si le tableau **existe** et `false` si le tableau n’existe **pas**.

En validant l’existence d’une table avant d’exécuter les instructions, la fonction `table_exists` simplifie le processus d’écriture d’un bloc anonyme pour couvrir les cas d’utilisation `CREATE` et `INSERT INTO`.

La syntaxe suivante définit la commande `table_exists` :

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

## Intégré {#inline}

La fonction `inline` sépare les éléments d’un tableau de structures et génère les valeurs dans un tableau. Il peut uniquement être placé dans la liste `SELECT` ou dans un `LATERAL VIEW`.

La fonction `inline` **ne peut pas** peut être placée dans une liste de sélection où il existe d&#39;autres fonctions de générateur.

Par défaut, les colonnes produites sont nommées « col1 », « col2 », etc. Si l’expression est `NULL`, aucune ligne n’est générée.

>[!TIP]
>
>Les noms des colonnes peuvent être renommés à l’aide de la commande `RENAME`.

**Exemple**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

L’exemple renvoie ce qui suit :

```text
1  a Spark SQL
2  b Spark SQL
```

Ce deuxième example illustre en outre le concept et l&#39;application de la fonction `inline`. Le modèle de données de l’exemple est illustré dans l’image ci-dessous.

![Diagramme de schéma pour productListItems.](../images/sql/productListItems.png)

**Exemple**

```sql
select inline(productListItems) from source_dataset limit 10;
```

Les valeurs extraites de la `source_dataset` sont utilisées pour renseigner la table cible.

| SKU | _experience | quantité | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (« (« (« (A,pass,B,NULL) ») ») | 5 | 10,5 |
| product-id-5 | (« (« (« (A, pass, B,NULL) ») ») |          |              |
| product-id-2 | (« (« (« (AF, C, D,NULL) ») ») | 6 | 40 |
| product-id-4 | (« (« (« (BM, pass, NA,NULL) ») ») | 3 | 12 |

## SET

La commande `SET` définit une propriété et renvoie la valeur d’une propriété existante ou répertorie toutes les propriétés existantes. Si une valeur est fournie pour une clé de propriété existante, l’ancienne valeur est remplacée.

```sql
SET property_key = property_value
```

| Paramètres | Description |
| ------ | ------ |
| `property_key` | Nom de la propriété que vous souhaitez répertorier ou modifier. |
| `property_value` | Valeur pour laquelle vous souhaitez définir la propriété. |

Pour renvoyer la valeur de n’importe quel paramètre, utilisez `SET [property key]` sans `property_value`.

## [!DNL PostgreSQL] des commandes

Les sous-sections ci-dessous couvrent les commandes [!DNL PostgreSQL] prises en charge par Query Service.

### ANALYSER LE TABLEAU {#analyze-table}

La commande `ANALYZE TABLE` effectue une analyse de répartition et des calculs statistiques pour la ou les tables nommées. L’utilisation de `ANALYZE TABLE` varie selon que les jeux de données sont stockés dans la [boutique accélérée](#compute-statistics-accelerated-store) ou dans le [lac de données](#compute-statistics-data-lake). Voir leurs sections respectives pour plus d’informations sur son utilisation.

#### COMPUTE STATISTICS sur la boutique accélérée {#compute-statistics-accelerated-store}

La commande `ANALYZE TABLE` calcule les statistiques d’une table sur la boutique accélérée. Les statistiques sont calculées sur les requêtes CTAS ou ITAS exécutées pour une table donnée sur la boutique accélérée.

**Exemple**

```sql
ANALYZE TABLE <original_table_name>
```

Voici une liste des calculs statistiques disponibles après avoir utilisé la commande `ANALYZE TABLE` :-

| Valeurs calculées | Description |
|---|---|
| `field` | Nom de la colonne dans un tableau. |
| `data-type` | Type de données acceptable pour chaque colonne. |
| `count` | Nombre de lignes contenant une valeur non nulle pour ce champ. |
| `distinct-count` | Nombre de valeurs uniques ou distinctes pour ce champ. |
| `missing` | Nombre de lignes ayant une valeur nulle pour ce champ. |
| `max` | Valeur maximale du tableau analysé. |
| `min` | Valeur minimale du tableau analysé. |
| `mean` | Valeur moyenne du tableau analysé. |
| `stdev` | Écart type du tableau analysé. |

#### CALCULER LES STATISTIQUES sur le lac de données {#compute-statistics-data-lake}

Vous pouvez désormais calculer les statistiques au niveau des colonnes sur les jeux de données [!DNL Azure Data Lake Storage] (ADLS) avec la commande SQL `COMPUTE STATISTICS`. Calculer les statistiques des colonnes sur l’ensemble du jeu de données, un sous-ensemble d’un jeu de données, toutes les colonnes ou un sous-ensemble de colonnes.

`COMPUTE STATISTICS` étend la commande `ANALYZE TABLE`. Toutefois, les commandes `COMPUTE STATISTICS`, `FILTERCONTEXT` et `FOR COLUMNS` ne sont pas prises en charge sur les tables de la boutique accélérée. Ces extensions pour la commande `ANALYZE TABLE` ne sont actuellement prises en charge que pour les tables ADLS.

**Exemple**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

La commande `FILTER CONTEXT` calcule les statistiques sur un sous-ensemble du jeu de données en fonction de la condition de filtre fournie. La commande `FOR COLUMNS` cible des colonnes spécifiques à analyser.

>[!NOTE]
>
>Les `Statistics ID` et les statistiques générées ne sont valides que pour chaque session et ne sont pas accessibles dans différentes sessions PSQL.<br><br>Limites :<ul><li>La génération de statistiques n’est pas prise en charge pour les types de données de tableau ou de mappage</li><li>Les statistiques calculées ne sont **pas** conservées entre les sessions.</li></ul><br><br>Options:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>Par défaut, l’indicateur est défini sur « true ». Par conséquent, lorsque des statistiques sont demandées sur un type de données non pris en charge, elles ne génèrent pas d’erreur, mais ignorent silencieusement les champs contenant des types de données non pris en charge.<br>Pour activer les notifications sur les erreurs lorsque des statistiques sont demandées sur un type de données non pris en charge, utilisez : `SET skip_stats_for_complex_datatypes = false`.

La sortie de la console s’affiche comme illustré ci-dessous.

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

Vous pouvez ensuite interroger directement les statistiques calculées en référençant le `Statistics ID` . Utilisez le `Statistics ID` ou le nom d’alias comme indiqué dans l’exemple d’instruction ci-dessous pour afficher la sortie dans son intégralité. Pour en savoir plus sur cette fonctionnalité, consultez la documentation [nom d’alias](../key-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

Utilisez la commande `SHOW STATISTICS` pour afficher les métadonnées de toutes les statistiques temporaires générées dans la session. Vous pouvez ainsi affiner la portée de votre analyse statistique.

```sql
SHOW STATISTICS;
```

Vous trouverez ci-dessous un exemple de sortie de SHOW STATISTICS.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Pour plus d’informations, consultez la [documentation sur les statistiques des jeux de données](../key-concepts/dataset-statistics.md).

#### TABLESSAMPLE {#tablesample}

Adobe Experience Platform Query Service fournit des échantillons de jeux de données dans le cadre de ses fonctionnalités approximatives de traitement des requêtes.

Les exemples de jeux de données sont mieux utilisés lorsque vous n’avez pas besoin d’une réponse exacte pour une opération d’agrégation sur un jeu de données. Pour exécuter des requêtes exploratoires plus efficaces sur des jeux de données volumineux en émettant une requête approximative pour renvoyer une réponse approximative, utilisez la fonction `TABLESAMPLE` .

Des échantillons de jeux de données sont créés avec des échantillons aléatoires uniformes issus de jeux de données [!DNL Azure Data Lake Storage] (ADLS) existants, en utilisant uniquement un pourcentage d’enregistrements de l’original. La fonctionnalité d’exemple de jeu de données étend la commande `ANALYZE TABLE` avec les commandes SQL `TABLESAMPLE` et `SAMPLERATE`.

Dans l’exemple ci-dessous, la ligne 1 montre comment calculer un échantillon de 5 % de la table. La ligne 2 montre comment calculer un échantillon de 5 % à partir d’une vue filtrée des données du tableau.

**Exemple**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

Pour plus d’informations, consultez la [documentation sur les exemples de jeux de données](../key-concepts/dataset-samples.md).

### BEGIN

La commande `BEGIN`, ou encore la commande `BEGIN WORK` ou `BEGIN TRANSACTION`, initie un bloc de transaction. Toutes les instructions saisies après la commande begin sont exécutées dans une seule transaction jusqu&#39;à ce qu&#39;une commande COMMIT ou ROLLBACK explicite soit donnée. Cette commande est identique à `START TRANSACTION`.

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

Si `CLOSE name` est utilisé, `name` représente le nom d&#39;un curseur ouvert qui doit être fermé. Si `CLOSE ALL` est utilisé, tous les curseurs ouverts sont fermés.

### DEALLOCATE

Pour désallouer une instruction SQL préparée précédemment, utilisez la commande `DEALLOCATE`. Si vous n’avez pas désaffecté explicitement une instruction préparée, elle est désaffectée à la fin de la session. Vous trouverez plus d&#39;informations sur les instructions préparées dans la section [commande PREPARE](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Si `DEALLOCATE name` est utilisé, `name` représente le nom de l&#39;instruction préparée qui doit être distribuée. Si `DEALLOCATE ALL` est utilisé, toutes les instructions préparées sont désallouées.

### DECLARE

La commande `DECLARE` permet à l’utilisateur de créer un curseur qui peut être utilisé pour récupérer un petit nombre de lignes dans une requête plus volumineuse. Une fois le curseur créé, les lignes sont récupérées à l’aide de `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Paramètres | Description |
| ------ | ------ |
| `name` | Nom du curseur à créer. |
| `query` | Commande `SELECT` ou `VALUES` qui fournit les lignes à renvoyer par le curseur. |

### EXECUTE

La commande `EXECUTE` est utilisée pour exécuter une instruction préparée précédemment. Comme les instructions préparées n&#39;existent que pendant une session, elles doivent avoir été créées par une instruction `PREPARE` exécutée plus tôt dans la session en cours. Vous trouverez plus d&#39;informations sur l&#39;utilisation des instructions préparées dans la section [`PREPARE` command](#prepare).

Si l&#39;instruction `PREPARE` qui a créé l&#39;instruction spécifiait certains paramètres, un jeu de paramètres compatible doit être transmis à l&#39;instruction `EXECUTE`. Si ces paramètres ne sont pas transmis, une erreur est générée.

```sql
EXECUTE name [ ( parameter ) ]
```

| Paramètres | Description |
| ------ | ------ |
| `name` | Nom de l’instruction préparée à exécuter. |
| `parameter` | Valeur réelle d’un paramètre pour l’instruction préparée. Il doit s&#39;agir d&#39;une expression produisant une valeur compatible avec le type de données de ce paramètre, tel que déterminé lors de la création de l&#39;instruction préparée. S’il existe plusieurs paramètres pour l’instruction préparée, ils sont séparés par des virgules. |

### EXPLAIN

La commande `EXPLAIN` affiche le plan d&#39;exécution de l&#39;instruction fournie. Le plan d’exécution indique comment les tables référencées par l’instruction seront analysées. Si plusieurs tables sont référencées, cela indique quels algorithmes de jointure sont utilisés pour rassembler les lignes requises de chaque table d’entrée.

```sql
EXPLAIN statement
```

Pour définir le format de la réponse, utilisez le mot-clé `FORMAT` avec la commande `EXPLAIN`.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Paramètres | Description |
| ------ | ------ |
| `FORMAT` | Utilisez la commande `FORMAT` pour spécifier le format de sortie. Les options disponibles sont `TEXT` ou `JSON`. Les sorties autres que text contiennent les mêmes informations que le format de sortie text, mais les programmes pourront plus facilement les analyser. Ce paramètre est défini par défaut sur `TEXT`. |
| `statement` | Toute instruction `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` ou `CREATE MATERIALIZED VIEW AS` dont vous souhaitez afficher le plan d’exécution. |

>[!IMPORTANT]
>
>Toute sortie renvoyée par une instruction `SELECT` est ignorée lors de l’exécution avec le mot-clé `EXPLAIN`. Les autres effets indésirables de l’instruction se produisent comme d’habitude.

**Exemple**

L’exemple suivant illustre le plan d’une requête simple sur une table avec une seule colonne `integer` et 10000 lignes :

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

La commande `FETCH` récupère les lignes à l&#39;aide d&#39;un curseur créé précédemment.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Paramètres | Description |
| ------ | ------ |
| `num_of_rows` | Nombre de lignes à récupérer. |
| `cursor_name` | Nom du curseur à partir duquel vous récupérez des informations. |

### PREPARE {#prepare}

La commande `PREPARE` permet de créer une instruction préparée. Une instruction préparée est un objet côté serveur qui peut être utilisé pour modéliser des instructions SQL similaires.

Les instructions préparées peuvent prendre des paramètres qui sont des valeurs qui sont remplacées dans l&#39;instruction lors de son exécution. Les paramètres sont référencés par position, en utilisant $1, $2, etc., lors de l&#39;utilisation d&#39;instructions préparées.

Vous pouvez éventuellement spécifier une liste de types de données de paramètre. Si le type de données d’un paramètre n’est pas répertorié, il peut être déduit du contexte.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Paramètres | Description |
| ------ | ------ |
| `name` | Nom de l&#39;instruction préparée. |
| `data_type` | Types de données des paramètres de l&#39;instruction préparée. Si le type de données d’un paramètre n’est pas répertorié, il peut être déduit du contexte. Si vous devez ajouter plusieurs types de données, vous pouvez les ajouter dans une liste séparée par des virgules. |

### ROLLBACK

La commande `ROLLBACK` annule la transaction en cours et ignore toutes les mises à jour effectuées par la transaction.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

La commande `SELECT INTO` crée une table et la remplit avec les données calculées par une requête. Les données ne sont pas renvoyées au client, comme c’est le cas avec une commande `SELECT` normale. Les colonnes du nouveau tableau portent les noms et les types de données associés aux colonnes de sortie de la commande `SELECT`.

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

Vous trouverez plus d’informations sur les paramètres de requête SELECT standard dans la section [Requête SELECT](#select-queries). Cette section répertorie uniquement les paramètres exclusifs à la commande `SELECT INTO`.

| Paramètres | Description |
| ------ | ------ |
| `TEMPORARY` ou `TEMP`. | Paramètre facultatif. Si le paramètre est spécifié, la table créée est une table temporaire. |
| `UNLOGGED` | Paramètre facultatif. Si le paramètre est spécifié, la table créée est une table non enregistrée. Vous trouverez plus d’informations sur les tables non enregistrées dans la [[!DNL PostgreSQL] documentation](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | Nom de la table à créer. |

**Exemple**

La requête suivante crée un `films_recent` de table composé uniquement des entrées récentes du `films` de table :

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

La commande `SHOW` affiche le paramètre actuel des paramètres d’exécution. Ces variables peuvent être définies à l’aide de l’instruction `SET`, en modifiant le fichier de configuration `postgresql.conf`, par le biais de la variable d’environnement `PGOPTIONS` (lors de l’utilisation de libpq ou d’une application basée sur libpq) ou par des indicateurs de ligne de commande lors du démarrage du serveur Postgres.

```sql
SHOW name
SHOW ALL
```

| Paramètres | Description |
| ------ | ------ |
| `name` | Nom du paramètre d’exécution à propos duquel vous souhaitez obtenir des informations. Les valeurs possibles du paramètre d’exécution sont les suivantes : <br>`SERVER_VERSION` : ce paramètre affiche le numéro de version du serveur.<br>`SERVER_ENCODING` : ce paramètre affiche le codage du jeu de caractères côté serveur.<br>`LC_COLLATE` : ce paramètre affiche le paramètre régional de la base de données pour le classement (ordre du texte).<br>`LC_CTYPE` : ce paramètre affiche le paramètre régional de la base de données pour la classification des caractères.<br>`IS_SUPERUSER` : ce paramètre indique si le rôle actuel dispose de privilèges de superutilisateur. |
| `ALL` | Affichez les valeurs de tous les paramètres de configuration avec des descriptions. |

**Exemple**

La requête suivante affiche le paramètre actuel du `DateStyle` de paramètres.

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

La commande `COPY` duplique la sortie de toute requête `SELECT` vers un emplacement spécifié. L’utilisateur doit avoir accès à cet emplacement pour que cette commande réussisse.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Paramètres | Description |
| ------ | ------ |
| `query` | Requête à copier. |
| `format_name` | Format dans lequel vous souhaitez copier la requête. Le `format_name` peut être `parquet`, `csv` ou `json`. Par défaut, la valeur est `parquet`. |

>[!NOTE]
>
>Le chemin de sortie complet est `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE {#alter-table}

La commande `ALTER TABLE` permet d’ajouter ou de supprimer des contraintes de clé primaire ou étrangère et d’ajouter des colonnes au tableau.

#### AJOUTER OU SUPPRIMER UNE CONTRAINTE

Les requêtes SQL suivantes présentent des exemples d’ajout ou de suppression de contraintes dans une table. Les contraintes de clé de Principal et de clé étrangère peuvent être ajoutées à plusieurs colonnes avec des valeurs séparées par des virgules. Vous pouvez créer des clés composites en transmettant plusieurs valeurs de nom de colonne, comme illustré dans les exemples ci-dessous.

**Définir des clés primaires ou composites**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name1, column_name2 ) NAMESPACE namespace
```

**Définir une relation entre des tables basée sur une ou plusieurs clés**

```sql
ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name1, column_name2 ) REFERENCES referenced_table_name ( primary_column_name1, primary_column_name2 )
```

**Définir une colonne d’identité**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace
```

**Déposer une contrainte/relation/identité**

```sql
ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name1, column_name2 )

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
>Le schéma de la table doit être unique et non partagé entre plusieurs tables. En outre, l’espace de noms est obligatoire pour les contraintes de clé primaire, d’identité primaire et d’identité.

#### Ajouter ou supprimer des identités principales et secondaires

Pour ajouter ou supprimer des contraintes pour les colonnes du tableau d’identités principal et secondaire, utilisez la commande `ALTER TABLE`.

Les exemples suivants ajoutent une identité principale et une identité secondaire en ajoutant des contraintes.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Les identités peuvent également être supprimées en supprimant des contraintes, comme illustré dans l’exemple ci-dessous.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Pour plus d’informations, consultez le document sur la [définition d’identités dans des jeux de données ad hoc](../data-governance/ad-hoc-schema-identities.md).

#### AJOUTER UNE COLONNE

Les requêtes SQL suivantes présentent des exemples d’ajout de colonnes à une table.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Types de données pris en charge

Le tableau suivant répertorie les types de données acceptés pour l’ajout de colonnes à un tableau avec [!DNL Postgres SQL], XDM et le [!DNL Accelerated Database Recovery] (ADR) dans Azure SQL.

| --- | Client PSQL | XDM | ADR | Description |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Type de données numériques utilisé pour stocker des entiers volumineux allant de -9 223 372 036 854 775 807 à 9 223 372 036 854 775 807 dans 8 octets. |
| 2 | `integer` | `int4` | `integer` | Type de données numériques utilisé pour stocker des entiers compris entre -2 147 483 648 et 2 147 483 647 en 4 octets. |
| 3 | `smallint` | `int2` | `smallint` | Type de données numériques utilisé pour stocker des entiers allant de -32 768 à 215-1 32 767 en 2 octets. |
| 4 | `tinyint` | `int1` | `tinyint` | Type de données numérique utilisé pour stocker des entiers compris entre 0 et 255 sur 1 octet. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Type de données de caractères de taille variable. `varchar` est préférable de l’utiliser lorsque la taille des entrées de données de colonne varie considérablement. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` et `FLOAT` sont des synonymes valides pour `DOUBLE PRECISION`. `double precision` est un type de données à virgule flottante. Les valeurs à virgule flottante sont stockées sur 8 octets. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` est un synonyme valide de `double precision`.`double precision` est un type de données à virgule flottante. Les valeurs à virgule flottante sont stockées sur 8 octets. |
| 8 | `date` | `date` | `date` | Les types de données `date` sont des valeurs de date de calendrier stockées sur 4 octets sans informations d’horodatage. La plage de dates valides s’étend du 01-01-0001 au 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Type de données utilisé pour stocker un instant dans le temps exprimé sous la forme d’une date et d’une heure de calendrier. `datetime` inclut les qualificateurs de : année, mois, jour, heure, seconde et fraction. Une déclaration de `datetime` peut inclure n&#39;importe quel sous-ensemble de ces unités de temps qui sont reliées dans cette séquence, ou même comprendre une seule unité de temps. |
| 10 | `char(len)` | `string` | `char(len)` | Le mot-clé `char(len)` est utilisé pour indiquer que l’élément est un caractère de longueur fixe. |

#### AJOUTER UN SCHÉMA

La requête SQL suivante illustre un exemple d&#39;ajout d&#39;une table à une base de données/un schéma.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Les tables et vues ADLS ne peuvent pas être ajoutées aux bases de données / schémas DWH.


#### SUPPRIMER LE SCHÉMA

La requête SQL suivante illustre un exemple de suppression d&#39;une table d&#39;une base de données/d&#39;un schéma.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Les tables et vues DWH ne peuvent pas être supprimées des bases de données/schémas DWH physiquement liés.


**Paramètres**

| Paramètres | Description |
| ------ | ------ |
| `table_name` | Nom de la table que vous modifiez. |
| `column_name` | Nom de la colonne à ajouter. |
| `data_type` | Type de données de la colonne à ajouter. Les types de données pris en charge sont les suivants : bigint, char, string, date, datetime, double, double précision, integer, smallint, tinyint, varchar. |

### AFFICHER LES CLÉS DE PRINCIPAL

La commande `SHOW PRIMARY KEYS` répertorie toutes les contraintes de clé primaire pour la base de données donnée.

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


### AFFICHER LES GROUPES DE DONNÉES

La commande `SHOW DATAGROUPS` renvoie un tableau de toutes les bases de données associées. Pour chaque base de données, le tableau comprend un schéma, un type de groupe, un type enfant, un nom enfant et un ID enfant.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Accelerated Store | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### AFFICHER LES GROUPES DE DONNÉES POUR LE TABLEAU

La commande `SHOW DATAGROUPS FOR 'table_name'` renvoie une table de toutes les bases de données associées qui contiennent le paramètre en tant qu’enfant. Pour chaque base de données, le tableau comprend un schéma, un type de groupe, un type enfant, un nom enfant et un ID enfant.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Paramètres**

- `table_name` : nom de la table pour laquelle vous souhaitez rechercher les bases de données associées.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```

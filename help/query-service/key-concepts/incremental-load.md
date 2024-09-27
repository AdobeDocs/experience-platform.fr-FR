---
title: Chargement incrémentiel dans Query Service
description: La fonction de chargement incrémentiel utilise des fonctions d’instantanés et de blocs anonymes afin de fournir une solution en temps quasi réel pour déplacer les données du lac de données vers votre entrepôt de données, tout en ignorant les données correspondantes.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 65eeeb1df1d512c4cd6c67892905a63cc1cc4fc5
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 99%

---

# Chargement incrémentiel dans Query Service

Le modèle de conception de chargement incrémentiel est une solution de gestion des données. Le modèle ne traite que les informations du jeu de données qui ont été créées ou modifiées depuis la dernière exécution du chargement.

Le chargement incrémentiel utilise différentes fonctionnalités fournies par Adobe Experience Platform Query Service, telles que les blocs anonymes et les instantanés. Ce modèle de conception augmente l’efficacité du traitement, car toutes les données déjà traitées à partir de la source sont ignorées. Il peut être utilisé avec le traitement des données en streaming et par lots.

Ce document fournit une série d’instructions pour créer un modèle de conception pour le traitement incrémentiel. Ces étapes peuvent être utilisées comme modèle pour créer vos propres requêtes de chargement incrémentiel de données.

## Prise en main

Les exemples SQL de ce document requièrent une connaissance des fonctions d’instantanés et de blocs anonymes. Nous vous recommandons de lire la documentation sur l’[exemple de requêtes en blocs anonymes](./anonymous-block.md) et la documentation sur la [clause d’instantané](../sql/syntax.md#snapshot-clause).

Pour vous familiariser avec la terminologie utilisée dans ce guide, constulez le [guide de syntaxe SQL](../sql/syntax.md).

## Chargement incrémentiel des données

Les étapes ci-dessous montrent comment créer et charger incrémentiellement des données à l’aide d’instantanés et de la fonction de bloc anonyme. Le modèle de conception peut être utilisé comme modèle pour votre propre séquence de requêtes.

1. Créez une table `checkpoint_log` pour effectuer le suivi de l’instantané le plus récent utilisé pour traiter les données avec succès. La table de suivi (`checkpoint_log` dans cet exemple) doit d’abord être initialisé en `null` afin de traiter de manière incrémentielle un jeu de données.

   ```SQL
   DROP TABLE IF EXISTS checkpoint_log;
   CREATE TABLE  checkpoint_log AS
   SELECT
      cast(NULL AS string) process_name,
      cast(NULL AS string) process_status,
      cast(NULL AS string) last_snapshot_id,
      cast(NULL AS TIMESTAMP) process_timestamp
      WHERE false;
   ```

1. Renseignez la table `checkpoint_log` avec un enregistrement vide pour le jeu de données qui nécessite un traitement incrémentiel. `DIM_TABLE_ABC` est le jeu de données à traiter dans l’exemple ci-dessous. Lors du premier traitement de `DIM_TABLE_ABC`, l’`last_snapshot_id` est initialisé en tant que `null`. Cela vous permet de traiter l’ensemble du jeu de données la première fois et de manière incrémentielle par la suite.

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. Ensuite, initialisez `DIM_TABLE_ABC_Incremental` pour contenir la sortie traitée de `DIM_TABLE_ABC`. Le bloc anonyme dans la section d’exécution **obligatoire** de l’exemple SQL ci-dessous, comme décrit dans les étapes 1 à 4, est exécuté de manière séquentielle pour traiter les données de manière incrémentielle.

   1. Définissez l’`from_snapshot_id` qui indique l’endroit où commence le traitement. L’`from_snapshot_id` dans l’exemple est interrogé à partir de la table `checkpoint_log` à utiliser avec `DIM_TABLE_ABC`. Lors de l’exécution initiale, l’ID de l’instantané est `null`, ce qui signifie que l’ensemble du jeu de données sera traité.
   1. Définissez l’`to_snapshot_id` comme ID d’instantané actuel de la table source (`DIM_TABLE_ABC`). Dans l’exemple, cette requête provient de la table des métadonnées de la table source.
   1. Utilisez le mot-clé `CREATE` pour créer `DIM_TABLE_ABC_Incremenal` comme table de destination. La table de destination conserve les données traitées du jeu de données source (`DIM_TABLE_ABC`). Cela permet aux données traitées de la table source entre `from_snapshot_id` et `to_snapshot_id`, d’être ajoutées de manière incrémentielle à la table de destination.
   1. Mettez à jour la table `checkpoint_log` avec l’`to_snapshot_id` des données source que `DIM_TABLE_ABC` a traité avec succès.
   1. Si l’une des requêtes exécutées de manière séquentielle du bloc anonyme échoue, la section d’exception **facultative** est exécutée. Cela renvoie une erreur et met fin au processus.

   >[!NOTE]
   >
   >L’élément `history_meta('source table name')` est une méthode pratique utilisée pour accéder à l’instantané disponible dans un jeu de données.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       CREATE TABLE DIM_TABLE_ABC_Incremental AS
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
   
   INSERT INTO
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

1. Utilisez la logique de chargement incrémentiel des données dans l’exemple de bloc anonyme ci-dessous pour permettre le traitement et l’ajout régulier de toutes les nouvelles données du jeu de données source (depuis la date et l’heure les plus récentes) à la table de destination. Dans l’exemple, les données modifiées en `DIM_TABLE_ABC` seront traitées et ajoutées à `DIM_TABLE_ABC_incremental`.

   >[!NOTE]
   >
   > `_ID` est la clé primaire dans `DIM_TABLE_ABC_Incremental` et `SELECT history_meta('DIM_TABLE_ABC')`.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       INSERT INTO DIM_TABLE_ABC_Incremental
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
   
   INSERT INTO
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

Cette logique peut être appliquée à n’importe quelle table pour effectuer des chargements incrémentiels.

## Instantanés expirés

Pour résoudre le problème d’un ID d’instantané expiré, insérez la commande suivante au début du bloc anonyme. La ligne de code suivante remplace l’`@from_snapshot_id` par l’`snapshot_id` disponible en premier à partir des métadonnées.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

L’ensemble du bloc de code se présente comme suit :

```SQL
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

## Étapes suivantes

En lisant ce document, vous devriez mieux comprendre comment utiliser les fonctions d’instantané et de bloc anonyme pour effectuer des chargements incrémentiels et appliquer cette logique à vos propres requêtes spécifiques. Pour des directives générales sur l’exécution de requêtes, consultez le [guide sur l’exécution de requêtes dans Query Service](../best-practices/writing-queries.md).

---
title: Chargement incrémentiel dans Query Service
description: La fonction de chargement incrémentiel utilise des fonctions de blocage et d’instantané anonymes afin de fournir une solution en temps quasi réel pour déplacer les données du lac de données vers votre entrepôt de données, tout en ignorant les données correspondantes.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Chargement incrémentiel dans Query Service

Le modèle de conception de charge incrémentale est une solution de gestion des données. Le modèle ne traite que les informations du jeu de données qui ont été créées ou modifiées depuis la dernière exécution du chargement.

Le chargement incrémentiel utilise différentes fonctionnalités fournies par Adobe Experience Platform Query Service, telles que les blocs anonymes et les instantanés. Ce modèle de conception augmente l’efficacité du traitement, car toutes les données déjà traitées à partir de la source sont ignorées. Il peut être utilisé avec la diffusion en continu et le traitement des données par lots.

Ce document fournit une série d’instructions pour créer un modèle de conception pour le traitement incrémentiel. Ces étapes peuvent être utilisées comme modèle pour créer vos propres requêtes de chargement de données incrémentielles.

## Prise en main

Les exemples SQL de ce document nécessitent une compréhension du bloc anonyme et des fonctionnalités d’instantané. Il est recommandé de lire le [exemple de requêtes bloquées anonymes](./anonymous-block.md) la documentation et la [clause d’instantané](../sql/syntax.md#snapshot-clause) documentation.

Reportez-vous à la section [Guide de syntaxe SQL](../sql/syntax.md).

## Chargement incrémentiel des données

Les étapes ci-dessous montrent comment créer et charger des données par incréments à l’aide d’instantanés et de la fonction de blocage anonyme. Le modèle de conception peut être utilisé comme modèle pour votre propre séquence de requêtes.

1 Créez une `checkpoint_log` pour effectuer le suivi de l’instantané le plus récent utilisé pour traiter les données avec succès. La table de tracking (`checkpoint_log` dans cet exemple) doit d’abord être initialisé en `null` afin de traiter de manière incrémentielle un jeu de données.

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

2 Renseignez la variable `checkpoint_log` avec un enregistrement vide pour le jeu de données qui nécessite un traitement incrémentiel. `DIM_TABLE_ABC` est le jeu de données à traiter dans l’exemple ci-dessous. Lors de la première fois de traitement `DIM_TABLE_ABC`, la variable `last_snapshot_id` est initialisé en tant que `null`. Cela vous permet de traiter l’ensemble du jeu de données la première fois et de manière incrémentielle par la suite.

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

3 Ensuite, initialisez `DIM_TABLE_ABC_Incremental` pour contenir la sortie traitée de `DIM_TABLE_ABC`. Le bloc anonyme dans la **required** la section exécution de l’exemple SQL ci-dessous, comme décrit dans les étapes 1 à 4, est exécutée de manière séquentielle pour traiter les données de manière incrémentielle.

1. Définissez la variable `from_snapshot_id` qui indique d’où commence le traitement. Le `from_snapshot_id` dans l’exemple est interrogé à partir de la fonction `checkpoint_log` table à utiliser avec `DIM_TABLE_ABC`. Lors de l’exécution initiale, l’ID d’instantané est `null` ce qui signifie que l’ensemble du jeu de données sera traité.
2. Définissez la variable `to_snapshot_id` comme ID d’instantané actuel de la table source (`DIM_TABLE_ABC`). Dans l’exemple, cette requête provient de la table des métadonnées de la table source.
3. Utilisez la variable `CREATE` mot-clé à créer `DIM_TABLE_ABC_Incremenal` comme table de destination. Le tableau de destination conserve les données traitées du jeu de données source (`DIM_TABLE_ABC`). Cela permet aux données traitées du tableau source entre `from_snapshot_id` et `to_snapshot_id`, à ajouter de manière incrémentielle au tableau de destination.
4. Mettez à jour le `checkpoint_log` avec le `to_snapshot_id` pour les données source qui `DIM_TABLE_ABC` traité avec succès.
5. Si l’une des requêtes exécutées de manière séquentielle du bloc anonyme échoue, la variable **facultatif** exception est exécutée. Cela renvoie une erreur et met fin au processus.

>[!NOTE]
>
>Le `history_meta('source table name')` est une méthode pratique utilisée pour accéder à l’instantané disponible dans un jeu de données.

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

4 Utilisez la logique de chargement des données incrémentielles dans l’exemple de bloc anonyme ci-dessous pour permettre le traitement et l’ajout régulier de toutes les nouvelles données du jeu de données source (depuis l’horodatage le plus récent) à la table de destination. Dans l’exemple, les données sont modifiées en `DIM_TABLE_ABC` sera traité et ajouté à `DIM_TABLE_ABC_incremental`.

>[!NOTE]
>
> `_ID` est la clé Principal dans les deux `DIM_TABLE_ABC_Incremental` et `SELECT history_meta('DIM_TABLE_ABC')`.

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

Cette logique peut être appliquée à n’importe quel tableau pour effectuer des chargements incrémentiels.

## Instantanés expirés

>[!IMPORTANT]
>
>Les métadonnées d’instantané expirent après **two** jours. Un instantané expiré invalide la logique du script fourni ci-dessus.

Pour résoudre le problème d&#39;un ID d&#39;instantané expiré, insérez la commande suivante au début du bloc anonyme. La ligne de code suivante remplace la variable `@from_snapshot_id` avec le plus tôt possible `snapshot_id` à partir des métadonnées.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

L’ensemble du bloc de code se présente comme suit :

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

En lisant ce document, vous devriez mieux comprendre comment utiliser les fonctions de blocage et d’instantané anonymes pour effectuer des chargements incrémentiels et appliquer cette logique à vos propres requêtes spécifiques. Pour des directives générales sur l’exécution de requêtes, consultez le [guide sur l’exécution de requêtes dans Query Service](../best-practices/writing-queries.md).

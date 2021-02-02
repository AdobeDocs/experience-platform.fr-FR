---
keywords: informations ; attribution ai ; attribution ai ; informations d’identification Ai ; service de requête AAI ; requêtes d’attribution ; scores d’attribution
solution: Intelligent Services, Experience Platform
title: Guide de début rapide du service de Requête AAI
topic: Attribution AI queries
description: Ce document fournit un guide et des modèles pour l’utilisation de Requête Service afin d’analyser vos scores d’attribution.
translation-type: tm+mt
source-git-commit: 32d49c9244414afeb2729ef44eb364fb2c609380
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# Guide de début rapide de Adobe Experience Platform Requête Service pour l’analyse des scores d’attribution

Chaque ligne des données représente une conversion, dans laquelle les informations des points de contact connexes sont stockées sous la forme d&#39;un tableau de structures sous la colonne `touchpointsDetail`.

| Informations sur les points de contact | Colonne |
| ---------------------- | ------ |
| Nom du point de contact | `touchpointsDetail. touchpointName` |
| Canal du point de contact | `touchpointsDetail.touchPoint.mediaChannel` |
| Scores algorithmiques AAI de point de contact | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## Recherche des chemins de données

Dans l’interface utilisateur de Adobe Experience Platform, sélectionnez **[!UICONTROL Datasets]** dans le volet de navigation de gauche. La page **[!UICONTROL Datasets]** s&#39;affiche. Ensuite, sélectionnez l&#39;onglet **[!UICONTROL Parcourir]** et recherchez le jeu de données de sortie pour vos scores Attribution AI.

![Accès à votre instance](./images/aai-query/datasets_browse.png)

Sélectionnez votre jeu de données de sortie. La page activité du jeu de données s&#39;affiche.

![activité de données](./images/aai-query/select_preview.png)

Dans la page d&#39;activité des ensembles de données, sélectionnez **[!UICONTROL Jeu de données de Prévisualisation]** dans le coin supérieur droit pour prévisualisation vos données et assurez-vous qu&#39;elles ont été ingérées comme prévu.

![Jeu de données de prévisualisation](./images/aai-query/preview_dataset.JPG)

Après avoir prévisualisé vos données, sélectionnez le schéma dans le rail de droite. Une fenêtre contextuelle s’affiche avec le nom et la description du schéma. Sélectionnez l’hyperlien du nom du schéma à rediriger vers le schéma de notation.

![sélectionner le schéma](./images/aai-query/select_schema.png)

Le schéma de notation vous permet de sélectionner ou de rechercher une valeur. Une fois sélectionnée, les propriétés **[!UICONTROL Field]** du rail latéral s’ouvrent et vous permettent de copier le chemin d’accès à utiliser dans la création de requêtes.

![copier le chemin](./images/aai-query/copy_path.png)

## Service de Requête d&#39;accès

Pour accéder à Requête Service à partir de l’interface utilisateur de la plateforme, début en sélectionnant **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Parcourir]**. Une liste de vos requêtes précédemment enregistrées est chargée.

![Parcourir le service de requête](./images/aai-query/query_tab.png)

Ensuite, sélectionnez **[!UICONTROL Créer une requête]** dans le coin supérieur droit. L’éditeur de Requêtes se charge. L’éditeur de Requêtes vous permet de commencer à créer des requêtes à l’aide de vos données de score.

![Éditeur de requête](./images/aai-query/query_example.png)

Pour plus d’informations sur l’éditeur de Requêtes, consultez le [Guide de l’utilisateur de l’éditeur de Requêtes](../../query-service/ui/user-guide.md).

## Modèles de requête pour l’analyse de score d’attribution

Les requêtes ci-dessous peuvent être utilisées comme modèle pour différents scénarios d’analyse de score. Vous devez remplacer `_tenantId` et `your_score_output_dataset` par les valeurs appropriées figurant dans votre schéma de sortie de score.

>[!NOTE]
>
> Selon la manière dont vos données ont été ingérées, les valeurs utilisées ci-dessous, telles que `timestamp`, peuvent être dans un format différent.

### Exemples de validation

**Nombre total de conversions par événement de conversion (dans une fenêtre de conversion)**

```sql
    SELECT conversionName,
           SUM(scores.firstTouch) as total_conversions,
           SUM(scores.algorithmicSourced) as total_attributed_conversions
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName
                    as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16'
      AND
        conversion_timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

**Nombre total de événements de conversion uniquement (dans une fenêtre de conversion)**

```sql
    SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        COUNT(1) as convOnly_cnt
    FROM
        your_score_output_dataset
    WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

### Exemples d’analyse des tendances

**Nombre de conversions par jour**

```sql
    SELECT conversionName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.firstTouch) as convertion_cnt
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    GROUP BY
        conversionName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, DATE(conversion_timestamp)
    LIMIT 20
```

### Exemples d’analyse de distribution

**Nombre de points de contact sur les chemins de conversion par type défini (dans une fenêtre de conversion)**

```sql
    SELECT conversionName,
           touchpointName,
           COUNT(1) as tp_count
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14' AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, tp_count DESC
```

### Exemples de génération d’informations

**Ventilation incrémentielle des unités par point de contact et date de conversion (dans une fenêtre de conversion)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(conversion_timestamp)
```

**Ventilation incrémentielle des unités par date de point de contact et de point de contact (dans une fenêtre de conversion)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(touchpoint.timestamp) as touchpoint_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    LIMIT 20
```

**Résultats agrégés pour un certain type de point de contact pour tous les modèles de notation (dans une fenêtre de conversion)**

```sql
    SELECT
           conversionName,
           touchpointName,
           SUM(scores.algorithmicSourced) as total_incremental_units,
           SUM(scores.algorithmicInfluenced) as total_influenced_units,
           SUM(scores.uShape) as total_uShape_units,
           SUM(scores.decayUnits) as total_decay_units,
           SUM(scores.linear) as total_linear_units,
           SUM(scores.lastTouch) as total_lastTouch_units,
           SUM(scores.firstTouch) as total_firstTouch_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName = 'display'
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, touchpointName
```

**Avancé - analyse de longueur de chemin**

Obtenez une distribution de longueur de chemin pour chaque type d&#39;événement de conversion :

```sql
    WITH agg_path AS (
          SELECT
            _tenantId.your_score_output_dataset.conversionName as conversionName,
            sum(size(_tenantId.your_score_output_dataset.touchpointsDetail)) as path_length
          FROM
            your_score_output_dataset
          WHERE
            _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
            timestamp >= '2020-07-16' AND
            timestamp <  '2020-10-14'
          GROUP BY
            _tenantId.your_score_output_dataset.conversionName,
            eventMergeId
    )
    SELECT
        conversionName,
        path_length,
        count(1) as conversionPath_count
    FROM
        agg_path
    GROUP BY
        conversionName, path_length
    ORDER BY
        conversionName, path_length
```

**Avancé : nombre distinct de points de contact sur l&#39;analyse des chemins de conversion**

Obtenez la distribution du nombre de points de contact distincts sur un chemin de conversion pour chaque type d&#39;événement de conversion :

```sql
    WITH agg_path AS (
      SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        size(array_distinct(flatten(collect_list(_tenantId.your_score_output_dataset.touchpointsDetail.touchpointName)))) as num_dist_tp
      FROM
        your_score_output_dataset
      WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
      GROUP BY
        _tenantId.your_score_output_dataset.conversionName,
        eventMergeId
    )
    SELECT
        conversionName,
        num_dist_tp,
        count(1) as conversionPath_count
    FROM
     agg_path
    GROUP BY
        conversionName, num_dist_tp
    ORDER BY
        conversionName, num_dist_tp
```

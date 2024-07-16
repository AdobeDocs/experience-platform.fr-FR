---
title: Informations sur le profil
description: Découvrez le langage SQL qui alimente vos insights de profil et utilisez ces requêtes pour générer des insights personnalisés qui explorent davantage vos clients et leurs expériences client.
exl-id: f3792076-3e01-4e26-8788-32927202a2e5
source-git-commit: 34eb9151cc6bb8551553b0a8427e58871acb4dbb
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 3%

---

# Informations sur les profils

Les informations dérivées de l’analyse de votre modèle de données rendent vos données Adobe Real-time Customer Data Platform plus accessibles, compréhensibles et pertinentes pour la prise de décision.

Comprenez vos informations sur les profils en accédant aux données SQL qui les alimentent, puis générez vos propres informations afin d’explorer davantage vos clients et leurs expériences client qui constituent vos profils. Transformez vos données brutes en nouvelles informations exploitables en utilisant le modèle de données Real-Time CDP SQL existant comme source d’inspiration pour créer des requêtes en fonction de vos besoins professionnels uniques.

Pour plus d’informations sur la manière d’adapter le langage SQL de vos insights directement via l’interface utilisateur de Platform, consultez la [documentation sur l’affichage SQL](../view-sql.md).

Les informations suivantes sont toutes disponibles pour que vous puissiez les utiliser dans le [tableau de bord des profils](../guides/profiles.md) ou dans un [ tableau de bord personnalisé ](../user-defined-dashboards.md) défini par l’utilisateur. Consultez la [présentation de la personnalisation](../customize/overview.md) pour obtenir des instructions sur la personnalisation de votre tableau de bord ou la [création et modification de nouveaux widgets](../customize/custom-widgets.md) dans la bibliothèque de widgets et [tableau de bord défini par l’utilisateur](../user-defined-dashboards.md#create-widget).

## Chevauchement des audiences par politique de fusion {#audience-overlap-by-merge-policy}

Questions auxquelles répond cet aperçu :

- Quels profils sont communs aux deux audiences ?
- Quel est l’impact du chevauchement sur les taux d’engagement ou de conversion ?
- Comment les stratégies marketing peuvent-elles être adaptées au segment qui se chevauchent ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            sum(count_of_overlap)Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1333234510
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1559754729)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1559754729
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1333234510))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1333234510
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1559754729 ) a;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation sur le chevauchement des audiences par widget de stratégie de fusion](../guides/profiles.md#audience-overlap-by-merge-policy) .

## Rapport de chevauchement des audiences {#audience-overlap-report}

Questions auxquelles répond cet aperçu :

- Quelles sont les 50 audiences qui se chevauchent le plus ?
- Quelles sont les audiences qui se chevauchent le moins 50 ?
- Comment le modèle se chevauchant change-t-il par stratégie de fusion ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT source_segment_name,
        source_segment_id,
        overlap_segment_name,
        overlap_segment_id,
        max(source_segment_audience_count) source_segment_audience_count,
        max(overlap_segment_audience_count) overlap_segment_audience_count,
        max(overlap_audience_count) overlap_audience_count,
        CASE
            WHEN (max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) > 0 THEN (cast(max(overlap_audience_count) AS DECIMAL(18, 2)) / cast((max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) AS DECIMAL(18, 2))) * 100::DECIMAL(9, 2)
            ELSE 100.00
        END overlapping_percentage
  FROM
    (SELECT adwh_fact_profile_overlap_of_segments.Segment1 source_segment_id,
            adwh_fact_profile_overlap_of_segments.Segment2 overlap_segment_id,
            Sum(count_of_overlap) overlap_audience_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment2 ,
              qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment1) a
  INNER JOIN
    (SELECT sum(count_of_profiles) source_segment_audience_count,
            adwh_dim_segments.segment_name source_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment1
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_dim_segments.segment_id = qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) b ON a.source_segment_id = b.segment1
  INNER JOIN
    (SELECT sum(count_of_profiles) overlap_segment_audience_count,
            adwh_dim_segments.segment_name overlap_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment2
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_dim_segments.segment_id = adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) c ON a.overlap_segment_id = c.segment2
  GROUP BY source_segment_name,
          source_segment_id,
          overlap_segment_name,
          overlap_segment_id
  ORDER BY overlapping_percentage DESC
  LIMIT 5;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de rapport sur le chevauchement des audiences](../guides/profiles.md#audience-overlap-report) .

## Audiences (nombre) {#audiences}

Questions auxquelles répond cet aperçu :

- Quelle stratégie de fusion est principalement utilisée pour la segmentation ?
- Qu’est-ce que la distribution des audiences entre les stratégies de fusion ?
- Existe-t-il des changements significatifs dans le nombre d’audiences pour des stratégies de fusion spécifiques au fil du temps ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT count(DISTINCT a.segment_id) count_of_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) b ON a.merge_policy_id= b.merge_policy_id
  AND a.date_key = b.last_process_date
  WHERE a.merge_policy_id= 2027892989;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget Audiences](../guides/profiles.md#audiences) .

## Audiences mappées au statut de destination {#audiences-mapped-to-destination-status}

Questions auxquelles répond cet aperçu :

- Quelle est la distribution globale des audiences entre les destinations mappées et non mappées ?
- Quelles destinations spécifiques ont le plus grand nombre d’audiences mappées ?
- Quelle proportion du total des audiences reste non mappée ?
- De ces audiences non mappées, existe-t-il des modèles ou des tendances associées ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT COUNT(DISTINCT (y.segment_id)) AS count_mapped_segments,
        COUNT(DISTINCT (x.segment_id)) - COUNT(DISTINCT (y.segment_id)) AS count_unmapped_segments,
        COUNT(DISTINCT (x.segment_id)) AS total_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  LEFT JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations y ON x.segment_id = y.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) z ON x.merge_policy_id = z.merge_policy_id
  AND x.date_key = z.last_process_date
  WHERE x.merge_policy_id = 2027892989;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation sur les audiences mappées sur le widget d’état de destination](../guides/profiles.md#audiences-mapped-to-destination-status) .

## Taille des audiences {#audiences-size}

Questions auxquelles répond cet aperçu :

- Quel segment d’audience a la plus grande taille ?
- Quelles sont les cinq audiences les plus importantes ?
- Comment la distribution de la taille de l’audience change-t-elle au fil du temps pour la plus grande audience ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
        qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
        qsaccel.profile_agg.adwh_dim_segments.segment,
        qsaccel.profile_agg.adwh_dim_segments.segment_name,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles)count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id= 2027892989
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
          qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
          qsaccel.profile_agg.adwh_dim_segments.segment,
          qsaccel.profile_agg.adwh_dim_segments.segment_name
  ORDER BY count_of_profiles DESC
  LIMIT 20;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget Taille des audiences](../guides/profiles.md#audiences-size) .

## Répartition des scores (IA dédiée aux clients) {#customer-ai-distribution-of-scores}

Questions auxquelles répond cet aperçu :

- Quelle est la distribution des scores entre les intervalles pour chacun de mes modèles Customer AI ?
- Quelle est la distribution des scores par score élevé, moyen et faible ?
- Quelle est la ventilation de la distribution de notation par stratégie de fusion ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT b.model_name,
     b.model_type,
     CASE
         WHEN score >= 0
              AND score < 25 THEN 'LOW'
         WHEN score >= 25
              AND score < 75 THEN 'MEDIUM'
         WHEN score >= 75
              AND score <= 100 THEN 'HIGH'
     END bucket_name,
     CASE
         WHEN score >= 0
              AND score < 5 THEN '02.50'
         WHEN score >= 5
              AND score < 10 THEN '07.50'
         WHEN score >= 10
              AND score < 15 THEN '12.50'
         WHEN score >= 15
              AND score < 20 THEN '17.50'
         WHEN score >= 20
              AND score < 25 THEN '22.50'
         WHEN score >= 25
              AND score < 30 THEN '27.50'
         WHEN score >= 30
              AND score < 35 THEN '32.50'
         WHEN score >= 35
              AND score < 40 THEN '37.50'
         WHEN score >= 40
              AND score < 45 THEN '42.50'
         WHEN score >= 45
              AND score < 50 THEN '47.50'
         WHEN score >= 50
              AND score < 55 THEN '52.50'
         WHEN score >= 55
              AND score < 60 THEN '57.50'
         WHEN score >= 60
              AND score < 65 THEN '62.50'
         WHEN score >= 65
              AND score < 70 THEN '67.50'
         WHEN score >= 70
              AND score < 75 THEN '72.50'
         WHEN score >= 75
              AND score < 80 THEN '77.50'
         WHEN score >= 80
              AND score < 85 THEN '82.50'
         WHEN score >= 85
              AND score < 90 THEN '87.50'
         WHEN score >= 90
              AND score < 95 THEN '92.50'
         WHEN score >= 95
              AND score <= 100 THEN '97.50'
     END score_bins,
     Sum(CASE
             WHEN score >= 0
                  AND score < 25 THEN count_of_profiles
             WHEN score >= 25
                  AND score < 75 THEN count_of_profiles
             WHEN score >= 75
                  AND score <= 100 THEN count_of_profiles
         END) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
  AND a.model_id = b.model_id
  WHERE a.merge_policy_id = 2027892989
    AND a.model_id = 1829081696
    AND score_date =
      (SELECT Max(score_date)
       FROM qsaccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
          model_type,
          CASE
              WHEN score >= 0
                   AND score < 25 THEN 'LOW'
              WHEN score >= 25
                   AND score < 75 THEN 'MEDIUM'
              WHEN score >= 75
                   AND score <= 100 THEN 'HIGH'
          END,
          CASE
              WHEN score >= 0
                   AND score < 5 THEN '02.50'
              WHEN score >= 5
                   AND score < 10 THEN '07.50'
              WHEN score >= 10
                   AND score < 15 THEN '12.50'
              WHEN score >= 15
                   AND score < 20 THEN '17.50'
              WHEN score >= 20
                   AND score < 25 THEN '22.50'
              WHEN score >= 25
                   AND score < 30 THEN '27.50'
              WHEN score >= 30
                   AND score < 35 THEN '32.50'
              WHEN score >= 35
                   AND score < 40 THEN '37.50'
              WHEN score >= 40
                   AND score < 45 THEN '42.50'
              WHEN score >= 45
                   AND score < 50 THEN '47.50'
              WHEN score >= 50
                   AND score < 55 THEN '52.50'
              WHEN score >= 55
                   AND score < 60 THEN '57.50'
              WHEN score >= 60
                   AND score < 65 THEN '62.50'
              WHEN score >= 65
                   AND score < 70 THEN '67.50'
              WHEN score >= 70
                   AND score < 75 THEN '72.50'
              WHEN score >= 75
                   AND score < 80 THEN '77.50'
              WHEN score >= 80
                   AND score < 85 THEN '82.50'
              WHEN score >= 85
                   AND score < 90 THEN '87.50'
              WHEN score >= 90
                   AND score < 95 THEN '92.50'
              WHEN score >= 95
                   AND score <= 100 THEN '97.50'
          END;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, consultez la [documentation sur la distribution du widget de scores dans Customer AI](../guides/profiles.md#customer-ai-distribution-of-scores) .

## Résumé du score de l’IA dédiée aux clients {#customer-ai-scoring-summary}

Questions auxquelles répond cet aperçu :

- Quel est le résumé de notation de chacun de mes modèles Customer AI ?
- Comment les scores de propension de Customer AI changent-ils pour différentes audiences ?
- Comment la synthèse de mon score est-elle modifiée par rapport aux autres IPC dans la présentation des profils ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT model_name,
         model_type,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  WHERE a.merge_policy_id=2027892989
    AND a.model_id =1829081696
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de résumé de notation de Customer AI](../guides/profiles.md#customer-ai-scoring-summary) .

## Chevauchement des identités {#identity-overlap}

Questions auxquelles répond cet aperçu :

- Quelle est l’intersection commune entre [!UICONTROL Type d’identité A] et [!UICONTROL Type d’identité B] ?
- Comment puis-je affiner les audiences de clients en fonction du chevauchement de types d’identité spécifiques afin d’améliorer les stratégies de marketing ciblées ?
- Quelles sont les informations à tirer de l’évaluation des performances d’une campagne dans les zones intersectées ?
- À l’aide de ces informations sur les performances des campagnes, comment optimiser les futurs efforts marketing ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 2027892989
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('avid',
                                                                                          'crmid')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'avid'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid' )a;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation sur le widget de chevauchement des identités](../guides/profiles.md#identity-overlap) .

## Nombre de profils {#profile-count}

Questions auxquelles répond cet aperçu :

- Quel est le nombre total de profils dans Adobe Real-Time Customer Data Platform ?
- Comment les profils sont-ils distribués en fonction de stratégies de fusion ?
- Quelle stratégie de fusion possède le nombre de profils le plus élevé ?

Le SQl qui génère ces informations est le suivant :

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

Vous trouverez des informations complètes sur l’apparence et les fonctionnalités de cet aperçu dans le [guide du widget de nombre de profils](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count).

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget Nombre de profils](../guides/profiles.md#profile-count) .

## Modification du nombre de profils {#profile-count-change}

Questions auxquelles répond cet aperçu :

- Quelle est la tendance des changements globaux du nombre de profils ?
- Qu’est-ce qui a causé des pics ou des baisses significatifs du nombre de profils ?
- Existe-t-il des stratégies de fusion spécifiques qui entraînent le changement du nombre de profils ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT (sum(count_of_profiles) - sum(count_of_profiles_days_ago)) profiles_added
  FROM
    (SELECT sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) count_of_profiles,
            0 count_of_profiles_days_ago
    FROM qsaccel.profile_agg.adwh_fact_profile
    WHERE qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile.date_key = '2024-01-10'
    UNION ALL SELECT 0 count_of_profiles,
                      CASE
                          WHEN sum(cntondatediff) =0 THEN sum(cntmin)
                          ELSE sum(cntondatediff)
                      END AS count_of_profiles_days_ago
    FROM
      (SELECT coalesce(sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles), 0) cntondatediff,
              0 cntmin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =dateadd(DAY, - 30, '2024-01-10')
        UNION ALL SELECT 0 cntondatediff,
                        sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) countMin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =
            (SELECT min(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) col
            FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
            WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >= dateadd(DAY, - 30, '2024-01-10')
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles IS NOT NULL) )b) a;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de modification du nombre de profils](../guides/profiles.md#profile-count-change) .

## Tendance à la modification du nombre de profils {#profile-count-change-trend}

Questions auxquelles répond cet aperçu :

- Quelle est la tendance globale du changement du nombre de profils au cours des 12 derniers mois en fonction de la stratégie de fusion ?
- Existe-t-il des schémas ou des fluctuations spécifiques du nombre de profils qui changent au cours des 30 derniers jours et qui nécessitent une attention particulière ?
- Comment le nombre de profils change-t-il au cours des 90 derniers jours par rapport à la tendance globale ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de tendance de changement de nombre de profils](../guides/profiles.md#profile-count-change-trend) .

## Tendance du nombre de profils {#profile-count-trend}

Questions auxquelles répond cet aperçu :

- Quelle est la tendance globale du nombre de profils basée sur la stratégie de fusion au cours des 30 derniers jours ?
- Sur la base de cette tendance, comment se compare-t-il aux tendances à long terme (par exemple, 90 jours et 12 mois) ?
- Quelle stratégie de fusion contribue le plus à l’augmentation ou à la diminution du nombre de profils au cours des périodes spécifiées (30 jours, 90 jours et 12 mois) ?
- Existe-t-il des pics ou creux spécifiques dans le nombre de profils qui instaurent une corrélation avec certains événements ou périodes au cours de la période de 30 jours ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT date_key,
       sum(count_of_profiles) AS count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -365, y.last_process_date)
    AND x.merge_policy_id = 2027892989
  GROUP BY date_key;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de tendance du nombre de profils](../guides/profiles.md#profile-count-trend) .

## Profils par identité {#profiles-by-identity}

Questions auxquelles répond cet aperçu :

- Parmi le nombre total de profils, quel type d’identité possède une proportion plus élevée ?
- Existe-t-il des disparités significatives entre les types d&#39;identité ?
- Quelle est la distribution globale des types d’identité ?
- Y a-t-il des disparités ou des anomalies significatives dans le nombre d&#39;identités ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, consultez la [documentation sur les profils par widget d’identité](../guides/profiles.md#profiles-by-identity) .

## Tendance de modification du nombre de profils {#profiles-count-change-trend}

Questions auxquelles répond cet aperçu :

- Quelle est la tendance globale du changement du nombre de profils au cours des 12 derniers mois, selon la stratégie de fusion ?
- Existe-t-il des schémas ou des fluctuations spécifiques dans le changement du nombre de profils au cours des 30 derniers jours qui nécessitent une attention particulière ?
- Comment le changement du nombre de profils au cours des 90 derniers jours se compare-t-il à la tendance globale ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de tendance de changement de nombre de profils](../guides/profiles.md#profiles-count-change-trend) .

## Évolution du nombre de profils en fonction des identités {#profiles-count-change-trend-by-identity}

Questions auxquelles répond cet aperçu :

- Quelle est la tendance générale du changement du nombre de profils entre différentes identités au cours des 12 derniers mois ?
- Existe-t-il des tendances d’identité spécifiques qui montrent des changements significatifs au cours des 30 derniers jours ?
- En quoi les modifications du nombre de profils diffèrent-elles lors de la comparaison des tendances de 30 jours, de 90 jours et de 12 mois pour une identité spécifique ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT date_key,
        namespace_description,
        profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            namespace_description,
            (count_of_profiles - lag(count_of_profiles, 1, 0) over(PARTITION BY namespace_description
                                                                  ORDER BY date_key)) profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
              qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (PARTITION BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
                                  ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
        LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
        AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id= -1042977439
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key >= dateadd(DAY, - 30 -1, '2024-01-10')
        GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
                adwh_dim_namespaces.namespace_description)a)b
  WHERE rn_num > 1;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget d’identité sur le nombre de profils](../guides/profiles.md#profiles-count-change-trend-by-identity) .

## Profils à identité unique {#single-identity-profiles}

Questions auxquelles répond cet aperçu :

- Mes données d’identité client sont-elles représentées de manière cohérente avec des identités uniques ?
- Quel pourcentage de ma base d’utilisateurs se compose de profils n’ayant qu’un seul type d’identité ?
- Sur les profils ne comportant qu’un seul type d’identité, comment cela affecte-t-il l’exhaustivité des profils ?
- Existe-t-il une corrélation entre le type d’identité le plus courant et le nombre de profils d’identité uniques ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Single_Identity_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de profils d’identité unique](../guides/profiles.md#single-identity-profiles) .

## Profils à une seule identité par identité {#single-identity-profiles-by-identity}

Questions auxquelles répond cet aperçu :

- Combien de clients uniques se sont enregistrés avec une seule identité (par exemple, un numéro de téléphone ou un courrier électronique) ?
- Quelle est la distribution des profils d’identité uniques entre différents types d’identité, tels que les numéros de téléphone ou d’adresse électronique ?
- Existe-t-il des modèles d’identité ou des changements dans les profils d’identité uniques ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation sur les profils d’identité uniques par widget d’identité](../guides/profiles.md#single-identity-profiles-by-identity) .

## Profils non segmentés {#unsegmented-profiles}

Questions auxquelles répond cet aperçu :

- Combien de profils ne font pas partie d’une audience ?
- Quel pourcentage de l’audience totale est représenté par des profils non segmentés ?
- Une stratégie de fusion contribue-t-elle à un grand nombre de profils non segmentés ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Orphan_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de profils non segmentés](../guides/profiles.md#unsegmented-profiles) .

## Étapes suivantes

En lisant ce document, vous comprenez désormais le langage SQL qui génère des informations de tableau de bord et les questions courantes que cette analyse résout. Vous pouvez désormais modifier et itérer sur le SQL pour générer vos propres informations.

Pour plus d’informations sur la manière d’adapter le langage SQL de vos insights directement via l’interface utilisateur de PLatform, consultez la [documentation sur l’affichage de SQL](../view-sql.md) .

Vous pouvez également lire et comprendre le code SQL qui génère des insights pour les tableaux de bord [Audiences](./audiences.md), [Profils de compte](./account-profiles.md) et [Destinations](./destinations.md).

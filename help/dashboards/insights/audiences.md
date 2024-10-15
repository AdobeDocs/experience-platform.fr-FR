---
title: Informations sur les audiences
description: Découvrez le code SQL qui alimente vos insights d’audience et utilisez ces requêtes pour générer des insights personnalisés afin d’explorer plus en détail les données d’audience de Adobe Experience Platform.
exl-id: 99624234-c4e1-44bb-9567-505bc0c4723e
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 3%

---

# Informations sur les audiences

Les informations dérivées de l’analyse de votre modèle de données rendent vos données Adobe Real-time Customer Data Platform plus accessibles, compréhensibles et pertinentes pour la prise de décision.

Comprenez vos insights d’audience en accédant au code SQL qui les alimente, puis générez vos propres informations afin d’explorer plus en détail les identités et les profils qui constituent vos audiences. Transformez vos données brutes en nouvelles informations exploitables en utilisant le modèle de données Real-Time CDP SQL existant comme source d’inspiration pour créer des requêtes en fonction de vos besoins professionnels uniques.

Pour plus d’informations sur la manière d’adapter le langage SQL de vos insights directement via l’interface utilisateur de PLatform, consultez la [documentation sur l’affichage de SQL](../view-sql.md) .

Les informations suivantes sont toutes disponibles pour que vous puissiez les utiliser dans le [tableau de bord Audiences](../guides/audiences.md) ou dans un [tableau de bord défini par l’utilisateur](../standard-dashboards.md) personnalisé. Consultez la [présentation de la personnalisation](../customize/overview.md) pour obtenir des instructions sur la personnalisation de votre tableau de bord ou la [création et modification de nouveaux widgets](../customize/custom-widgets.md) dans la bibliothèque de widgets et [tableau de bord défini par l’utilisateur](../standard-dashboards.md#create-widget).

Les informations suivantes sont toutes disponibles pour que vous puissiez les utiliser dans le [tableau de bord Audiences](../guides/audiences.md) ou dans un tableau de bord personnalisé.

## Rapport de chevauchement des audiences {#audience-overlap-report}

Questions auxquelles répond cet aperçu :

- Quelles sont les 50 premières audiences qui se chevauchent d’une audience filtrée particulière ?
- Quelles sont les 50 audiences qui se chevauchent le moins d’une audience filtrée particulière ?
- Comment le modèle se chevauchant change-t-il pour une audience filtrée différente ?

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

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de rapport sur le chevauchement des audiences](../guides/audiences.md#audience-overlap-report) .

## Chevauchement des audiences {#audience-overlap}

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
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1870062812
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=2080256533)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=2080256533
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1870062812))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1870062812
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 2080256533 ) a;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation sur le widget de chevauchement d’audiences](../guides/audiences.md#audience-overlap) .

## Tendance modif. taille audience {#audience-size-change-trend}

Questions auxquelles répond cet aperçu :

- La taille de l’audience a-t-elle connu des pics ou des creux significatifs au cours des 30, 90 ou 12 derniers jours ?
- Comment la taille de l’audience change-t-elle au cours de jours spécifiques ?
- Y a-t-il eu des anomalies ou des schémas répétés de pics ou creux détectés au cours des 12 derniers mois ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT date_key,
      Profiles_added
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                                ORDER BY date_key))Profiles_added
    FROM
      (SELECT date_key,
              sum(x.count_of_profiles)count_of_profiles,
              row_number() OVER (
                                  ORDER BY date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
        INNER JOIN
          (SELECT MAX(process_date) last_process_date,
                  merge_policy_id
          FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
          WHERE process_name = 'FACT_TABLES_PROCESSING'
            AND process_status = 'SUCCESSFUL'
          GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
        WHERE segment_id = 1333234510
          AND x.date_key >= dateadd(DAY, -30 -1, y.last_process_date)
        GROUP BY x.date_key) a)b
  WHERE rn_num > 1;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, consultez la [documentation du widget de tendance de changement de taille d’audience](../guides/audiences.md#audience-size-change-trend) .

## Tendance de la taille des audiences par identité {#audience-size-trend-by-identity}

Questions auxquelles répond cet aperçu :

- Mon audience est-elle en constante croissance, stabilisation ou fluctuation ?
- Existe-t-il une identité spécifique qui présente des pics ou des creux dans la croissance de l’audience au fil du temps ?
- Y a-t-il des anomalies dans la croissance de mon identité au fil du temps ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT sum(count_of_profiles) AS identities,
        date_key
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_namespaces z ON x.namespace_id = z.namespace_id
  AND x.merge_policy_id = z.merge_policy_id
  WHERE x.date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
    AND z.namespace_description = 'crmid'
  GROUP BY date_key;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation sur la taille de l’audience par widget d’identité](../guides/audiences.md#audience-size-trend-by-identity) .

## Tendance de la taille de l’audience {#audience-size-trend}

Questions auxquelles répond cet aperçu :

- Comment la taille de l’audience a-t-elle changé au fil du temps, y compris les anomalies ?
- Comment puis-je trouver la tendance globale de la taille de l’audience sur les périodes : 30 jours, 90 jours et 12 mois ?
- Quelles sont les caractéristiques clés de l’audience qui contribuent à sa taille ? Pics dus, par exemple, à des campagnes de marketing par e-mail.

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT date_key,
        sum(count_of_profiles) AS audience_size
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
  GROUP BY date_key,
          segment_id;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation sur le widget de tendance de la taille de l’audience](../guides/audiences.md#audience-size-trend) .

## Taille de l’audience {#audience-size}

Questions auxquelles répond cet aperçu :

- Quelle est la taille totale actuelle de l’audience ?
- Comment la taille actuelle de l’audience se compare-t-elle à des périodes précédentes ou à des audiences spécifiques ?
- Quel est l’impact des campagnes marketing récentes sur la taille de l’audience ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT
  sum(
    qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles
  ) count_of_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
WHERE
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = -1323307941
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1914917902
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-12';
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget Taille de l’audience](../guides/audiences.md#audience-size) .

## Répartition des scores (IA dédiée aux clients) {#customer-ai-distribution-of-scores}

Questions auxquelles répond cet aperçu :

- Quelle est la distribution de notation pour chaque compartiment de mon modèle Customer AI, filtrée par une audience sélectionnée ?
- Quelle est la distribution de notation des niveaux élevé, moyen et faible pour une audience particulière ?
- Quelle est la ventilation de la distribution de notation par différents publics ciblés ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT b.model_name,
      b.model_type,
      c.segment_name,
      c.segment_id,
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
   FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
          JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
     AND a.model_id = b.model_id
          JOIN qsaccel.profile_agg.adwh_dim_segments c ON a.segment_id = c.segment_id
   WHERE a.merge_policy_id = 1133248113
     AND a.model_id = 1829081696
     AND a.segment_id = 1870062812
     AND score_date =
         (SELECT MAX(score_date)
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
          WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
             b.model_type,
             c.segment_name,
             c.segment_id,
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

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, consultez la [documentation sur la distribution du widget de scores dans Customer AI](../guides/audiences.md#customer-ai-distribution-of-scores) .

## Résumé du score de l’IA dédiée aux clients {#customer-ai-scoring-summary}

Questions auxquelles répond cet aperçu :

- Quel est le résumé de notation de chacun de mes modèles Customer AI pour une audience spécifique ?
- Comment les scores de propension de Customer AI changent-ils pour différentes audiences ?
- Comment mon résumé de notation se compare-t-il aux autres IPC dans la présentation de l’audience ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT model_name,
         model_type,
         segment_name,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  JOIN QSAccel.profile_agg.adwh_dim_segments c ON a.segment_id=c.segment_id
  WHERE a.merge_policy_id=1133248113
    AND a.model_id =1829081696
    AND a.segment_id=1870062812
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           segment_name,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget de résumé de notation de Customer AI](../guides/audiences.md#customer-ai-scoring-summary) .

## Chevauchement des identités {#identity-overlap}

Questions auxquelles répond cet aperçu :

- Quelle est l’intersection courante entre [!UICONTROL Type d’identité A] et [!UICONTROL Type d’identité B] pour une audience filtrée ?
- Comment affiner les audiences de clients en fonction du chevauchement de types d’identité spécifiques afin d’améliorer les stratégies marketing ciblées ?
- Quelles sont les informations à tirer de l’évaluation des performances d’une campagne dans les zones intersectées ?
- Sur la base de ces informations, comment optimiser les efforts marketing futurs ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 1709997014
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('crmid',
                                                                                          'email')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'email'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10' ) a;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation sur le widget de chevauchement des identités](../guides/audiences.md#identity-overlap) .

## Profils par identité {#profiles-by-identity}

Questions auxquelles répond cet aperçu :

- Quel type d’identité a la proportion la plus élevée dans le nombre total de profils pour une audience sélectionnée ?
- Existe-t-il des disparités significatives entre les types d’identité pour une audience sélectionnée ?
- Quelle est la distribution globale des types d’identité par audience ?
- Existe-t-il des disparités ou des anomalies significatives dans le nombre d’identités pour différentes audiences ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, consultez la [documentation sur les profils par widget d’identité](../guides/audiences.md#profiles-by-identity) .

## Activations planifiées {#scheduled-activations}

Questions auxquelles répond cet aperçu :

- Quelles sont les dates de début et de fin des activations les plus performantes pour une audience spécifique sur une plateforme spécifique ?
- Quelles plateformes ont été les plus utilisées pour les activations planifiées d’une audience particulière ?
- Existe-t-il des schémas d’utilisation de la plateforme qui pourraient guider les décisions concernant la hiérarchisation ou la diversification des stratégies d’activation pour une audience spécifique ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT p.destination_platform ,
       p.destination_platform_name AS platform ,
       d.destination_name ,
       d.destination ,
       br.start_date ,
       CASE
           WHEN br.end_date = '9999-12-31' THEN 'Ongoing'
           ELSE br.end_date
       END AS end_date
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations br
  JOIN qsaccel.profile_agg.adwh_dim_destination d ON br.destination_id = d.destination_id
  JOIN qsaccel.profile_agg.adwh_dim_destination_platform p ON d.destination_platform_id = p.destination_platform_id
  JOIN
    (SELECT MAX(process_date) AS last_process_date
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) lpd ON lpd.last_process_date BETWEEN br.start_date AND br.end_date
  AND br.segment_id = 1333234510;
```

+++

Pour plus d’informations sur l’apparence et les fonctionnalités de cet aperçu, voir la [documentation du widget Activations planifiées](../guides/audiences.md#scheduled-activations) .

## Étapes suivantes

En lisant ce document, vous comprenez désormais le langage SQL qui génère des informations de tableau de bord et les questions courantes que cette analyse résout. Vous pouvez désormais modifier et itérer sur le SQL pour générer vos propres informations.

Pour plus d’informations sur la manière d’adapter le langage SQL de vos insights directement via l’interface utilisateur de PLatform, consultez la [documentation sur l’affichage de SQL](../view-sql.md) .

Vous pouvez également lire et comprendre le code SQL qui génère des insights pour les tableaux de bord [Profils](./profiles.md), [Profils de compte](./account-profiles.md) et [Destinations](./destinations.md).

---
title: Informations sur les destinations
description: Découvrez le langage SQL qui alimente vos informations sur les destinations et utilisez ces requêtes pour générer des informations personnalisées afin d’explorer plus en détail l’activation des données de Adobe Experience Platform.
exl-id: 762a9960-e7a5-4796-80c7-ef745157cc04
source-git-commit: e4ee4accdb28dafda7e37625eb84062bb6e53644
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 3%

---

# Informations sur les destinations

Les informations dérivées de l’analyse de votre modèle de données rendent vos données Adobe Real-Time CDP plus accessibles, plus compréhensibles et plus pertinentes pour la prise de décision.

Découvrez vos informations sur les destinations en accédant au SQL qui les alimente, puis générez vos propres informations pour explorer plus en détail l’activation des données de Adobe Experience Platform vers vos plateformes de destination. Transformez vos données brutes en nouvelles informations exploitables en utilisant le modèle de données Real-Time CDP existant SQL comme inspiration pour créer des requêtes correspondant aux besoins uniques de votre entreprise.

Consultez la [Documentation View SQL](../view-sql.md) pour plus d’informations sur la manière d’adapter le langage SQL de vos informations directement via l’interface utilisateur de Platform.

Vous pouvez tous utiliser les informations suivantes dans le [tableau de bord des destinations](../guides/destinations.md) ou un [tableau de bord personnalisé défini par l’utilisateur](../standard-dashboards.md). Consultez la [présentation de la personnalisation](../customize/overview.md) pour obtenir des instructions sur la personnalisation de votre tableau de bord ou [créer et modifier de nouveaux widgets](../customize/custom-widgets.md) dans la bibliothèque de widgets et dans le tableau de bord [défini par l’utilisateur](../standard-dashboards.md#create-widget).

## Audiences activées {#activated-audiences}

Questions traitées par cette insight :

- Quel est le nombre total d’audiences activées filtrées par une destination particulière ?
- Quel est le nombre de profils des audiences activé par chaque destination ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette [&#x200B; consultez la &#x200B;](../guides/destinations.md#activated-audiences) Documentation sur le widget Audiences activées .

## Audiences activées dans toutes les destinations {#activated-audiences-across-all-destinations}

Questions traitées par cette insight :

- Combien d’audiences sont activées sur toutes les destinations ?
- Quel est le nombre total d’audiences activées ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette insight, consultez la documentation sur le widget [Audiences activées sur toutes les destinations](../guides/destinations.md#activated-audiences-across-all-destinations).

## Destinations actives par plateforme de destination {#active-destinations-by-destination-platform}

Questions traitées par cette insight :

- Combien de destinations sont actives ?
- Quelle est la répartition des destinations actives par plateforme de destination ?
- Quel est le nombre de destinations actives réparties par chaque plateforme de destination ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

Consultez la [Documentation sur le widget Destinations actives par plateforme de destination](../guides/destinations.md#active-destinations-by-destination-platform) pour plus d’informations sur l’aspect et les fonctionnalités de cette insight.

## Tendance de la taille de l’audience {#audience-size-trend}

Questions traitées par cette insight :

- Comment la taille de l’audience a-t-elle changé au fil du temps, y compris les anomalies pour une audience mappée à une destination ?
- Comment puis-je trouver la tendance globale de la taille de l’audience, par destination, sur les périodes spécifiées de 30 jours, 90 jours et 12 mois ?
- Quelles sont les principales caractéristiques de l’audience qui contribuent à la taille, par exemple les pics concernant les campagnes marketing par e-mail ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette insight, consultez la [documentation sur le widget de tendance de la taille d’audience](../guides/destinations.md#audience-size-trend).

## Audiences courantes {#common-audiences}

Questions traitées par cette insight :

- Quelles sont les audiences communes à deux destinations différentes ?
- Combien de profils ont chacune des audiences communes entre deux destinations différentes ?
- Quelle est l’audience la plus grande à laquelle deux destinations sont mappées ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette [&#x200B; consultez la &#x200B;](../guides/destinations.md#common-audiences) Documentation sur le widget des audiences courantes .

## Statut de destination {#destination-status}

Questions traitées par cette insight :

- Quel est le nombre total de destinations activées pour l’utilisation ?
- Quel est le nombre total de destinations désactivées ?
- Quel est le pourcentage de partage entre les destinations activées et désactivées ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Consultez la [documentation du widget Statut de destination](../guides/destinations.md#destination-status) pour plus d’informations sur l’aspect et les fonctionnalités de cette insight.

## Nombre de destinations {#destinations-count}

Questions traitées par cette insight :

- Combien de destinations sont actuellement configurées ?
- Comment le nombre total de destinations a-t-il changé au fil du temps ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette [&#x200B; consultez la documentation du widget &#x200B;](../guides/destinations.md#destinations-count)Nombre de destinations.

## Intégrité de l’audience mappée {#mapped-audience-health}

Questions traitées par cette insight :

- Quelles audiences mappées à une destination ont présenté des variations significatives au cours des 30 derniers jours ?
- Quelle est la dernière taille d’une audience mappée et si elle a changé au cours du dernier mois ?
- Comment puis-je répertorier toutes les audiences mappées à une destination en fonction de la gravité de leurs modifications de taille au cours du dernier mois ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette [&#x200B; consultez la documentation du widget &#x200B;](../guides/destinations.md#mapped-audience-health)Intégrité de l’audience mappée.

## Audiences mappées {#mapped-audiences}

Questions traitées par cette insight :

- Combien d’audiences sont mappées à une destination spécifique ?
- Comment le nombre d’audiences mappées a-t-il changé au fil du temps ?
- Où puis-je comparer deux destinations pour voir le chevauchement des audiences mappé à chaque destination ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette [&#x200B; consultez la documentation du widget &#x200B;](../guides/destinations.md#mapped-audiences)Audiences mappées.

<!-- 
Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## Destinations les plus utilisées {#most-used-destinations}

Questions traitées par cette insight :

- Quelles sont les destinations les plus utilisées ?
- Combien d’audiences sont mappées à chaque destination, triées du plus au moins ?
- Comment le mappage des audiences aux destinations change-t-il d’un instantané à un autre ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette [&#x200B; consultez la documentation du widget &#x200B;](../guides/destinations.md#most-used-destinations)Destinations les plus utilisées.

## Audiences récemment activées {#recently-activated-audiences}

Questions traitées par cette insight :

- Vers quelle destination une audience a-t-elle été activée le plus récemment ?
- Comment puis-je trouver une liste de toutes les destinations triées par date de la dernière mise à jour ?
- Comment puis-je comparer deux destinations en fonction des activations les plus récentes ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette [&#x200B; consultez la documentation sur le widget &#x200B;](../guides/destinations.md#recently-activated-audiences) Audiences récemment activées .

## Audiences récemment activées par destination {#recently-activated-audiences-by-destination}

Questions traitées par cette insight :

- Quelles sont les audiences activées vers une destination particulière ?
- Comment puis-je trouver une liste d’audiences activées par une audience particulière du plus récent au moins récent ?
- Comment puis-je trouver une liste d’audiences à la date d’activation pour une destination spécifique ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette insight, consultez la documentation sur le widget [Audiences récemment activées par destination](../guides/destinations.md#recently-activated-audiences-by-destination).

## Destinations récemment créées {#recently-created-destinations}

Questions traitées par cette insight :

- Quelles sont les destinations créées le plus récemment ?
- Comment puis-je trouver une liste de destinations avec la date à laquelle elles ont été créées ?
- Quelle nouvelle destination a été créée récemment ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette insight

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

Pour plus d’informations sur l’aspect et les fonctionnalités de cette [&#x200B; consultez la &#x200B;](../guides/destinations.md#recently-created-destinations) Documentation sur le widget des destinations récemment créées .

<!-- 
Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## Étapes suivantes {#next-steps}

En lisant ce document, vous comprenez désormais le langage SQL qui génère des informations sur les tableaux de bord et les questions courantes que cette analyse résout. Vous pouvez désormais modifier et itérer ces requêtes SQL pour générer vos propres informations.

Consultez la [Documentation View SQL](../view-sql.md) pour plus d’informations sur la manière d’adapter le langage SQL de vos informations directement via l’interface utilisateur de Platform.

Vous pouvez également lire et comprendre le langage SQL qui génère des informations pour les tableaux de bord [Profils](./profiles.md), [Profils de compte](./account-profiles.md) et [Audiences](./audiences.md).

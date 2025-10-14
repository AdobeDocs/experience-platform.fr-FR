---
title: Modèle de données Real-Time Customer Data Platform Insights B2C Edition
description: Découvrez comment utiliser les requêtes SQL avec les modèles de données Real-Time Customer Data Platform Insights (édition B2C) pour personnaliser vos propres rapports Real-Time CDP pour vos cas d’utilisation de marketing et d’indicateurs de performance clés.
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Édition B2P" type="Informative" url="https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 1%

---

# Modèle de données Real-Time Customer Data Platform Insights B2C Edition

Le modèle de données Real-Time Customer Data Platform Insights pour l’[&#x200B; édition B2C](../../rtcdp/overview.md#rtcdp-b2c) expose les modèles de données et SQL qui alimentent les insights pour divers widgets de profil, de destination et de segmentation. Vous pouvez personnaliser ces modèles de requête SQL afin de créer des rapports Real-Time CDP pour vos cas d’utilisation d’indicateurs de performance clés (IPC) et marketing. Ces informations peuvent ensuite être utilisées comme widgets personnalisés pour vos tableaux de bord définis par l’utilisateur. Consultez la documentation sur les insights de reporting de magasin accéléré pour découvrir [comment créer un modèle de données d’insights de reporting via Query Service pour l’utiliser avec les données de magasin accélérées et les tableaux de bord définis par l’utilisateur](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).

>[!NOTE]
>
>Le terme &quot;segment&quot; a été mis à jour en &quot;audience&quot; sur l’ensemble des systèmes Adobe Experience Platform. Certaines références aux segments restent utilisées pour les chemins d’accès aux fichiers et les conventions de dénomination des jeux de données.

## Conditions préalables

Ce guide nécessite une compréhension pratique de la [fonctionnalité de tableaux de bord définis par l’utilisateur](../standard-dashboards.md). Veuillez lire la documentation avant de poursuivre avec ce guide.

## Rapports et cas d’utilisation Real-Time CDP

Les rapports Real-Time CDP fournissent des informations sur vos données de profil et sur leurs relations avec les audiences et les destinations. Divers modèles de schémas étoiles ont été développés pour répondre à divers cas d’utilisation marketing courants et chaque modèle de données peut prendre en charge plusieurs cas d’utilisation.

>[!IMPORTANT]
>
>Les données utilisées pour les rapports Real-Time CDP sont exactes pour une stratégie de fusion choisie et pour l’instantané quotidien le plus récent.

### Modèle Profile {#profile-model}

Le modèle de profil se compose de trois jeux de données :

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

L’image ci-dessous contient les champs de données appropriés dans chaque jeu de données.

![Un ERD du modèle de profil.](../images/cdp-insights/profile-model.png)

#### Cas pratique du nombre de profils {#profile-count}

La logique utilisée pour le widget [!UICONTROL Nombre de profils] renvoie le nombre total de profils fusionnés dans la banque de profils au moment où l’instantané a été pris. Pour plus d’informations, voir la documentation du widget [[!UICONTROL Profile count] &#x200B;](../guides/profiles.md#profile-count) .

Le code SQL qui génère le widget [!UICONTROL Profile count] est visible dans la section réductible ci-dessous.

+++Requête SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

#### Cas d’utilisation des profils d’identité uniques {#single-identity-profiles}

La logique utilisée pour le widget [!UICONTROL Profils d’identité unique] fournit un décompte des profils de votre organisation qui n’ont qu’un seul type d’ID qui crée leur identité. Pour plus d’informations, consultez la [[!UICONTROL &#x200B; documentation du widget Profils d’identité unique].](../guides/profiles.md#single-identity-profiles)

Le code SQL qui génère le widget [!UICONTROL Profils d’identité unique] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

### Modèle Namespace {#namespace-model}

Le modèle d’espace de noms comprend les jeux de données suivants :

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

L’image ci-dessous contient les champs de données appropriés dans chaque jeu de données.

![Un ERD du modèle d’espace de noms.](../images/cdp-insights/namespace-model.png)

#### Profils par cas d’utilisation d’identité {#profiles-by-identity}

Le widget [!UICONTROL &#x200B; Profils par identité &#x200B;] affiche la ventilation des identités sur tous les profils fusionnés de votre banque de profils. Pour plus d’informations, consultez la [[!UICONTROL documentation du widget Profils par identité]](../guides/profiles.md#profiles-by-identity) .

Le widget SQL qui génère le widget [!UICONTROL Profils par identité] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

#### Profils d’identité uniques par cas d’utilisation d’identité {#single-identity-profiles-by-identity}

La logique utilisée pour le widget [!UICONTROL Profils d’identité unique par identité] illustre le nombre total de profils qui sont identifiés avec un seul identifiant unique. Pour plus d’informations, consultez la [documentation sur les profils d’identité uniques par widget d’identité](../guides/profiles.md#single-identity-profiles-by-identity) .

Le widget SQL qui génère les [!UICONTROL profils d’identité unique par identité] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

### Modèle d’audience {#audience-model}

Le modèle d’audience comprend les jeux de données suivants :

- `adwh_dim_date`
- `adwh_fact_profile_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’image ci-dessous contient les champs de données appropriés dans chaque jeu de données.

![Un ERD du modèle d’audience.](../images/cdp-insights/audience-model.png)

#### Cas d’utilisation de la taille d’audience {#audience-size}

La logique utilisée pour le widget [!UICONTROL Taille de l’audience] renvoie le nombre total de profils fusionnés dans l’audience sélectionnée au moment de l’instantané le plus récent. Pour plus d’informations, consultez la [[!UICONTROL documentation du widget Taille de l’audience].](../guides/audiences.md#audience-size)

Le code SQL qui génère le widget [!UICONTROL Taille de l’audience] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

#### Cas d’utilisation de la tendance de modification de la taille de l’audience {#audience-size-change-trend}

La logique utilisée pour le widget [!UICONTROL tendance de changement de la taille de l’audience] fournit une représentation graphique linéaire de la différence du nombre total de profils qui remplissent les critères d’une audience donnée entre les instantanés quotidiens les plus récents. Pour plus d’informations, consultez la [[!UICONTROL documentation du widget Tendance des changements de taille d’audience]](../guides/audiences.md#audience-size-change-trend) .

Le code SQL qui génère la tendance de changement de la taille de l’audience [!UICONTROL &#x200B; est visible dans la section réductible ci-dessous.]

+++Requête SQL

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

#### Cas d’utilisation des destinations les plus utilisées {#most-used-destinations}

La logique utilisée dans le widget [!UICONTROL Destinations les plus utilisées] répertorie les destinations les plus utilisées de votre entreprise en fonction du nombre d’audiences qui y sont mappées. Ce classement permet de savoir quelles destinations sont utilisées, tout en présentant éventuellement celles qui peuvent être sous-utilisées. Pour plus d’informations, consultez la documentation du widget [[!UICONTROL Destinations les plus utilisées]](../guides/destinations.md#most-used-destinations) .

Le code SQL qui génère le widget [!UICONTROL Destinations les plus utilisées] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

#### Cas d’utilisation des audiences récemment activées {#recently-activated-audiences}

La logique du widget [!UICONTROL Audiences récemment activées] fournit une liste des audiences les plus récemment mappées à une destination. Cette liste fournit un instantané des audiences et des destinations activement utilisées dans le système et peut vous aider à résoudre les problèmes de mappages erronés. Pour plus d’informations, consultez la [[!UICONTROL documentation du widget Audiences récemment activées].](../guides/destinations.md#recently-activated-audiences)

Le code SQL qui génère le widget [!UICONTROL Audiences récemment activées] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

### Modèle Namespace-audience {#namespace-audience-model}

Le modèle namespace-audience comprend les jeux de données suivants :

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’image ci-dessous contient les champs de données appropriés dans chaque jeu de données.

![Un ERD du modèle namespace-audience.](../images/cdp-insights/namespace-audience-model.png)

#### Profils par identité pour un cas d’utilisation d’audience {#audience-profiles-by-identity}

La logique utilisée dans le widget [!UICONTROL Profils par identité] fournit une ventilation des identités sur tous les profils fusionnés de votre banque de profils pour une audience donnée. Pour plus d’informations, consultez la [[!UICONTROL documentation du widget Profils par identité]](../guides/audiences.md#profiles-by-identity) .

Le widget SQL qui génère le widget [!UICONTROL Profils par identité] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

### Modèle d’espace de noms de chevauchement

Le modèle d’espace de noms de chevauchement est constitué des jeux de données suivants :

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

L’image ci-dessous contient les champs de données appropriés dans chaque jeu de données.

![Un ERD du modèle d’espace de noms de chevauchement.](../images/cdp-insights/overlap-namespace-model.png)

#### Cas d’utilisation de chevauchement d’identités (profils) {#profiles-identity-overlap}

La logique utilisée dans le widget [!UICONTROL chevauchement des identités] affiche le chevauchement des profils dans votre **banque de profils** qui contiennent les deux identités sélectionnées. Pour plus d’informations, reportez-vous à la section du widget [[!UICONTROL chevauchement des identités] de la documentation du tableau de bord [!UICONTROL &#x200B; Profils] &#x200B;](../guides/profiles.md#identity-overlap).

Le code SQL qui génère le widget [!UICONTROL chevauchement d’identités] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

### Espace de noms de chevauchement par modèle d’audience {#overlap-namespace-by-audience-model}

L’espace de noms de chevauchement par modèle d’audience est constitué des jeux de données suivants :

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’image ci-dessous contient les champs de données appropriés dans chaque jeu de données.

![Un ERD de l’espace de noms de chevauchement par modèle d’audience.](../images/cdp-insights/overlap-namespace-by-audience-model.png)

#### Cas d’utilisation du chevauchement des identités (audiences) {#audiences-identity-overlap}

La logique utilisée dans le widget [!UICONTROL chevauchement d’identités] du tableau de bord [!UICONTROL Audiences] illustre le chevauchement des profils qui contiennent les deux identités sélectionnées pour une audience particulière. Pour plus d’informations, reportez-vous à la section du widget [[!UICONTROL chevauchement des identités] de la documentation du tableau de bord [!UICONTROL Audiences]](../guides/audiences.md#identity-overlap).

Le code SQL qui génère le widget [!UICONTROL chevauchement d’identités] est visible dans la section réductible ci-dessous.

+++Requête SQL

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

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### Overlap Namespace-Audience model {#overlap-namespace-audience-model}

The overlap namespace-audience model is comprised of the following datasets: 

- `adwh_fact_profile_overlap_by_namespace_and_segment`
- `adwh_dim_date`
- `adwh_dim_namespace`
- `adwh_dim_overlap_namespaces`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

![An ERD of the overlap namespace-audience model.](../images/cdp-insights/overlap-namespace-audience-model.png) -->

<!-- What insights are gathered from this particular data model? -->

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### AI model {#ai-model}

The AI model is comprised of the following datasets: 

- `adwh_fact_profile_ai_models`
- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_ai_models`

![An ERD of the AI model.](./images/cdp-insights/ai-model.png) -->

<!-- What insights are gathered from this particular data model? -->


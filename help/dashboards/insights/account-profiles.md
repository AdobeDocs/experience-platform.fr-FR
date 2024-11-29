---
title: Informations sur le profil du compte
description: Découvrez le code SQL qui alimente vos informations de profil de compte et utilisez ces requêtes pour générer des informations personnalisées qui explorent davantage vos clients et leurs expériences client.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Édition B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Informations sur le profil du compte

Les [profils de compte](../../rtcdp/accounts/account-profile-overview.md) sont utilisés pour consolider les informations de compte provenant de diverses sources, y compris de plusieurs canaux marketing et systèmes organisationnels. Cette vue unifiée permet une compréhension complète des comptes clients, améliorant ainsi les campagnes marketing B2B. Les insights dérivés de l’analyse de votre modèle de données rendent vos données Adobe Real-Time CDP B2B plus accessibles, plus compréhensibles et plus efficaces pour la prise de décision.

Grâce à l’accès au code SQL qui alimente vos informations, vous pouvez mieux comprendre vos données B2B et générer vos propres informations réutilisables hautement personnalisées pour explorer plus en détail les informations de votre compte client. Transformez vos données brutes en nouvelles informations exploitables en utilisant le modèle de données Real-Time CDP SQL existant comme source d’inspiration pour créer des requêtes en fonction de vos besoins professionnels uniques.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Les informations suivantes sont toutes disponibles pour que vous puissiez les utiliser dans le [tableau de bord Profils de compte](../guides/account-profiles.md) ou dans un [tableau de bord personnalisé](../standard-dashboards.md). Consultez la [présentation de la personnalisation](../customize/overview.md) pour obtenir des instructions sur la personnalisation de votre tableau de bord ou la [création et modification de nouveaux widgets](../customize/custom-widgets.md) dans la bibliothèque de widgets et [tableau de bord défini par l’utilisateur](../standard-dashboards.md#create-widget).

## Profils de compte ajoutés {#account-profiles-added}

Questions auxquelles répond cet aperçu :

- Combien de profils de compte ont été ajoutés sur une période donnée ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## Nouveaux comptes par secteur {#accounts-by-industry}

Questions auxquelles répond cet aperçu :

- À quels sont les cinq principaux secteurs d’activité auxquels appartiennent les profils de compte ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## Nouveaux comptes par type {#accounts-by-type}

Questions auxquelles répond cet aperçu :

- Quel est le nombre de comptes par type ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

## Opportunités ajoutées {#opportunities-added}

Questions auxquelles répond cet aperçu :

- Combien d&#39;opportunités ont été ajoutées sur une période donnée ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## Nouvelles opportunités par rôle individuel {#opportunities-by-person-role}

Questions auxquelles répond cet aperçu :

- Quelle est la taille et le nombre relatifs des différents rôles dans une opportunité ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## Nouvelles opportunités par recettes {#opportunities-by-revenue}

Questions auxquelles répond cet aperçu :

- Quelles sont les 20 meilleures opportunités classées en fonction de leurs recettes (en dollars américains) ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## Nouvelles opportunités par statut et étape {#opportunities-by-status-and-stage}

Questions auxquelles répond cet aperçu :

- Quelles sont les opportunités ouvertes et à quel stade de l&#39;entonnoir de vente ou de marketing ?
- Quelles sont les opportunités fermées et à quel stade de l&#39;entonnoir de vente ou de marketing ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## De nouvelles opportunités gagnées {#opportunities-won}

Questions auxquelles répond cet aperçu :

- Quel est le nombre d&#39;opportunités qui ont été terminées ou qui ont été correctement clôturées ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## Opportunités gagnées (graphique linéaire) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

Questions auxquelles répond cet aperçu :

- Combien d’opportunités ont été finalisées ou bien terminées (gagnées) sur une période donnée ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## Présentation des clients par compte {#customers-per-account-overview}

>[!NOTE]
>
>Le graphique [!UICONTROL  Customers per Account Overview] comprend trois insights d’analyse : [!UICONTROL Customers per Account Detail], [!UICONTROL Opportunités par Account Overview] et [!UICONTROL Opportunités par Account Detail]. Ces explorations publicitaires fournissent des informations plus granulaires, ventilant le nombre de clients et d’opportunités par catégories (comme les clients directs et indirects) et plages (comme les plages de nombres de clients et d’opportunités). Ces graphiques ne sont pas affectés par les filtres de date globaux que vous avez peut-être définis.

Questions auxquelles répond cet aperçu :

- Quelle est la répartition des comptes selon qu&#39;ils ont des clients directs ou indirects ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH LatestDate AS (SELECT MAX(inserted_date) AS max_inserted_date FROM adwh_b2b_account_person_association),
     CategorizedData AS (
         SELECT CASE 
                    WHEN is_direct = 'true' AND person_count = 0 THEN 'Accounts without Direct Customers' 
                    WHEN is_direct = 'false' AND person_count = 0 THEN 'Accounts without Indirect Customers' 
                    WHEN is_direct = 'true' AND person_count > 0 THEN 'Accounts with Direct Customers' 
                    WHEN is_direct = 'false' AND person_count > 0 THEN 'Accounts with Indirect Customers' 
                END AS Account_Category, 
                account_count 
         FROM adwh_b2b_account_person_association 
         WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
     ),
     AggregatedData AS (
         SELECT Account_Category, SUM(account_count) AS Accounts 
         FROM CategorizedData 
         GROUP BY Account_Category
     ),
     AllCategories AS (
         SELECT 'Accounts without Direct Customers' AS Account_Category 
         UNION ALL SELECT 'Accounts without Indirect Customers' 
         UNION ALL SELECT 'Accounts with Direct Customers' 
         UNION ALL SELECT 'Accounts with Indirect Customers'
     )
SELECT ac.Account_Category AS Account_Category, COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad ON ac.Account_Category = ad.Account_Category 
ORDER BY ac.Account_Category;
```

+++

## Clients par détail de compte {#customers-per-account-detail}

>[!NOTE]
>
>Cet aperçu n’est pas affecté par les filtres de dates globaux.

Questions auxquelles répond cet aperçu :

- Combien de comptes ont des plages de clients directs ou indirects différentes ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH customer_ranges AS (
    SELECT 'Direct Customer' AS customer_type, '1-10 Customers' AS person_range 
    UNION ALL
    SELECT 'Direct Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '1000+ Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1-10 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1000+ Customers'
)
SELECT 
    cr.customer_type, 
    cr.person_range, 
    COALESCE(SUM(ap.account_count), 0) AS Accounts
FROM customer_ranges cr
LEFT JOIN (
    SELECT 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END AS customer_type,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END AS person_range,
        SUM(account_count) AS account_count
    FROM adwh_b2b_account_person_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_person_association) 
    GROUP BY 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END
) ap ON cr.customer_type = ap.customer_type AND cr.person_range = ap.person_range
GROUP BY cr.customer_type, cr.person_range
ORDER BY cr.customer_type, 
    CASE cr.person_range 
        WHEN '1-10 Customers' THEN 1 
        WHEN '11-100 Customers' THEN 2 
        WHEN '101-1000 Customers' THEN 3 
        WHEN '1000+ Customers' THEN 4 
    END;
```

+++

## Présentation des opportunités par compte {#opportunities-per-account-overview}

>[!NOTE]
>
>Cet aperçu n’est pas affecté par les filtres de dates globaux.

Questions auxquelles répond cet aperçu :

- Quelle est la distribution des comptes en fonction des opportunités qui leur sont associées ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH LatestDate AS (
    SELECT MAX(inserted_date) AS max_inserted_date 
    FROM adwh_b2b_account_opportunity_association
),
CategorizedData AS (
    SELECT 
        CASE 
            WHEN opportunity_count = 0 THEN 'Accounts without Opportunities'
            WHEN opportunity_count > 0 THEN 'Accounts with Opportunities'
        END AS Opportunity_Category, 
        account_count 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
),
AggregatedData AS (
    SELECT 
        Opportunity_Category,
        SUM(account_count) AS Accounts 
    FROM CategorizedData 
    GROUP BY Opportunity_Category
),
AllCategories AS (
    SELECT 'Accounts without Opportunities' AS Opportunity_Category 
    UNION ALL 
    SELECT 'Accounts with Opportunities'
)
SELECT 
    ac.Opportunity_Category AS Opportunity_Category, 
    COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad 
    ON ac.Opportunity_Category = ad.Opportunity_Category 
ORDER BY ac.Opportunity_Category;
```

+++

## Opportunités par détail de compte {#opportunities-per-account-detail}

>[!NOTE]
>
>Cet aperçu n’est pas affecté par les filtres de dates globaux.

Questions auxquelles répond cet aperçu :

- Combien de comptes présentent différentes plages d’opportunités associées ?

+++Sélectionnez cette option pour afficher le code SQL qui génère cette information.

```sql
WITH opportunity_ranges AS (
    SELECT '1-10 Opportunities' AS opportunity_range 
    UNION ALL 
    SELECT '11-50 Opportunities' 
    UNION ALL 
    SELECT '51-100 Opportunities' 
    UNION ALL 
    SELECT '100+ Opportunities'
)
SELECT opportunity_ranges.opportunity_range AS OPPORTUNITIES, 
       COALESCE(SUM(accounts.total_accounts), 0) AS ACCOUNTS 
FROM opportunity_ranges 
LEFT JOIN (
    SELECT 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END AS opportunity_range, 
        SUM(account_count) AS total_accounts 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_opportunity_association) 
      AND opportunity_count > 0 
    GROUP BY 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END
) AS accounts ON opportunity_ranges.opportunity_range = accounts.opportunity_range 
GROUP BY opportunity_ranges.opportunity_range 
ORDER BY CASE opportunity_ranges.opportunity_range 
            WHEN '1-10 Opportunities' THEN 1 
            WHEN '11-50 Opportunities' THEN 2 
            WHEN '51-100 Opportunities' THEN 3 
            WHEN '100+ Opportunities' THEN 4 
        END;
```

+++

## Étapes suivantes

En lisant ce document, vous comprenez désormais le code SQL qui génère les informations du tableau de bord des profils de compte et les questions courantes que cette analyse résout. Vous pouvez désormais modifier et itérer sur le SQL pour générer vos propres informations. Reportez-vous à la [présentation du mode Query Pro](../sql-insights-query-pro-mode/overview.md) pour savoir comment générer des insights personnalisés avec SQL.

Vous pouvez également lire et comprendre le code SQL qui génère des insights pour les tableaux de bord [Profils](./profiles.md), [Audiences](./audiences.md) et [Destinations](./destinations.md).

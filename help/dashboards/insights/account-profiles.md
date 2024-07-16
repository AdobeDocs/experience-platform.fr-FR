---
title: Informations sur le profil du compte
description: Découvrez le code SQL qui alimente vos informations de profil de compte et utilisez ces requêtes pour générer des informations personnalisées qui explorent davantage vos clients et leurs expériences client.
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Édition B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Informations sur le profil du compte

Les [profils de compte](../../rtcdp/accounts/account-profile-overview.md) sont utilisés pour consolider les informations de compte provenant de diverses sources, y compris de plusieurs canaux marketing et systèmes organisationnels. Cette vue unifiée permet une compréhension complète des comptes clients, améliorant ainsi les campagnes marketing B2B. Les insights dérivés de l’analyse de votre modèle de données rendent vos données Adobe Real-time Customer Data Platform B2B plus accessibles, plus compréhensibles et plus efficaces pour la prise de décision.

Grâce à l’accès au code SQL qui alimente vos informations, vous pouvez mieux comprendre vos données B2B et générer vos propres informations réutilisables hautement personnalisées pour explorer plus en détail les informations de votre compte client. Transformez vos données brutes en nouvelles informations exploitables en utilisant le modèle de données Real-Time CDP SQL existant comme source d’inspiration pour créer des requêtes en fonction de vos besoins professionnels uniques.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Les informations suivantes sont toutes disponibles pour que vous puissiez les utiliser dans le [tableau de bord Profils de compte](../guides/account-profiles.md) ou dans un [tableau de bord personnalisé](../user-defined-dashboards.md). Consultez la [présentation de la personnalisation](../customize/overview.md) pour obtenir des instructions sur la personnalisation de votre tableau de bord ou la [création et modification de nouveaux widgets](../customize/custom-widgets.md) dans la bibliothèque de widgets et [tableau de bord défini par l’utilisateur](../user-defined-dashboards.md#create-widget).

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

## Étapes suivantes

En lisant ce document, vous comprenez désormais le code SQL qui génère les informations du tableau de bord des profils de compte et les questions courantes que cette analyse résout. Vous pouvez désormais modifier et itérer sur le SQL pour générer vos propres informations.

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

Vous pouvez également lire et comprendre le code SQL qui génère des insights pour les tableaux de bord [Profils](./profiles.md), [Audiences](./audiences.md) et [Destinations](./destinations.md).

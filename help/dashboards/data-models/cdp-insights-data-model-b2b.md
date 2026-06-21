---
title: B2B edition du modèle de données d’informations Real-Time Customer Data Platform
description: Découvrez comment utiliser des requêtes SQL avec les modèles de données Real-Time Customer Data Platform Insights (B2B edition) pour personnaliser vos propres rapports Real-Time CDP pour vos cas d’utilisation de marketing et de KPI.
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 7b77ca19-e4c6-4e93-b9e7-c4ef77d6d6d1
TQID: https://experienceleague.adobe.com/5zA8YXF364wlpGwZsTXqu99TOhFsSWGboM3KPEzt3qg
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
subfeature_v2:
  - id: f6ac78a3-5b59-40f5-a37d-45df5303d3a3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 497
ht-degree: 4%

---

# B2B edition du modèle de données d’informations Real-Time CDP

Le modèle de données Real-Time CDP Insights pour B2B edition expose les modèles de données et SQL qui alimentent les informations pour les [profils de compte](https://experienceleague.adobe.com/fr/docs/experience-platform/rtcdp/account/account-profile-overview). Vous pouvez personnaliser ces modèles de requête SQL pour créer des rapports Real-Time CDP pour vos cas d’utilisation de marketing B2B et d’indicateurs clés de performance (KPI). Ces informations peuvent ensuite être utilisées comme widgets personnalisés pour vos tableaux de bord.

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté les packages Real-Time CDP Prime et Ultimate. Consultez la documentation sur les [éditions de Real-Time CDP disponibles](../../rtcdp/overview.md#rtcdp-editions) pour plus d’informations, ou contactez votre représentant Adobe.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).
 -->

## Conditions préalables

Ce guide nécessite une connaissance pratique des tableaux de bord personnalisés. Lisez la documentation sur [comment créer un tableau de bord personnalisé](../standard-dashboards.md) avant de poursuivre avec ce guide.

## Rapports et cas d’utilisation Real-Time CDP B2B insight {#B2B-insight-reports-and-use-cases}

Les rapports B2B de Real-Time CDP fournissent des informations sur les données des profils de votre compte et sur la relation entre les comptes et les opportunités. Les modèles de schéma en étoile suivants ont été développés pour répondre à divers cas d’utilisation marketing courants. Chaque modèle de données peut prendre en charge plusieurs cas d’utilisation.

>[!IMPORTANT]
>
>Les données utilisées pour les rapports B2B de Real-Time CDP sont exactes pour une politique de fusion choisie et à partir de l’instantané quotidien le plus récent.

### Modèle de profil de compte {#account-profile-model}

Le modèle de profil de compte se compose de huit jeux de données :

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

Le diagramme ci-dessous affiche les champs de données pertinents dans chaque jeu de données, leur type de données et les clés étrangères liant les jeux de données.

![Diagramme relationnel d’entité pour le modèle Profil de compte.](../images/data-models/account-profile-model.png)

#### Cas pratique des nouveaux comptes par secteur {#accounts-by-industry}

La logique utilisée pour l’[!UICONTROL Nouveaux comptes par secteur d’activité] insight renvoie les cinq premiers secteurs d’activité en fonction de leur nombre de profils de compte et de leur taille relative les uns par rapport aux autres. Pour plus d’informations[&#128279;](../guides/account-profiles.md#accounts-by-industry) consultez la documentation du widget [!UICONTROL Nouveaux comptes par secteur] .

>[!TIP]
>
>Vous pouvez personnaliser cette requête SQL pour qu’elle renvoie plus ou moins de valeurs que pour les cinq principaux secteurs d’activité.

Le code SQL qui génère le [!UICONTROL Nouveaux comptes par secteur] insight est visible dans la section réductible ci-dessous.

+++Requête SQL

```sql
WITH RankedIndustries AS (
    SELECT
        i.industry,
        SUM(f.counts) AS total_accounts,
        ROW_NUMBER() OVER (ORDER BY SUM(f.counts) DESC) AS industry_rank
    FROM
        adwh_fact_account f
    INNER JOIN adwh_dim_industry i ON f.industry_id = i.industry_id
    WHERE f.accounts_created_date between UPPER(COALESCE('$START_DATE', '')) and UPPER(COALESCE('$END_DATE', ''))
    GROUP BY
        i.industry
)
SELECT
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END AS industry_group,
    SUM(total_accounts) AS total_accounts
FROM
    RankedIndustries
GROUP BY
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END
ORDER BY
    total_accounts DESC
LIMIT 5000;
```

+++

#### Cas d’utilisation des nouveaux comptes par type {#accounts-by-type}

La logique utilisée pour la [!UICONTROL Nouveaux comptes par type] insight renvoie la répartition numérique des comptes par type. Cette insight peut vous aider à orienter la stratégie commerciale et les opérations, y compris l’allocation des ressources ou les stratégies marketing. Pour plus d’informations&rbrack; consultez la documentation du widget &lbrack;[[!UICONTROL Nouveaux comptes par type]](../guides/account-profiles.md#accounts-by-type) .

Le code SQL qui génère le [!UICONTROL Nouveaux comptes par type] insight est visible dans la section réductible ci-dessous.

+++Requête SQL

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

### Modèle d’opportunité {#opportunity-model}

Le modèle d’opportunité se compose de sept jeux de données :

- `adwh_dim_opportunity_stage`
- `adwh_dim_person_role`
- `adwh_dim_opportunity_source_type`
- `adwh_dim_opportunity_name`
- `adwh_fact_opportunity`
- `adwh_opportunity_amount`
- `adwh_fact_opportunity_person`

Le diagramme ci-dessous affiche les champs de données pertinents dans chaque jeu de données.

![Diagramme relationnel d’entité pour le modèle d’opportunité.](../images/data-models/opportunity-model.png)

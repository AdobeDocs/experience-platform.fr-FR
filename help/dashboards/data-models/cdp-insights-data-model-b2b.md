---
title: Modèle de données Real-time Customer Data Platform Insights B2B
description: Découvrez comment utiliser les requêtes SQL avec les modèles de données de statistiques Real-time Customer Data Platform (édition B2B) pour personnaliser vos propres rapports Real-Time CDP pour vos cas d’utilisation de marketing et d’indicateurs de performance clés.
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Édition B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
source-git-commit: 52f67037756af97bac97908d4736a3cbafce6844
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---

# Modèle de données Real-time Customer Data Platform Insights B2B

Le modèle de données Real-time Customer Data Platform Insights pour l’édition B2B expose les modèles de données et SQL qui alimentent les insights pour [profils de compte](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/account/account-profile-overview). Vous pouvez personnaliser ces modèles de requête SQL afin de créer des rapports Real-Time CDP pour vos cas d’utilisation d’indicateurs de performance clés et de marketing B2B. Ces informations peuvent ensuite être utilisées comme widgets personnalisés pour vos tableaux de bord.

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté les packages Real-Time CDP Prime et Ultimate. Consultez la documentation sur la version disponible [éditions Real-Time CDP](../../rtcdp/overview.md#rtcdp-editions) pour plus d’informations, ou contactez votre représentant Adobe.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/customizable-insights/reporting-insights-data-model.md).
 -->

## Conditions préalables

Ce guide nécessite une compréhension pratique des tableaux de bord personnalisés. Lisez la documentation sur [création d’un tableau de bord personnalisé](../user-defined-dashboards.md) avant de poursuivre avec ce guide.

## Rapports d’informations sur Real-Time CDP B2B et cas d’utilisation {#B2B-insight-reports-and-use-cases}

Les rapports Real-Time CDP B2B fournissent des informations sur les données de vos profils de compte et sur la relation entre les comptes et les opportunités. Les modèles de schémas d’étoiles suivants ont été développés pour répondre à divers cas d’utilisation marketing courants et chaque modèle de données peut prendre en charge plusieurs cas d’utilisation.

>[!IMPORTANT]
>
>Les données utilisées pour les rapports Real-Time CDP B2B sont précises pour une stratégie de fusion choisie et issues de l’instantané quotidien le plus récent.

### Modèle de profil de compte {#account-profile-model}

Le modèle de profil de compte comprend huit jeux de données :

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

Le diagramme ci-dessous affiche les champs de données pertinents de chaque jeu de données, leur type de données et les clés étrangères qui lient les jeux de données ensemble.

![Diagramme relationnel d’entité pour le modèle de profil de compte.](../images/data-models/account-profile-model.png)

#### Cas pratique Comptes par secteur {#accounts-by-industry}

La logique utilisée pour la variable [!UICONTROL Comptes par secteur industriel] insight renvoie les cinq premières industries en fonction de leur nombre de profils de compte et de leur taille relative les unes par rapport aux autres. Voir [[!UICONTROL Comptes par secteur industriel] documentation sur les widgets](../guides/account-profiles.md#accounts-by-industry) pour plus d’informations.

>[!TIP]
>
>Vous pouvez personnaliser cette requête SQL pour renvoyer plus ou moins de données que les cinq premières industries.

Le SQL qui génère la variable [!UICONTROL Comptes par secteur industriel] Un aperçu est présenté dans la section réductible ci-dessous.

Requête +++SQL

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

#### Cas d’utilisation Comptes par type {#accounts-by-type}

La logique utilisée pour la variable [!UICONTROL Comptes par type] insight renvoie la ventilation numérique des comptes selon leur type. Ces informations peuvent vous aider à orienter la stratégie commerciale et les opérations, y compris l’allocation des ressources ou les stratégies marketing. Voir [[!UICONTROL Comptes par type] documentation sur les widgets](../guides/account-profiles.md#accounts-by-type) pour plus d’informations.

Le SQL qui génère la variable [!UICONTROL Comptes par type] Un aperçu est présenté dans la section réductible ci-dessous.

Requête +++SQL

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

Le modèle d’opportunité comprend sept jeux de données :

- `adwh_dim_opportunity_stage`
- `adwh_dim_person_role`
- `adwh_dim_opportunity_source_type`
- `adwh_dim_opportunity_name`
- `adwh_fact_opportunity`
- `adwh_opportunity_amount`
- `adwh_fact_opportunity_person`

Le diagramme ci-dessous affiche les champs de données pertinents dans chaque jeu de données.

![Diagramme relationnel de l’entité pour le modèle d’opportunité.](../images/data-models/opportunity-model.png)

---
title: Analytics Insights for Web and Mobile Interactions
description: Ce document explique comment utiliser Query Service pour créer des informations exploitables à partir de données Adobe Analytics ingérées.
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# Analytics - Aperçu des interactions web et mobiles

Adobe Experience Platform vous permet d’ingérer des données à partir de suites de rapports Adobe Analytics à l’aide de champs de modèle de données d’expérience (XDM) pour renseigner les jeux de données. Ces données d’analyse sont modifiées pour être conformes à la classe [!DNL XDM ExperienceEvent]. Query Service peut ensuite utiliser ces données en exécutant des requêtes SQL pour générer des informations précieuses à partir du comportement d’un utilisateur sur les plateformes numériques.

Ce document fournit divers exemples de requêtes SQL qui montrent des cas d’utilisation courants lors de la création d’informations à partir de données Analytics web et mobiles.

Pour plus d’informations sur l’ingestion et le mappage des données d’analyse, consultez la [documentation sur les mappages de champs Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) .

## Commencer

Pour chacun des cas d’utilisation suivants, un exemple de requête SQL paramétré est fourni comme modèle que vous pouvez personnaliser. Spécifiez des paramètres partout où `{ }` apparaît dans les exemples SQL pour le jeu de données, l’eVar, l’événement ou la période que vous souhaitez évaluer.

## Objectifs

Les exemples suivants présentent des requêtes SQL pour des cas d’utilisation courants afin d’analyser vos données Adobe Analytics.

### Générer le nombre de visiteurs pour chaque heure un jour donné

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Identifier les 10 pages les plus consultées un jour donné

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### Identifier les 10 utilisateurs les plus actifs

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Identifier les 10 villes les plus souhaitées en fonction de l’activité des utilisateurs

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Identifier les 10 produits les plus consultés

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU,
              commerce.productviews.value   AS Product_Views
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL)
GROUP BY Product_SKU
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Identifier les 10 revenus les plus élevés

```sql
SELECT Purchase_ID,
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID,
               Explode(productlistitems)   AS Product_Items
        FROM   {TARGET_TABLE}
        WHERE  commerce.`order`.purchaseid IS NOT NULL
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID
ORDER BY total_order_revenue DESC
LIMIT  10;
```

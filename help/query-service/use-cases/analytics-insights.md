---
title: Analytics Insights pour les interactions web et mobiles
description: Ce document explique comment utiliser Query Service pour créer des informations exploitables à partir de données Adobe Analytics ingérées.
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
TQID: https://experienceleague.adobe.com/L5JMf3Vj14Pr5aDyjjEUVctLN89LvFZ-esMKwxqGDUs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 1%

---

# Informations d’Analytics pour les interactions web et mobiles

Adobe Experience Platform vous permet d’ingérer des données à partir de suites de rapports Adobe Analytics à l’aide de champs de modèle de données d’expérience (XDM) afin de renseigner des jeux de données. Ces données d’analyse sont modifiées pour être conformes à la classe [!DNL XDM ExperienceEvent]. Query Service peut ensuite utiliser ces données en exécutant des requêtes SQL pour générer des informations précieuses à partir du comportement d’un utilisateur sur les plateformes numériques.

Ce document fournit divers exemples de requêtes SQL qui montrent des cas d’utilisation courants lors de la création d’informations à partir de données Analytics web et mobiles.

Pour plus d’informations sur l’ingestion et le mappage de données d’analyse[&#128279;](../../sources/connectors/adobe-applications/mapping/analytics.md) consultez la  Documentation sur les mappages de champs Analytics .

## Prise en main

Pour chacun des cas d’utilisation suivants, un exemple de requête SQL paramétrée est fourni comme modèle que vous pouvez personnaliser. Indiquez des paramètres partout où vous voyez des `{ }` dans les exemples SQL pour le jeu de données, l’eVar, l’événement ou la période que vous souhaitez évaluer.

## Objectifs

Les exemples suivants montrent les requêtes SQL pour les cas d’utilisation courants afin d’analyser vos données Adobe Analytics.

### Générer le nombre de visiteurs et visiteuses pour chaque heure d’un jour donné

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

### Identifier les 10 villes les plus souhaitées en fonction de l&#39;activité des utilisateurs

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

### Identifier les 10 revenus de commande les plus élevés

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

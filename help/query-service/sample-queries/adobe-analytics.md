---
keywords: Experience Platform;home;popular topics;query service;Query service;sample queries;sample query;adobe analytics;
solution: Experience Platform
title: Exemples de requêtes
topic: queries
translation-type: tm+mt
source-git-commit: f9749dbc5f2e3ac15be50cc5317ad60586b2c07e
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 89%

---


# Exemples de requêtes pour les données d’Adobe Analytics

Data from selected Adobe Analytics report suites is transformed into XDM [!DNL ExperienceEvents] and ingested into Adobe Experience Platform as datasets for you. This document outlines a number of use cases where Adobe Experience Platform [!DNL Query Service] makes use of this data, and the included sample queries should work with your Adobe Analytics datasets. See the [Analytics field mapping documentation](../../sources/connectors/adobe-applications/mapping/analytics.md) for more information on mapping to XDM [!DNL ExperienceEvents].

## Prise en main

Les exemples SQL de ce document nécessitent la modification du code SQL et le renseignement des paramètres attendus pour vos requêtes en fonction du jeu de données, de l’eVar, de l’événement ou de la période que vous souhaitez évaluer. Spécifiez des paramètres pour chaque `{ }` dans les exemples SQL suivants.

## Exemples SQL couramment utilisés

### Nombre de visiteurs par heure pour un jour donné

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Les 10 pages les plus consultées pour un jour donné

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Les 10 utilisateurs les plus actifs

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Les 10 villes où les utilisateurs sont les plus actifs

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Les 10 produits les plus consultés

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
            WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Les 10 recettes totales de commande les plus élevées

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Nombre d’événements par jour

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## Variables de marchandisage (syntaxe de produit)

Dans Adobe Analytics, les données personnalisées au niveau du produit peuvent être collectées au moyen de variables configurées spécialement et appelées « variables de marchandisage ». Elles sont basées sur une eVar ou un événement personnalisé. La différence entre ces variables et leur utilisation standard est qu’elles représentent une valeur distincte pour chaque produit du résultat plutôt qu’une seule valeur pour le résultat. Ces variables sont appelées « variables de marchandisage de syntaxe de produit ». Elles permettent de collecter des informations, telles qu’une remise par produit ou l’emplacement du produit sur la page dans les résultats de recherche du client.

Here are the XDM fields to access the merchandising variables in your [!DNL Analytics] dataset:

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

Où `[#]` est un index de tableau et `evar#` est la variable eVar spécifique.

### Événements personnalisés

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

Où `[#]` est un index de tableau et `event#` est la variable d’événement personnalisé spécifique.

### Exemples de requêtes

Voici un exemple de requête renvoyant une eVar de marchandisage et un événement pour le premier produit trouvé dans `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

La requête suivante applique « explode » sur `productListItems` et renvoie chaque eVar de marchandisage et chaque événement par produit. Le champ `_id` est inclus pour indiquer la relation avec le résultat d’origine. La valeur `_id` est une clé primaire unique dans le jeu de données [!DNL ExperienceEvent]

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### Erreur courante lors de l’implémentation des exemples de requête

L’erreur « No such struct field » se produit lorsque vous essayez de récupérer un champ qui n’existe pas dans le jeu de données actuel. Évaluez le motif renvoyé dans le message d’erreur afin d’identifier un champ disponible, puis mettez à jour votre requête et relancez l’exécution.

```console
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## Variables de marchandisage (syntaxe de conversion)

La syntaxe de conversion est un autre type de variable de marchandisage trouvé dans Adobe Analytics. Avec la syntaxe de produit, la valeur est collectée en même temps que le produit, mais les données doivent être présentes sur la même page. Il existe des scénarios où les données se produisent sur une page avant la conversion ou l’événement d’intérêt relatif au produit. Par exemple, étudions ce cas d’utilisation portant sur la génération de rapport avec la méthode de recherche de produit.

1. Un utilisateur effectue une recherche interne pour « bonnet d’hiver », qui définit l’eVar6 de marchandisage avec syntaxe de conversion active sur « recherche interne : bonnet d’hiver ».
2. L’utilisateur clique sur « bonnet à pompon » et accède à la page détaillée du produit.\
   a. Cet accès déclenche un événement `Product View` pour le « bonnet à pompon » à 12,99 €.\
   b. Puisque `Product View` est configuré comme un événement de liaison, le produit « bonnet à pompon » est désormais lié à la valeur eVar6 de « recherche interne : bonnet d’hiver ». Chaque fois que le produit « bonnet à pompon » est collecté, il est associé à « recherche interne : bonnet d’hiver » jusqu’à ce que (1) le paramètre d’expiration soit atteint ou (2) qu’une nouvelle valeur eVar6 soit définie et que l’événement de liaison se produise à nouveau pour ce produit.
3. L’utilisateur ajoute le produit à son panier, déclenchant l’événement `Cart Add`.
4. L’utilisateur effectue une autre recherche interne pour « T-shirt d’été », qui définit l’eVar6 de marchandisage avec syntaxe de conversion active sur « recherche interne : T-shirt d’été ».
5. L’utilisateur clique sur « T-shirt de sport » et accède à la page détaillée du produit.\
   a. Cet accès déclenche un événement `Product View` pour le « T-shirt de sport » à 19,99 €.\
   b. L’événement `Product View` reste notre événement de liaison, donc le produit « T-shirt de sport » est maintenant lié à la valeur eVar6 de « recherche interne : T-shirt d’été » et le produit précédent, « bonnet à pompon », reste lié à la valeur eVar6 de « recherche interne : bonnet hivernal ».
6. L’utilisateur ajoute le produit à son panier, déclenchant l’événement `Cart Add`.
7. L’utilisateur procède au paiement des deux produits.

Dans les rapports, les commandes, recettes, consultations de produit et ajouts au panier seront rapportés à eVar6 et s’aligneront sur l’activité du produit lié.

| eVar6 (méthode de recherche de produit) | recettes | commandes | consultations de produit | ajouts au panier |
|---|---|---|---|---|
| recherche interne : T-shirt d’été | 19,99 | 1 | 1 | 1 |
| recherche interne : bonnet d’hiver | 12,99 | 1 | 1 | 1 |

Here are the XDM fields to produce the Conversion Syntax in your [!DNL Analytics] dataset:

### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

Où `evar#` est la variable eVar spécifique.

### Product

```console
productListItems[#].sku
```

Où `[#]` est un index de tableau.

### Exemples de requêtes

Voici un exemple de requête liant la valeur à la paire produit-événement spécifique, à savoir l’événement de consultation de produit dans le cas présent.

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

Voici un exemple où la valeur reste liée aux occurrences suivantes pour le produit concerné. La sous-requête inférieure établit la relation des valeurs pour le produit sur l’événement de liaison déclaré. La sous-requête suivante effectue l’attribution de cette valeur liée lors des prochaines interactions avec le produit concerné. Le niveau supérieur agrège les résultats pour générer le rapport.

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```

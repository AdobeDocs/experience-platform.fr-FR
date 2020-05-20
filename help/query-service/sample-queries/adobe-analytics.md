---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exemples de requêtes
topic: queries
translation-type: tm+mt
source-git-commit: 75c446aed75100bd2b5b4a3d365c090cb01dcc69
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 1%

---


# Exemples de requêtes pour les données Adobe Analytics

Les données des suites de rapports Adobe Analytics sélectionnées sont transformées en événements d’expérience XDM et assimilées à la plateforme Adobe Experience en tant que jeux de données. Ce document décrit un certain nombre de cas d’utilisation où Adobe Experience Platform Requête Service utilise ces données et les exemples de requêtes inclus doivent fonctionner avec vos jeux de données Adobe Analytics. Pour plus d’informations sur la mise en correspondance des champs [Analytics, reportez-vous à la documentation](../../sources/connectors/adobe-applications/mapping/analytics.md) relative au mappage des champs vers XDM ExperienceEvents.

## Prise en main

Les exemples SQL de ce document nécessitent que vous modifiez le code SQL et remplissiez les paramètres attendus pour vos requêtes en fonction du jeu de données, de l&#39;eVar, du événement ou de la période que vous souhaitez évaluer. Fournissez des paramètres où vous le voyez `{ }` dans les exemples SQL suivants.

## Exemples SQL couramment utilisés

### Nombre de visiteurs horaires pour un jour donné

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

### 10 premières pages consultées pour un jour donné

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### 10 utilisateurs les plus actifs

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Les 10 meilleures villes par activité d&#39;utilisateurs

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 10 meilleurs produits consultés

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  _acp_year = {target_year}
              AND _acp_month = {target_month}
              AND _acp_day = {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### 10 principales recettes de commande

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
               AND _acp_year = {target_year} 
               AND _acp_month = {target_month}  
               AND _acp_day = {target_day}) 
GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Nombre de Événements par jour

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND _acp_year = {target_year} 
        AND _acp_month = {target_month}  
        AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

## Variables de marchandisage (syntaxe de produit)

Dans Adobe Analytics, les données personnalisées au niveau du produit peuvent être collectées par le biais de variables configurées spécialement appelées &quot;Variables de marchandisage&quot;. Elles sont basées sur une eVar ou un Événement personnalisé. La différence entre ces variables et leur utilisation standard est qu’elles représentent une valeur distincte pour chaque produit trouvé sur l’accès plutôt qu’une seule valeur pour l’accès. Ces variables sont appelées Variables de marchandisage Syntaxe du produit. Cela permet de collecter des informations telles qu&#39;un &quot;montant d&#39;escompte&quot; par produit ou des informations sur l&#39;&quot;emplacement sur la page&quot; du produit dans les résultats de recherche du client.

Voici les champs XDM pour accéder aux variables de marchandisage de votre jeu de données Analytics :

### eVars

```
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

Où `[#]` est un index de tableau et `evar#` est la variable eVar spécifique.

### Événements personnalisés

```
productListItems[#]._experience.analytics.event1to100.event#.value
```

Où `[#]` est un index de tableau et `event#` est la variable de événement personnalisée spécifique.

### Exemples de requêtes

Voici un exemple de requête renvoyant une eVar et un événement de marchandisage pour le premier produit trouvé dans le `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Cette requête suivante &quot;explose&quot; la variable `productListItems` et renvoie chaque eVar et événement de marchandisage par produit. Le `_id` champ est inclus pour montrer la relation avec l’accès d’origine. La `_id` valeur est une clé primaire unique dans le jeu de données ExperienceEvent.

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
  WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### Erreur courante lors de l’implémentation des exemples de requêtes

L&#39;erreur &quot;Aucun champ struct de ce type&quot; se produit lorsque vous tentez de récupérer un champ qui n&#39;existe pas dans votre jeu de données actuel. Evaluez le motif renvoyé dans le message d’erreur afin d’identifier un champ disponible, puis mettez à jour votre requête et réexécutez-la.

```
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## Variables de marchandisage (syntaxe de conversion)

La syntaxe de conversion est un autre type de variable de marchandisage d’Adobe Analytics. Avec Syntaxe du produit, la valeur est collectée en même temps que le produit, mais les données doivent être présentes sur la même page. Il existe des scénarios où les données se produisent sur une page avant la conversion ou le événement d’intérêt lié au produit. Par exemple, prenez en compte le cas d’utilisation du rapports de méthode de recherche de produits.

1. Un utilisateur effectue une recherche interne de &quot;chapeau d’hiver&quot; qui définit la variable eVar6 de marchandisage activée pour la syntaxe de conversion sur &quot;recherche interne : chapeau d’hiver&quot;.
2. L’utilisateur clique sur &quot;gaufre&quot; et accède à la page des détails du produit.\
   a. L&#39;atterrissage ici déclenche un `Product View` événement pour la &quot;beanie gaufre&quot; pour 12,99 $.\
   b. Etant donné que `Product View` est configuré comme événement de liaison, le produit &quot;waffle beanie&quot; est désormais lié à la valeur eVar6 de &quot;recherche interne : chapeau d&#39;hiver&quot;. Chaque fois que le produit &quot;waffle beanie&quot; est collecté, il est associé à &quot;recherche interne : chapeau d&#39;hiver&quot; jusqu&#39;à ce que (1) le paramètre d&#39;expiration soit atteint ou (2) une nouvelle valeur eVar6 soit définie et que le événement de liaison se produise de nouveau avec ce produit.
3. L’utilisateur ajoute le produit à son panier, en déclenchant le `Cart Add` événement.
4. L’utilisateur effectue une autre recherche interne pour &quot;chemise d’été&quot;, qui définit l’eVar de marchandisage eVar6 activée pour la syntaxe de conversion sur &quot;recherche interne : chemise d’été&quot;.
5. L&#39;utilisateur clique sur &quot;t-shirt sportif&quot; et accède à la page des détails du produit.\
   a. Le débarquement ici déclenche un `Product View` événement pour &quot;t-shirt sportif pour 19,99 $.\
   b. Le `Product View` événement est toujours notre événement de liaison donc maintenant le produit &quot;t-shirt sportif&quot; est maintenant lié à la valeur eVar6 de &quot;recherche interne : chemise d&#39;été&quot; et le produit précédent &quot;beanie de gaufre&quot; est toujours lié à une valeur eVar6 de &quot;recherche interne : beanie de gaufre&quot;.
6. L’utilisateur ajoute le produit à son panier, en déclenchant le `Cart Add` événement.
7. L’utilisateur extrait les données avec les deux produits.

Dans le rapports, les commandes, les recettes, les vues de produits et les ajouts au panier seront signalés par rapport à l’eVar6 et s’aligneront sur l’activité du produit lié.

| eVar6 (méthode de recherche de produits) | recette | commandes | vues de produits | ajouts au panier |
|---|---|---|---|---|
| recherche interne:chemise d’été | 19.99 | 1 | 1 | 1 |
| recherche interne:chapeau hivernal | 12.99 | 1 | 1 | 1 |

Voici les champs XDM pour générer la syntaxe de conversion dans votre jeu de données Analytics :

### eVars

```
_experience.analytics.customDimensions.evars.evar#
```

Où `evar#` est la variable eVar spécifique.

### Produit

```
productListItems[#].sku
```

Où `[#]` est un index de tableau.

### Exemples de requêtes

Voici un exemple de requête qui lie la valeur à la paire produit/événement spécifique, dans ce cas le événement vue produit.

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

Voici un exemple de requête conservant la valeur liée aux occurrences suivantes du produit concerné. La sous-requête la plus basse établit la relation des valeurs avec le produit sur le événement de liaison déclaré. La sous-requête suivante effectue l’attribution de cette valeur liée dans les interactions suivantes avec le produit concerné. Et le niveau supérieur sélectionne les agrégats des résultats pour produire le rapports.

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

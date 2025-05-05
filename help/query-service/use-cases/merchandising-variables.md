---
title: Renvoi et utilisation de variables de marchandisage à partir de données d’analyse
description: Découvrez comment fournir des champs XDM et des exemples de requêtes pour accéder aux variables de marchandisage dans vos jeux de données Analytics.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 12%

---

# Renvoyer et utiliser des variables de marchandisage à partir de données d’analyse

Utilisez Query Service pour gérer les données ingérées d’Adobe Analytics dans Adobe Experience Platform sous forme de jeux de données. Les sections suivantes contiennent des exemples de requêtes que vous pouvez utiliser pour accéder aux variables de marchandisage de vos jeux de données Analytics. Pour plus d’informations sur [l’ingestion et le mappage de données Adobe Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) via la source Analytics, consultez la documentation

## Variables de marchandisage {#merchandising-variables}

Les variables de marchandisage peuvent se conformer à l’une des deux syntaxes suivantes :

* **Syntaxe du produit** : associe la valeur d’eVar à un produit. 
* **Syntaxe de la variable de conversion** : associe l’eVar à un produit uniquement si un événement de liaison se produit. Vous pouvez sélectionner les événements qui agissent comme des événements de liaison.

## Syntaxe du produit {#product-syntax}

Dans Adobe Analytics, les données personnalisées au niveau du produit peuvent être collectées au moyen de variables configurées spécialement et appelées variables de marchandisage. Ils sont basés sur des événements d’eVar ou personnalisés. La différence entre ces variables et leur utilisation type est qu’elles représentent une valeur distincte pour chaque produit trouvé sur l’accès plutôt qu’une seule valeur pour l’accès.

Ces variables sont appelées variables de marchandisage de syntaxe de produit. Cela permet de collecter des informations, telles qu’un &quot;montant de remise&quot; par produit ou des informations sur l’&quot;emplacement sur la page&quot; du produit dans les résultats de recherche du client.

Pour en savoir plus sur l’utilisation de la syntaxe du produit, consultez la documentation Adobe Analytics sur l’ [ implémentation des eVars à l’aide de la syntaxe du produit](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=fr#implement-using-product-syntax).

Les sections ci-dessous décrivent les champs XDM nécessaires pour accéder aux variables de marchandisage dans votre jeu de données [!DNL Analytics] :

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#` : index du tableau auquel vous accédez.
* `evar#` : variable d’eVar spécifique à laquelle vous accédez.

### Événements personnalisés

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#` : index du tableau auquel vous accédez.
* `event#` : variable d’événement personnalisé spécifique à laquelle vous accédez.

## Cas d’utilisation de la syntaxe du produit {#product-use-cases}

Les cas d’utilisation suivants se concentrent sur le renvoi d’un eVar de marchandisage à partir du tableau `productListItems` à l’aide de SQL.

### Renvoie un eVar de marchandisage et un événement

La requête ci-dessous renvoie un eVar de marchandisage et un événement pour le premier produit trouvé dans le tableau `productListItems`.

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

### Développez le tableau productListItems et renvoyez l’eVar de marchandisage et l’événement pour chaque produit.

Cette requête suivante explose le tableau `productListItems` et renvoie chaque eVar de marchandisage et chaque événement par produit. Le champ `_id` est inclus pour indiquer la relation avec le résultat d’origine. La valeur `_id` est une clé primaire unique pour le jeu de données.

>[!NOTE]
>
>La fonction explode sépare les éléments d’un tableau en plusieurs lignes. Elle exclut les valeurs &quot;null&quot;.

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

>[!NOTE]
>
> Si vous tentez de récupérer un champ qui n’existe pas dans votre jeu de données actuel, l’erreur &quot;Aucun champ struct de ce type&quot; se produit. Évaluez le motif renvoyé dans le message d’erreur pour identifier un champ disponible, puis mettez à jour votre requête et relancez-la.
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Syntaxe de la variable de conversion {#conversion-variable-syntax}

La syntaxe des variables de conversion est un autre type de variable de marchandisage qui se trouve dans Adobe Analytics. La syntaxe de la variable de conversion est utilisée lorsque la valeur de l’eVar ne peut pas être définie dans la variable products. Ce scénario signifie généralement que votre page n’a aucun contexte pour le canal de marchandisage ou la méthode de recherche. Dans ce cas, vous devez définir la variable de marchandisage avant que l’utilisateur n’arrive sur la page du produit et la valeur persiste jusqu’à l’événement de liaison.

Par exemple, le scénario de recherche de produit ci-dessous illustre la manière dont les données requises peuvent être présentes sur une page avant la conversion ou l’événement associé au produit.

1. Un utilisateur effectue une recherche interne pour &quot;bonnet d’hiver&quot;, qui définit la syntaxe de conversion activée pour le marchandisage eVar6 sur &quot;recherche interne : bonnet d’hiver&quot;.
2. L’utilisateur clique sur « bonnet à pompon » et accède à la page détaillée du produit.\
   a. Cet accès déclenche un événement `Product View` pour le « bonnet à pompon » à 12,99 €.\
   b. Puisque `Product View` est configuré comme un événement de liaison, le produit &quot;bonnet à pompon&quot; est désormais lié à la valeur eVar6 de &quot;recherche interne : bonnet d’hiver&quot;. Chaque fois que le produit &quot;bonnet à pompon&quot; est collecté, il est associé à &quot;recherche interne : bonnet d’hiver&quot;. Cela se produit jusqu’à ce que le paramètre d’expiration de l’eVar soit atteint ou qu’une nouvelle valeur d’eVar6 soit définie et que l’événement de liaison se produise à nouveau avec ce produit.
3. L’utilisateur ajoute le produit à son panier, déclenchant l’événement `Cart Add`.
4. L’utilisateur effectue une autre recherche interne pour &quot;T-shirt d’été&quot;, qui définit la syntaxe de conversion activée pour le marchandisage eVar6 sur &quot;recherche interne : T-shirt d’été&quot;.
5. L’utilisateur sélectionne un &quot;T-shirt de sport&quot; et accède à la page des détails du produit.\
   a. Cet accès déclenche un événement `Product View` pour le « T-shirt de sport » à 19,99 €.\
   b. Comme l’événement `Product View` est l’événement de liaison, le produit &quot;T-shirt de sport&quot; est désormais lié à la valeur eVar6 de &quot;recherche interne : T-shirt d’été&quot;. Le produit précédent &quot;bonnet à pompon&quot; est toujours lié à une valeur eVar6 de &quot;recherche interne : bonnet à pompon&quot;.
6. L’utilisateur ajoute le produit à son panier, déclenchant l’événement `Cart Add`.
7. L’utilisateur procède au paiement des deux produits.

Dans les rapports, les commandes, les recettes, les consultations de produits et les ajouts au panier sont rapportés à l’eVar 6 et s’alignent sur l’activité du produit lié.

| eVar6 (méthode de recherche de produits) | recettes | commandes | consultations de produit | ajouts au panier |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| recherche interne : T-shirt d’été | 19,99 | 1 | 1 | 1 |
| recherche interne : bonnet d’hiver | 12,99 | 1 | 1 | 1 |

Pour en savoir plus sur l’utilisation de la syntaxe de variable de conversion, consultez la documentation Adobe Analytics sur l’ [ implémentation d’eVars à l’aide de la syntaxe de variable de conversion](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=fr#implement-using-conversion-variable-syntax).

Vous trouverez ci-dessous les champs XDM pour produire la syntaxe de variable de conversion dans votre jeu de données [!DNL Analytics] :

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#` : variable d’eVar spécifique à laquelle vous accédez.

#### Produit

```console
productListItems[#].sku
```

* `#` : index du tableau auquel vous accédez.

## La variable de conversion utilise des cas {#conversion-variable-use-cases}

Les cas d’utilisation ci-dessous reflètent des scénarios qui nécessitent une syntaxe de variable de conversion.

### Lier la valeur à la paire produit/événement spécifique

La requête ci-dessous associe la valeur à la paire produit-événement spécifique. Dans cet exemple, la valeur est liée à l’événement de consultation de produit.

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

### Conserver la valeur liée aux occurrences suivantes du produit respectif

L’exemple de requête ci-dessous conserve la valeur liée aux occurrences suivantes du produit correspondant. La sous-requête la plus basse établit la relation entre la valeur et le produit sur l’événement de liaison déclaré. La sous-requête suivante effectue l’attribution de cette valeur liée lors des prochaines interactions avec le produit concerné. Le niveau supérieur SELECT regroupe les résultats pour produire le rapport.

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

## Étapes suivantes

En lisant ce document, vous devriez mieux comprendre comment renvoyer un eVar de marchandisage à l’aide de la syntaxe du produit et lier une valeur à un produit spécifique avec la syntaxe de la variable de conversion.

Si vous ne l’avez pas déjà fait, vous devriez lire la [documentation sur les informations Analytics pour les interactions web et mobiles](./analytics-insights.md) suivante. Il fournit des cas d’utilisation courants et montre comment utiliser Query Service pour créer des informations exploitables à partir de données Adobe Analytics web et mobiles.

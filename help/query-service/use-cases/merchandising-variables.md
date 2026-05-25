---
title: Renvoyer et utiliser des variables de marchandisage à partir de données d’analyse
description: Découvrez comment fournir des champs XDM et des exemples de requêtes pour accéder aux variables de marchandisage dans vos jeux de données Analytics.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
TQID: https://experienceleague.adobe.com/6iWzOfWBaeqSO-JpcNpDJlZ-AAN221xqJRRsNC8cZus
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1118
ht-degree: 9%

---

# Renvoyer et utiliser des variables de marchandisage à partir de données d’analyse

Utilisez Query Service pour gérer les données ingérées d’Adobe Analytics dans Adobe Experience Platform sous forme de jeux de données. Les sections suivantes fournissent des exemples de requêtes que vous pouvez utiliser pour accéder aux variables de marchandisage dans vos jeux de données Analytics. Consultez la documentation pour plus d’informations sur [comment ingérer et mapper des données Adobe Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) via la source Analytics

## Variables de marchandisage {#merchandising-variables}

Les variables de marchandisage peuvent respecter l’une des deux syntaxes suivantes :

* **Syntaxe du produit** : associe la valeur eVar à un produit. 
* **Syntaxe de la variable de conversion** : associe uniquement l’eVar à un produit si un événement de liaison se produit. Vous pouvez sélectionner les événements qui se comportent comme des événements de liaison.

## Syntaxe du produit {#product-syntax}

Dans Adobe Analytics, les données personnalisées au niveau du produit peuvent être collectées au moyen de variables configurées spécialement et appelées variables de marchandisage. Elles sont basées sur un événement eVar ou personnalisé. La différence entre ces variables et leur utilisation type est qu’elles représentent une valeur distincte pour chaque produit trouvé sur l’accès plutôt qu’une seule valeur pour l’accès.

Ces variables sont appelées variables de marchandisage de syntaxe de produit. Cela permet de collecter des informations, telles qu’un « montant de remise » par produit ou des informations sur l’« emplacement sur la page » du produit dans les résultats de recherche du client.

Pour en savoir plus sur l’utilisation de la syntaxe du produit, consultez la documentation d’Adobe Analytics sur [l’implémentation d’eVars à l’aide de la syntaxe du produit](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=fr#implement-using-product-syntax).

Les sections ci-dessous décrivent les champs XDM nécessaires pour accéder aux variables de marchandisage dans votre jeu de données [!DNL Analytics] :

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#` : index du tableau auquel vous accédez.
* `evar#` : variable eVar spécifique à laquelle vous accédez.

### Événements personnalisés

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#` : index du tableau auquel vous accédez.
* `event#` : variable d’événement personnalisé spécifique à laquelle vous accédez.

## Cas d’utilisation de syntaxe de produit {#product-use-cases}

Les cas d’utilisation suivants portent sur le renvoi d’une eVar de marchandisage à partir du tableau `productListItems` à l’aide de SQL.

### Renvoyer une eVar et un événement de marchandisage

La requête ci-dessous renvoie un événement et une eVar de marchandisage pour le premier produit trouvé dans le tableau `productListItems`.

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

### Explosez le tableau productListItems et renvoyez l’eVar et l’événement de marchandisage pour chaque produit.

Cette requête suivante éclate le tableau `productListItems` et renvoie chaque eVar de marchandisage et événement par produit. Le champ `_id` est inclus pour indiquer la relation avec le résultat d’origine. La valeur `_id` est une clé primaire unique pour le jeu de données.

>[!NOTE]
>
>La fonction explode sépare les éléments d’un tableau en plusieurs lignes. Elle exclut les valeurs nulles.

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
> Si vous tentez de récupérer un champ qui n’existe pas dans votre jeu de données actuel, l’erreur « Aucun champ de structure de ce type » se produit. Évaluez la raison renvoyée dans le message d’erreur pour identifier un champ disponible, puis mettez à jour votre requête et réexécutez-la.
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Syntaxe de la variable de conversion {#conversion-variable-syntax}

La syntaxe de la variable de conversion est un autre type de variable de marchandisage qui se trouve dans Adobe Analytics. La syntaxe de la variable de conversion est utilisée lorsque la valeur eVar ne peut pas être définie dans la variable products. Ce scénario signifie généralement que votre page ne comporte aucun contexte du canal de marchandisage ou de la méthode de recherche. Dans ces cas, vous devez définir la variable de marchandisage avant que l’utilisateur n’arrive à la page de produit et que la valeur persiste jusqu’à ce que l’événement de liaison se produise.

Par exemple, le scénario de recherche de produit ci-dessous illustre la manière dont les données requises peuvent être présentes sur une page avant que la conversion ou l’événement lié au produit ne se produise.

1. Un utilisateur effectue une recherche interne pour « Winter hat », qui définit la syntaxe de conversion activée pour le marchandisage eVar6 sur « recherche interne :winter hat ».
2. L’utilisateur clique sur « bonnet à pompon » et accède à la page détaillée du produit.\
   a. Atterrissage ici déclenche un événement `Product View` pour le « bonnet gaufre » pour $12.99.\
   b. Comme `Product View` est configuré en tant qu’événement de liaison, le produit « waffle beanie » est désormais lié à la valeur eVar6 de « recherche interne :winter chapeau ». Chaque fois que le produit « bonnet gaufre » est collecté, il est associé à « recherche interne:winter chapeau ». Cela se produit jusqu’à ce que le paramètre d’expiration eVar soit atteint ou qu’une nouvelle valeur eVar6 soit définie et que l’événement de liaison se produise à nouveau avec ce produit.
3. L’utilisateur ajoute le produit à son panier, déclenchant l’événement `Cart Add`.
4. L’utilisateur effectue une autre recherche interne pour « Summer shirt », qui définit la syntaxe de conversion activée pour le marchandisage eVar6 sur « recherche interne :summer shirt ».
5. L’utilisateur sélectionne « t-shirt sportif » et accède à la page des détails du produit.\
   a. Landing ici déclenche un événement `Product View` pour « t-shirt sportif pour 19,99 $.\
   b. Comme l’événement `Product View` est l’événement de liaison, le produit « t-shirt sportif » est désormais lié à la valeur eVar6 de « recherche interne :summer chemise ». Le produit précédent « bonnet gaufre » est toujours lié à une valeur eVar6 de « recherche interne :waffle bonnet ».
6. L’utilisateur ajoute le produit à son panier, déclenchant l’événement `Cart Add`.
7. L’utilisateur procède au paiement des deux produits.

Dans le compte rendu des performances, les commandes, le chiffre d’affaires, les consultations de produits et les ajouts au panier sont comptabilisés dans eVar6 et correspondent à l’activité du produit lié.

| eVar6 (méthode de recherche de produit) | chiffre d’affaires | commandes | consultations de produit | ajouts au panier |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| recherche interne :summer chemise | 19,99 | 1 | 1 | 1 |
| recherche interne:winter chapeau | 12,99 | 1 | 1 | 1 |

Pour en savoir plus sur l’utilisation de la syntaxe de la variable de conversion, consultez la documentation d’Adobe Analytics sur l’[implémentation d’eVars à l’aide de la syntaxe de la variable de conversion](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=fr#implement-using-conversion-variable-syntax).

Les champs XDM affichés ci-dessous permettent de générer la syntaxe de la variable de conversion dans votre jeu de données [!DNL Analytics] :

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#` : variable eVar spécifique à laquelle vous accédez.

#### Produit

```console
productListItems[#].sku
```

* `#` : index du tableau auquel vous accédez.

## Cas d’utilisation des variables de conversion {#conversion-variable-use-cases}

Les cas d’utilisation ci-dessous représentent des scénarios qui nécessitent une syntaxe de variable de conversion.

### Lier la valeur à la paire produit-événement spécifique

La requête ci-dessous lie la valeur à la paire produit-événement spécifique. Dans cet exemple, la valeur est liée à l’événement d’affichage du produit.

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

### Conservez la valeur liée aux occurrences suivantes du produit correspondant

L’exemple de requête ci-dessous conserve la valeur liée aux occurrences suivantes du produit correspondant. La sous-requête la plus basse établit la relation de la valeur avec le produit sur l’événement de liaison déclaré. La sous-requête suivante effectue l’attribution de cette valeur liée lors des prochaines interactions avec le produit concerné. L’instruction SELECT de niveau supérieur agrège les résultats pour générer les rapports.

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

Grâce à la lecture de ce document, vous devriez mieux comprendre comment renvoyer une eVar de marchandisage à l’aide de la syntaxe du produit et lier une valeur à un produit spécifique avec la syntaxe de la variable de conversion.

Si vous ne l’avez pas déjà fait, nous vous invitons à lire la documentation [Analytics insights for web and mobile interactions](./analytics-insights.md) suivante. Il fournit des cas d’utilisation courants et montre comment utiliser Query Service pour créer des informations exploitables à partir de données Adobe Analytics web et mobiles.

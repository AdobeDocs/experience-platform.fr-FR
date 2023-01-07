---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;exemples de requêtes;exemple de requête;adobe analytics;
solution: Experience Platform
title: Exemples de requêtes pour les données Adobe Analytics
description: Les données des suites de rapports Adobe Analytics sélectionnées sont transformées en XDM ExperienceEvent et ingérées dans Adobe Experience Platform en tant que jeux de données. Ce document décrit un certain nombre de cas d’utilisation dans lesquels Query Service utilise ces données et inclut des exemples de requêtes conçues pour fonctionner avec vos jeux de données Adobe Analytics.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 41%

---

# Exemples de requêtes pour les données d’Adobe Analytics

Les données des suites de rapports Adobe Analytics sélectionnées sont transformées en données conformes au [!DNL XDM ExperienceEvent] et ingérés dans Adobe Experience Platform en tant que jeux de données.

Ce document décrit plusieurs cas d’utilisation de Adobe Experience Platform [!DNL Query Service] utilise ces données. Consultez la documentation relative à [Mappage des champs Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) pour plus d’informations sur le mappage à [!DNL Experience Events].

Voir [documentation sur les cas d’utilisation d’analytics](../use-cases/analytics-insights.md) pour savoir comment utiliser Query Service pour créer des informations exploitables à partir de données Adobe Analytics ingérées.

## Déduplication

[!DNL Query Service] prend en charge la déduplication des données. Voir [Déduplication des données dans [!DNL Query Service] documentation](../best-practices/deduplication.md) pour plus d’informations sur la génération de nouvelles valeurs au moment de l’interrogation. [!DNL Experience Event] jeux de données.

## Variables de marchandisage (syntaxe de produit)

Les sections suivantes contiennent des champs XDM et des exemples de requêtes que vous pouvez utiliser pour accéder aux variables de marchandisage de votre [!DNL Analytics] jeu de données.

### Syntaxe du produit

Dans Adobe Analytics, les données personnalisées au niveau du produit peuvent être collectées au moyen de variables configurées spécialement et appelées variables de marchandisage. Ils sont basés sur des événements d’eVar ou personnalisés. La différence entre ces variables et leur utilisation type est qu’elles représentent une valeur distincte pour chaque produit trouvé sur l’accès plutôt qu’une seule valeur pour l’accès.

Ces variables sont appelées variables de marchandisage de syntaxe de produit. Cela permet la collecte d’informations, telles qu’un &quot;montant de remise&quot; par produit ou des informations sur l’&quot;emplacement sur la page&quot; du produit dans les résultats de recherche du client.

Pour en savoir plus sur l’utilisation de la syntaxe du produit, consultez la documentation Adobe Analytics sur [implémentation d’eVars à l’aide de la syntaxe de produit](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

Les sections ci-dessous décrivent les champs XDM nécessaires pour accéder aux variables de marchandisage dans vos [!DNL Analytics] dataset:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: Index du tableau auquel vous accédez.
- `evar#`: La variable d’eVar spécifique à laquelle vous accédez.

#### Événements personnalisés

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: Index du tableau auquel vous accédez.
- `event#`: La variable d’événement personnalisé spécifique à laquelle vous accédez.

#### Exemples de requêtes

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

Cette requête suivante fait exploser le `productListItems` et renvoie chaque eVar de marchandisage et chaque événement par produit. Le champ `_id` est inclus pour indiquer la relation avec le résultat d’origine. Le `_id` est une clé Principale unique pour le jeu de données.

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
> Si vous tentez de récupérer un champ qui n’existe pas dans votre jeu de données actuel, l’erreur &quot;No such struct field&quot; (Aucun champ struct de ce type) se produira. Évaluez le motif renvoyé dans le message d’erreur pour identifier un champ disponible, puis mettez à jour votre requête et relancez l’exécution.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Syntaxe de conversion

La syntaxe de conversion est un autre type de variable de marchandisage qui se trouve dans Adobe Analytics. Avec la syntaxe du produit, la valeur est collectée en même temps que le produit, mais cela nécessite que les données soient présentes sur la même page. Il existe des scénarios où les données se produisent sur une page avant la conversion ou l’événement d’intérêt relatif au produit. Prenons l’exemple du cas d’utilisation de la méthode de recherche de produit.

1. Un utilisateur effectue une recherche interne pour « bonnet d’hiver », qui définit l’eVar6 de marchandisage avec syntaxe de conversion active sur « recherche interne : bonnet d’hiver ».
2. L’utilisateur clique sur « bonnet à pompon » et accède à la page détaillée du produit.\
   a. Cet accès déclenche un événement `Product View` pour le « bonnet à pompon » à 12,99 €.\
   b. Depuis `Product View` est configuré en tant qu’événement de liaison, le produit &quot;bonnet à pompon&quot; est désormais lié à la valeur eVar6 de &quot;recherche interne : bonnet d’hiver&quot;. Chaque fois que le produit « bonnet à pompon » est collecté, il est associé à « recherche interne : bonnet d’hiver » jusqu’à ce que (1) le paramètre d’expiration soit atteint ou (2) qu’une nouvelle valeur eVar6 soit définie et que l’événement de liaison se produise à nouveau pour ce produit.
3. L’utilisateur ajoute le produit à son panier, déclenchant l’événement `Cart Add`.
4. L’utilisateur effectue une autre recherche interne pour « T-shirt d’été », qui définit l’eVar6 de marchandisage avec syntaxe de conversion active sur « recherche interne : T-shirt d’été ».
5. L’utilisateur clique sur « T-shirt de sport » et accède à la page détaillée du produit.\
   a. Cet accès déclenche un événement `Product View` pour le « T-shirt de sport » à 19,99 €.\
   b. L’événement `Product View` reste notre événement de liaison, donc le produit « T-shirt de sport » est maintenant lié à la valeur eVar6 de « recherche interne : T-shirt d’été » et le produit précédent, « bonnet à pompon », reste lié à la valeur eVar6 de « recherche interne : bonnet hivernal ».
6. L’utilisateur ajoute le produit à son panier, déclenchant l’événement `Cart Add`.
7. L’utilisateur procède au paiement des deux produits.

Dans les rapports, les commandes, recettes, consultations de produit et ajouts au panier seront rapportés à eVar6 et s’aligneront sur l’activité du produit lié.

| eVar6 (méthode de recherche de produits) | recettes | commandes | consultations de produit | ajouts au panier |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| recherche interne : T-shirt d’été | 19,99 | 1 | 1 | 1 |
| recherche interne : bonnet d’hiver | 12,99 | 1 | 1 | 1 |

Pour en savoir plus sur l’utilisation de la syntaxe de conversion, consultez la documentation Adobe Analytics sur [implémentation d’eVars à l’aide de la syntaxe de conversion](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Voici les champs XDM pour générer la syntaxe de conversion dans votre [!DNL Analytics] dataset:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: La variable d’eVar spécifique à laquelle vous accédez.

#### Produit

```console
productListItems[#].sku
```

- `#`: Index du tableau auquel vous accédez.

#### Exemples de requêtes

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

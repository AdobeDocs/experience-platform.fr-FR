---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de requête ; service de Requête ; déduplication de données ; déduplication ;
solution: Experience Platform
title: Déduplication de données dans Requête Service
topic-legacy: queries
type: Tutorial
description: Ce document présente des exemples complets et de sous-sélection de requêtes pour dédupliquer trois cas d’utilisation courants Événements d’expérience, achats et mesures.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 18%

---

# Déduplication de données dans [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] prend en charge la déduplication des données. La déduplication de données peut être effectuée lorsqu’il est nécessaire de supprimer une ligne entière d’un calcul ou d’ignorer un ensemble de champs spécifique, car seule une partie des données de la ligne est des informations de duplicata.

La déduplication implique généralement l&#39;utilisation de la fonction `ROW_NUMBER()` sur une fenêtre pour un identifiant (ou une paire d&#39;identifiants) au fil du temps, ce qui renvoie un nouveau champ qui représente le nombre de fois où un duplicata a été détecté. L’heure est souvent représentée en utilisant le champ [!DNL Experience Data Model] (XDM) `timestamp`.

Lorsque la valeur de `ROW_NUMBER()` est `1`, elle fait référence à l’instance d’origine. En règle générale, il s’agit de l’instance que vous souhaitez utiliser. Cela se fait le plus souvent au sein d’une sous-sélection, dans laquelle le dédoublonnage est effectué avec une requête `SELECT` de niveau supérieur, comme le compte d’agrégats.

Les cas d&#39;utilisation de la déduplication peuvent être globaux ou limités à un seul utilisateur ou ID d&#39;utilisateur final dans `identityMap`.

Ce document décrit comment effectuer une déduplication pour trois cas d’utilisation courants : Événements d’expérience, achats et mesures.

Chaque exemple comprend la portée, la clé de fenêtre, un aperçu de la méthode de déduplication, ainsi que la requête SQL complète.

## Événements Experience {#experience-events}

Dans le cas des Événements d’expérience de duplicata, il est probable que vous souhaitiez ignorer la totalité de la ligne.

>[!CAUTION]
>
>De nombreux jeux de données dans [!DNL Experience Platform], y compris ceux produits par le connecteur de données Adobe Analytics, ont déjà une déduplication au niveau Événement d’expérience appliquée. Par conséquent, la réapplication de ce niveau de dédoublonnage est inutile et ralentira votre requête.
>
>Il est important de comprendre la source de vos jeux de données et de savoir si la déduplication au niveau du Événement d’expérience a déjà été appliquée. Pour tous les jeux de données diffusés en continu (par exemple, ceux d’Adobe Target), vous **devez** appliquer une déduplication au niveau Événement d’expérience, puisque ces sources de données ont une sémantique &quot;au moins une fois&quot;.

**Portée :** globale

**Touche de fenêtre :** `id`

### Exemple de déduplication

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Exemple complet

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## Achats {#purchases}

Si vous avez des achats de duplicata, vous souhaiterez probablement conserver la majeure partie de la ligne Événement d’expérience, mais ignorez les champs liés à l’achat (comme la mesure `commerce.orders`). Les achats contiennent un champ spécial pour l&#39;ID d&#39;achat, qui est `commerce.order.purchaseID`.

**Portée :** visiteur

**Clé de la fenêtre :** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### Exemple de déduplication

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

### Exemple complet

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## Mesures {#metrics}

Si une mesure utilise l’identifiant unique facultatif et qu’un duplicata de cet identifiant s’affiche, vous voudrez probablement ignorer cette valeur et conserver le reste du Événement d’expérience.

Dans XDM, la plupart des mesures utilisent le `Measure`type de données qui inclut un champ facultatif`id` que vous pouvez utiliser pour le dédoublonnage.

**Portée :** visiteur

**Clé de la fenêtre :** identityMap[$NAMESPACE].id &amp; id of Measure object

### Exemple de déduplication

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### Exemple complet

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## Étapes suivantes

Ce document décrit comment effectuer la déduplication de données dans Requête Service, ainsi que des exemples de déduplication de données. Pour plus d&#39;informations sur les meilleures pratiques lors de l&#39;écriture de requêtes à l&#39;aide de Requête Service, consultez le [guide de requêtes d&#39;écriture](./writing-queries.md).

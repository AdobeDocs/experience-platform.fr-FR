---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;déduplication des données;déduplication ;
solution: Experience Platform
title: Déduplication des données dans Query Service
topic-legacy: queries
type: Tutorial
description: 'Ce document présente des exemples de requêtes de sous-sélection et d’échantillon complet pour dédupliquer trois cas d’utilisation courants : Événements d’expérience, achats et mesures.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 18%

---

# Déduplication des données dans [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] prend en charge le dédoublonnage des données. La déduplication des données peut être effectuée lorsqu’il est nécessaire de supprimer une ligne entière d’un calcul ou d’ignorer un ensemble spécifique de champs, car seule une partie des données de la ligne est une duplication des informations.

La déduplication consiste généralement à utiliser la fonction `ROW_NUMBER()` sur une fenêtre pour un identifiant (ou une paire d’identifiants) au fil du temps ordonné, ce qui renvoie un nouveau champ qui représente le nombre de fois où un doublon a été détecté. L’heure est souvent représentée à l’aide du champ [!DNL Experience Data Model] (XDM) `timestamp` .

Lorsque la valeur de `ROW_NUMBER()` est `1`, elle fait référence à l’instance d’origine. En règle générale, il s’agit de l’instance que vous souhaitez utiliser. Cela se fait le plus souvent au sein d’une sous-sélection, dans laquelle le dédoublonnage est effectué avec une requête `SELECT` de niveau supérieur, comme le compte d’agrégats.

Les cas d’utilisation de déduplication peuvent être globaux ou limités à un seul utilisateur ou un identifiant d’utilisateur final dans `identityMap`.

Ce document décrit la procédure de déduplication pour trois cas d’utilisation courants : Événements d’expérience, achats et mesures.

Chaque exemple inclut le périmètre, la clé de fenêtre, une composition de la méthode de déduplication, ainsi que la requête SQL complète.

## Événements Experience {#experience-events}

Dans le cas d’événements d’expérience en double, vous souhaiterez probablement ignorer la ligne entière.

>[!CAUTION]
>
>De nombreux jeux de données dans [!DNL Experience Platform], y compris ceux générés par le connecteur de données Adobe Analytics, ont déjà été appliqués au dédoublonnage au niveau de l’événement d’expérience. Par conséquent, la réapplication de ce niveau de dédoublonnage est inutile et ralentira votre requête.
>
>Il est important de comprendre la source de vos jeux de données et de savoir si le dédoublonnage au niveau de l’événement d’expérience a déjà été appliqué. Pour tous les jeux de données diffusés en continu (par exemple, ceux d’Adobe Target), vous **devrez** appliquer une déduplication au niveau de l’événement d’expérience, car ces sources de données ont une sémantique &quot;au moins une fois&quot;.

**Portée :** globale

**Clé de la fenêtre :** `id`

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

Si vous avez des achats en double, vous souhaiterez probablement conserver la majeure partie de la ligne Événement d’expérience, mais ignorer les champs liés à l’achat (comme la mesure `commerce.orders`). Les achats contiennent un champ spécial pour l’identifiant d’achat, `commerce.order.purchaseID`.

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

Si une mesure utilise l’identifiant unique facultatif et qu’un doublon de cet identifiant apparaît, vous voudrez probablement ignorer cette valeur de mesure et conserver le reste de l’événement d’expérience.

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

Ce document décrit comment effectuer la déduplication des données dans Query Service, ainsi que des exemples de déduplication des données. Pour plus d’informations sur les bonnes pratiques à appliquer lors de l’écriture de requêtes à l’aide de Query Service, consultez le [guide sur l’écriture de requêtes](./writing-queries.md).

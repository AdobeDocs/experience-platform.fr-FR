---
keywords: Experience Platform;home;popular topics;query service;Query service;data deduplication;deduplication;
solution: Experience Platform
title: Dédoublonnage des données
topic: queries
type: Tutorial
description: 'Ce document présente des exemples complets et de sous-sélection de requêtes pour dédupliquer trois cas d’utilisation courants : Événements d’expérience, achats et mesures.'
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 71%

---


# Data deduplication in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] supports data deduplication when it may be required to remove an entire row from a calculation or ignore a specific set of fields because only part of the data in the row is a duplicate. The common pattern for deduplication involves using the `ROW_NUMBER()` function across a window for an ID, or pair of IDs, over ordered time (using the [!DNL Experience Data Model] (XDM) `timestamp` field) to return a new field that represents the number of times a duplicate has been detected. Lorsque cette valeur est `1`, elle fait référence à l’instance d’origine. Dans la plupart des cas, il s’agit de l’instance que vous souhaitez utiliser, ignorant ainsi toutes les autres instances. Cela se fait le plus souvent au sein d’une sous-sélection, dans laquelle le dédoublonnage est effectué avec une requête `SELECT` de niveau supérieur, comme le compte d’agrégats.

## Cas pratiques

Certains cas d’utilisation pour le dédoublonnage sont globaux dans la période spécifiée et d’autres sont limités à un seul identifiant de visiteur ou d’utilisateur final dans `identityMap`.

Ce document présente des exemples de requête de sous-sélection et d’échantillon complet pour le dédoublonnage de trois cas d’utilisation courants :
- [Instances ExperienceEvent](#experienceevents)
- [Achats](#purchases)
- [Mesures](#metrics)

### Instances ExperienceEvent {#experienceevents}

Dans le cas de doublons d’instances ExperienceEvent, vous souhaiterez probablement ignorer la ligne entière.

>[!CAUTION]
>
>Many DataSets in [!DNL Experience Platform], including those produced by the Adobe Analytics Data Connector, already have ExperienceEvent-level deduplication applied. Par conséquent, la réapplication de ce niveau de dédoublonnage est inutile et ralentira votre requête. Il est important de comprendre la source de vos jeux de données, et de savoir si le dédoublonnage d’instances ExperienceEvent a déjà été appliqué. Pour les jeux de données diffusés en continu (par exemple, ceux d’Adobe Target), vous devez appliquer un dédoublonnage d’instances ExperienceEvent car ces sources de données ont des sémantiques « au moins une fois ».

**Portée :** globale

**Clé de la fenêtre :** id

#### Sous-sélection

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### Exemple complet

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

### Achats {#purchases}

Dans le cas de doublons d’achats, vous souhaiterez probablement conserver la majeure partie de la ligne ExperienceEvent, mais ignorer les champs liés à l’achat (comme la mesure `commerce.orders`). Pour les achats, il existe un champ spécial pour l’identifiant d’achat. Ce champ est `commerce.order.purchaseID`.

**Portée :** visiteur

**Clé de la fenêtre :** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

#### Sous-sélection

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

#### Exemple complet

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

### Mesures {#metrics}

Si une mesure utilise l’identifiant unique facultatif et qu’un doublon de cet identifiant s’affiche, vous voudrez probablement ignorer cette valeur de mesure et conserver le reste de l’instance ExperienceEvent. Dans XDM, la plupart des mesures utilisent le `Measure`type de données qui inclut un champ facultatif`id` que vous pouvez utiliser pour le dédoublonnage.

**Portée :** visiteur

**Clé de la fenêtre :** identityMap[$NAMESPACE].id &amp; id of Measure object

#### Sous-sélection

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

#### Exemple complet

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

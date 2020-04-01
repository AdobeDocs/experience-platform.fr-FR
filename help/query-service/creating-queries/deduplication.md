---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' de données'
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


#  de données dans le service 

Le service de  de la plateforme Adobe Experience Platform prend en charge les de données  lorsqu’il peut être nécessaire de supprimer une ligne entière d’un calcul ou d’ignorer un ensemble spécifique de champs, car seule une partie des données de la ligne est un . Le modèle commun pour les  de consiste à utiliser la `ROW_NUMBER()` fonction sur une fenêtre pour un ID, ou une paire d’identifiants, au fil du temps (à l’aide du `timestamp` champ Modèle de données d’expérience (XDM)), afin de renvoyer un nouveau champ représentant le nombre de fois où un  de a été détecté. Lorsque cette valeur est `1`, elle fait référence à l’instance d’origine et, dans la plupart des cas, à l’instance que vous souhaitez utiliser, en ignorant toutes les autres instances. Cela se fait le plus souvent au sein d’une sous-sélection où le  est effectué à un niveau supérieur `SELECT` comme l’exécution d’un  nombre de.

## Cas d’utilisation

Certains cas d’utilisation pour les  de sont globaux dans la plage de dates et d’autres sont limités à un seul ou un seul ID d’utilisateur final dans la `identityMap`plage.

Ce  des exemples de sous-sélection et de  d’échantillon complet pour la déduplication de trois cas d’utilisation courants :
- [ExperienceEvents](#experienceevents)
- [Achats](#purchases)
- [Mesures](#metrics)

### ExperienceEvents {#experienceevents}

Dans le cas d’ ExperienceEvents, vous souhaiterez probablement ignorer la ligne entière.

>[!CAUTION] De nombreuses visionneuses de données dans la plateforme d’expérience, y compris celles produites par le connecteur de données Adobe Analytics, sont déjà  au niveau d’ExperienceEvent. Par conséquent, la réapplication de ce niveau de  est inutile et ralentira votre  de. Il est important de comprendre la source de vos DataSet et de savoir si des  au niveau de l’événement ExperienceEvent ont déjà été appliquées. Pour les DataSet en flux continu (par exemple, ceux d’Adobe), vous devez appliquer un au niveau d’ExperienceEvent  car ces sources de données ont une sémantique &quot;au moins une fois&quot;.

**Portée :** Global

**Touche Fenêtre :** id

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

Si vous avez des achats, vous souhaiterez probablement conserver la majeure partie de la ligne ExperienceEvent, mais ignorez les champs liés à l’achat (comme la `commerce.orders` mesure). Pour les achats, il existe un champ spécial pour l’ID d’achat. Ce champ est `commerce.order.purchaseID`.

**Portée :** {&quot;N&quot;:{&quot;visiteuse&quot;:[&quot;fs&quot;],&quot;visiteuses&quot;:[&quot;fp&quot;],&quot;visiteurs&quot;:[&quot;mp&quot;],&quot;visiteur&quot;:[&quot;ms&quot;]}} 

**Touche Fenêtre :** identityMap[$].id et commerce.order.purchaseID

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

Si une mesure utilise l’ID unique facultatif et qu’un de cet ID s’affiche, vous voudrez probablement ignorer cette valeur de mesure et conserver le reste de l’événement ExperienceEvent. Dans XDM, la plupart des mesures utilisent le type de `Measure` données qui inclut un `id` champ facultatif que vous pouvez utiliser pour les  de.

**Portée :** {&quot;N&quot;:{&quot;visiteuse&quot;:[&quot;fs&quot;],&quot;visiteuses&quot;:[&quot;fp&quot;],&quot;visiteurs&quot;:[&quot;mp&quot;],&quot;visiteur&quot;:[&quot;ms&quot;]}} 

**Touche Fenêtre :** identityMap[$ objet].id et id de mesure

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

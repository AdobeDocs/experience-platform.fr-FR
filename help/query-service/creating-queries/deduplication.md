---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: déduplication de données
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---


# déduplication de données dans Requête Service

Adobe Experience Platform Requête Service prend en charge la déduplication des données lorsqu’il peut être nécessaire de supprimer une ligne entière d’un calcul ou d’ignorer un ensemble de champs spécifique, car seule une partie des données de la ligne est un duplicata. Le modèle de déduplication commun consiste à utiliser la `ROW_NUMBER()` fonction sur une fenêtre pour un identifiant, ou une paire d’identifiants, au fil du temps (à l’aide du `timestamp` champ Modèle de données d’expérience (XDM)) pour renvoyer un nouveau champ qui représente le nombre de fois où un duplicata a été détecté. Lorsque cette valeur est définie `1`, elle fait référence à l’instance d’origine et, dans la plupart des cas, à l’instance que vous souhaitez utiliser, en ignorant toutes les autres instances. Cela se fait le plus souvent dans une sous-sélection où la déduplication est effectuée à un niveau supérieur, `SELECT` comme l’exécution d’un nombre d’agrégats.

## Cas d’utilisation

Certains cas d’utilisation pour la déduplication sont globaux dans la plage de dates et certains sont limités à un seul visiteur ou un seul ID d’utilisateur final dans la `identityMap`plage.

Ce document présente des exemples de requêtes sous-sélectionnés et complets pour la déduplication de trois cas d’utilisation courants :
- [ExperienceEvents](#experienceevents)
- [Achats](#purchases)
- [Mesures](#metrics)

### ExperienceEvents {#experienceevents}

Dans le cas des événements d’expérience de duplicata, vous souhaiterez probablement ignorer la totalité de la ligne.

>[!CAUTION]
>
>De nombreux DataSets en Experience Platform, y compris ceux produits par le Analytics Data Connector, utilisent déjà une déduplication au niveau d’ExperienceEvent. Par conséquent, la réapplication de ce niveau de déduplication est inutile et ralentira votre requête. Il est important de comprendre la source de vos DataSets et de savoir si la déduplication au niveau d’ExperienceEvent a déjà été appliquée. Pour les DataSets en flux continu (par exemple, ceux d’Adobe Target), vous devez appliquer une déduplication au niveau d’ExperienceEvent car ces sources de données ont une sémantique &quot;au moins une fois&quot;.

**Portée :** Global

**Touche de fenêtre :** id

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

Si vous effectuez des achats par duplicata, vous souhaiterez probablement conserver la majeure partie de la ligne ExperienceEvent, mais ignorer les champs liés à l’achat (par exemple la `commerce.orders` mesure). Pour les achats, il existe un champ spécial pour l’ID d’achat. Ce champ est `commerce.order.purchaseID`.

**Portée :** Visiteur

**Touche de fenêtre :** identityMap[$ESPACE DE NOMMAGE].id et commerce.order.purchaseID

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

Si une mesure utilise l’identifiant unique facultatif et qu’un duplicata de cet identifiant s’affiche, vous voudrez probablement ignorer cette valeur et conserver le reste de l’événement ExperienceEvent. Dans XDM, la plupart des mesures utilisent le type de `Measure` données qui inclut un champ facultatif `id` que vous pouvez utiliser pour la déduplication.

**Portée :** Visiteur

**Touche de fenêtre :** identityMap[$ESPACE DE NOMMAGE].id et id de l&#39;objet Measure

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

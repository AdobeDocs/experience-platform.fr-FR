---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;exemples de requêtes;exemple de requête;adobe target;
solution: Experience Platform
title: Exemples de requêtes pour les données Adobe Target
topic-legacy: queries
description: Les données issues d’Adobe Target sont transformées en schéma de modèle de données d’expérience et ingérées dans Experience Platform en tant que jeux de données. Ce document contient des exemples de requêtes pour utiliser Query Service avec vos jeux de données Adobe Target.
exl-id: 0ab3cd6e-25ed-43dc-b8f0-a2b71621ae50
source-git-commit: 76847d8286776a554e55209fa1b334c98b02d76b
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 52%

---

# Exemples de requêtes pour les données d’Adobe Target

Les données ingérées à partir d’Adobe Target sont transformées en schéma XDM d’événement d’expérience et ingérées dans Adobe Experience Platform en tant que jeux de données. Adobe Experience Platform Query Service facilite de nombreux cas d’utilisation de ces données. Les exemples de requêtes suivants doivent fonctionner avec vos jeux de données Adobe Target.

Dans Experience Platform, le nom d’un jeu de données créé automatiquement est &quot;Événements d’expérience Adobe Target&quot;. Lors de l’utilisation de ce jeu de données avec des requêtes, utilisez le nom `adobe_target_experience_events`.

## Mappage de champs XDM partiels de haut niveau

La liste suivante répertorie les champs Target qui correspondent aux champs XDM correspondants.

>[!NOTE]
>
> L’utilisation de `[ ]` dans le champ XDM indique un tableau.

- mboxName: `_experience.target.mboxname`
- Identifiant d’activité: `_experience.target.activities.activityID`
- Identifiant d’expérience: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- Identifiant de segment: `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- Portée d’événement: `_experience.target.activities[].activityEvents[].eventScope`
   - Ce champ effectue le suivi des nouveaux visiteurs et visites.
- Identifiant d’étape: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - Ce champ est un ID d’étape personnalisé pour Adobe Campaign.
- Prix total: `commerce.order.priceTotal`

## Exemples de requêtes

Les requêtes suivantes présentent des exemples de requêtes fréquemment utilisées avec Adobe Target.

Dans les exemples suivants, vous devrez modifier le code SQL pour remplir les paramètres attendus pour vos requêtes en fonction du jeu de données, des variables ou de la période que vous souhaitez évaluer. Spécifiez les paramètres partout où vous voyez `{ }` dans le SQL.

### Décomptes horaires d’activité pour un jour spécifique

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### Détails horaires d’une activité spécifique pour un jour spécifique

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### Identifiants Experience d’une activité précise pour un jour spécifique

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Renvoie une liste de portées d’événement (visiteurs, visite, impression), par instances, par identifiant d’activité pour un jour spécifique

```sql
SELECT
  Day,
  Activities.activityID,
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

### Renvoie le nombre de visiteurs, de visites et d’impressions par activité pour un jour spécifique

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

### Renvoie les visiteurs, les visites, les impressions pour un identifiant Experience, l’identifiant de segment et la portée d’événement pour un jour spécifique

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE 
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

### Renvoie les noms mbox et le nombre d’enregistrements pour un jour spécifique

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```

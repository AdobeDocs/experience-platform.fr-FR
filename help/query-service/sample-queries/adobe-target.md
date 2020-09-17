---
keywords: Experience Platform;home;popular topics;query service;Query service;sample queries;sample query;adobe target;
solution: Experience Platform
title: Exemples de requêtes
topic: queries
translation-type: tm+mt
source-git-commit: f9749dbc5f2e3ac15be50cc5317ad60586b2c07e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 82%

---


# Exemples de requêtes pour les données d’Adobe Target

Data from Adobe Target is transformed into Experience Event XDM schema and ingested into [!DNL Experience Platform] as datasets for you. There are many use cases for [!DNL Query Service] with this data, and the following sample queries should work with your Adobe Target datasets.

>[!NOTE]
>
>Dans les exemples suivants, vous devrez modifier le code SQL pour remplir les paramètres attendus pour vos requêtes en fonction du jeu de données, des variables ou de la période que vous souhaitez évaluer. Spécifiez les paramètres partout où vous voyez `{ }` dans le SQL.

## Nom de jeu de données standard pour la source de données cible sur [!DNL Platform]:

Événements d’expérience Adobe Target (nom convivial) <br>
`adobe_target_experience_events` (nom à utiliser dans la requête)

## Mappage de champs XDM partiels de haut niveau

L’utilisation de `[ ]` signale un tableau

| Nom | Champ XDM | Notes |
| ---- | --------- | ----- |
| mboxName | `_experience.target.mboxname` |  |
| Identifiant d’activité | `_experience.target.activities.activityID` |  |
| Identifiant d’expérience | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` |  |
| Identifiant de segment | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` |  |
| Portée d’événement | `_experience.target.activities[].activityEvents[].eventScope` | Suivi des nouveaux visiteurs et des nouvelles visites |
| Identifiant d’étape | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Identifiant d’étape personnalisée pour Campaign |
| Total prix | `commerce.order.priceTotal` |  |

## Décomptes horaires d’activité pour un jour spécifique

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
  WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

## Détails horaires d’une activité spécifique pour un jour spécifique

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
    TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

## Identifiants Experience d’une activité précise pour un jour spécifique

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
      TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

## Renvoie une liste de portées d’événement (visiteurs, visite, impression), par instances, par identifiant d’activité pour un jour spécifique

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
      TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

## Renvoie le nombre de visiteurs, de visites et d’impressions par activité pour un jour spécifique

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
    TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

## Renvoie les visiteurs, les visites, les impressions pour un identifiant Experience, l’identifiant de segment et la portée d’événement pour un jour spécifique

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
        TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
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

## Renvoie les noms mbox et le nombre d’enregistrements pour un jour spécifique

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```

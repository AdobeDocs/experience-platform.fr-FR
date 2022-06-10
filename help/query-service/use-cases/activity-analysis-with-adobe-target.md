---
title: Analyse des activités avec Adobe Target
description: Ce document explique comment utiliser Query Service pour créer des informations exploitables à partir de jeux de données créés avec vos données Adobe Target.
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 12%

---

# Analyse des activités avec Adobe Target

Adobe Experience Platform vous permet d’ingérer des données à partir d’Adobe Target à l’aide de champs de modèle de données d’expérience (XDM) afin de créer des jeux de données à utiliser avec Query Service. Adobe Target étant conçu pour personnaliser le contenu et les expériences utilisateur, les requêtes exécutées sur ces jeux de données permettent d’obtenir des informations hautement personnalisées et ciblées en analysant l’activité des utilisateurs via SQL.

Ce document fournit divers exemples de requêtes SQL qui montrent des cas d’utilisation courants en fonction des comportements et des caractéristiques des clients.

## Prise en main

Pour chacun des cas d’utilisation suivants, un exemple de requête SQL paramétré est fourni comme modèle que vous pouvez personnaliser. Fournir des paramètres partout où vous voyez `{ }` dans les exemples SQL que vous souhaitez évaluer.

## Mappage de champs XDM partiels de haut niveau

Le tableau suivant répertorie les champs cibles communs et les champs XDM correspondants vers lesquels ils sont mappés.

>[!NOTE]
>
>L’utilisation de `[ ]` dans le champ XDM indique un tableau.

| Nom du champ cible | Nom du champ XDM | Notes |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | S/O |
| Identifiant d’activité | `_experience.target.activities.activityID` | S/O |
| Identifiant d’expérience | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | S/O |
| Identifiant de segment | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | S/O |
| Portée d’événement | `_experience.target.activities[].activityEvents[].eventScope` | Ce champ effectue le suivi des nouveaux visiteurs et visites. |
| Identifiant d’étape | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Ce champ est un ID d’étape personnalisé pour Adobe Campaign. |
| Prix total | commerce.order.priceTotal | S/O |

>[!IMPORTANT]
>
>Le nom d’un jeu de données automatiquement créé à l’aide des données Target est &quot;Événements d’expérience Adobe Target&quot;. Lors de l’utilisation de ce jeu de données avec des requêtes, utilisez le nom `adobe_target_experience_events`.

## Objectifs

En analysant les activités des utilisateurs, vous pouvez personnaliser le contenu pour une audience spécifique et tester différentes versions du contenu pour une entité individuelle. En outre, l’analyse d’une activité spécifique sur une période donnée ou pour des utilisateurs individuels permet de mieux comprendre les performances de chaque activité. Les résultats de cette analyse combinée peuvent être utilisés pour comprendre les performances de chaque activité.

Les cas d’utilisation de personnalisation suivants sont créés à l’aide des données Adobe Target et se concentrent sur les activités des utilisateurs afin de créer des informations précieuses sur le comportement des clients par rapport aux applications commerciales.

Ce guide illustre les concepts clés suivants à travers des exemples de cas d’utilisation :

* Pour comprendre les performances d’un ID d’activité pour un jour donné, telles que le nombre, les détails et les ID d’expérience associés.
* Pour déterminer la portée du visiteur et de l’événement pour une activité.
* Pour rassembler le nombre de visiteurs, de visites et d’informations d’impression pour l’Experience ID, l’identifiant de segment et l’identifiant d’activité.

### Générer le décompte horaire de l’activité pour un jour donné

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

### Générer des détails horaires pour un

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

### Déterminer la liste des ID d’expérience pour une activité spécifique pour un jour donné

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

### Déterminer le nombre de visiteurs, de visites et d’impressions par activité pour un jour donné

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

### Déterminer les visiteurs, les visites et les impressions pour l’Experience ID, l’identifiant de segment et la portée de l’événement pour un jour donné

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

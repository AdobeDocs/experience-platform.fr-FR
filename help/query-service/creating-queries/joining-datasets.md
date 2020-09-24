---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: Association de jeux de données
topic: queries
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 100%

---


# Association de jeux de données

L’association de jeux de données vous permet d’inclure dans votre requête des données provenant d’autres jeux de données. Cet exemple utilise un jeu de données personnalisé provenant du système d’exploitation pour mapper la valeur `operatingsystemID` à la valeur `operatingsystem`.

Jeux de données :
- your_analytics_table
- custom_operating_system_lookup

Créez une instruction `SELECT` pour les 50 premiers systèmes d’exploitation classés par nombre de visites des pages.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Image](../images/queries/joining-datasets/select-operating-systems.png)
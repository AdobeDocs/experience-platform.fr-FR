---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Regroupement de jeux de données
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 3%

---


# Regroupement de jeux de données

La jonction de jeux de données vous permet d&#39;inclure dans votre requête des données provenant d&#39;autres jeux de données. Cet exemple utilise un jeu de données personnalisé du système d’exploitation pour mapper le `operatingsystemID` paramètre à la `operatingsystem` valeur.

Jeux de données:
- your_analytics_table
- custom_operating_system_lookup

Créez une `SELECT` instruction pour les 50 premiers systèmes d’exploitation par nombre de vues de page.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE _ACP_YEAR=2018 
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Image](../images/queries/joining-datasets/select-operating-systems.png)
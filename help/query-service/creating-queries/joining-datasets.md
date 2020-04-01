---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Jonction de jeux de données
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Jonction de jeux de données

L’association de jeux de données vous permet d’inclure dans votre  des données provenant d’autres jeux de données. Cet exemple utilise un jeu de données personnalisé du système d’exploitation pour mapper la `operatingsystemID` valeur à la `operatingsystem` valeur.

Jeux de données:
- your_analytics_table
- custom_operating_system_lookup

Créez une `SELECT` instruction pour les 50 premiers systèmes d’exploitation par nombre de  de page.

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
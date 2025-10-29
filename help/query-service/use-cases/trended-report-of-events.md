---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;requêtes experienceevent;requête experienceevent;requête Experience Event;
title: Création d’un rapport de tendances d’événements
description: Découvrez comment écrire des requêtes qui utilisent des événements d’expérience pour créer un rapport de tendances d’événements sur une période spécifiée, regroupés par date.
exl-id: 8f7ed5b5-c265-4a1e-a360-4293d1e86e97
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# Créer un rapport de tendance d’événements

Ce document fournit un exemple de code SQL requis pour créer un rapport de tendances d’événements par jour sur une période spécifique. Avec Adobe Experience Platform Query Service, vous pouvez écrire des requêtes qui utilisent [!DNL Experience Events] pour capturer divers cas d’utilisation. Les événements d’expérience sont représentés par la classe ExperienceEvent du modèle de données d’expérience (XDM), qui capture un instantané non modifiable et non agrégé du système lorsqu’un utilisateur interagit avec un site web ou un service. Les événements d’expérience peuvent même être utilisés pour l’analyse de domaine temporel. Voir la [section étapes suivantes](#next-steps) pour d’autres cas d’utilisation qui impliquent des [!DNL Experience Events] pour générer des rapports de visiteur.

Les rapports vous donnent accès aux données Experience Platform afin de bénéficier des informations commerciales stratégiques de votre organisation. Grâce à ces rapports, vous pouvez examiner vos données Experience Platform de différentes manières, afficher les mesures clés dans des formats faciles à comprendre et partager les informations qui en résultent.

Vous trouverez plus d’informations sur XDM et [!DNL Experience Events] dans la [[!DNL XDM System] présentation](../../xdm/home.md). En combinant Query Service à [!DNL Experience Events], vous pouvez suivre efficacement les tendances comportementales parmi vos utilisateurs. Le document suivant fournit des exemples de requêtes impliquant des [!DNL Experience Events].

## Objectifs

L’exemple suivant crée un rapport de tendance d’événements sur une période donnée avec un regroupement par date. Plus précisément, cet exemple SQL résume diverses valeurs d’analyse sous la forme `A`, `B` et `C`, puis additionne le nombre de fois où les parkas ont été consultés sur une période d’un mois.

La colonne d’horodatage trouvée dans [!DNL Experience Event] jeux de données est au format UTC. L’exemple utilise la fonction `from_utc_timestamp()` pour transformer l’horodatage UTC en EDT, puis utilise la fonction `date_format()` pour isoler la date du reste de l’horodatage.

```sql
SELECT 
date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
SUM(web.webPageDetails.pageviews.value) as pageViews,
SUM(_experience.analytics.event1to100.event1.value) as A,
SUM(_experience.analytics.event1to100.event2.value) as B,
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE TIMESTAMP >= to_timestamp('2019-03-01') AND TIMESTAMP <= to_timestamp('2019-03-31')
GROUP BY Day 
ORDER BY Day ASC, pageViews DESC;
```

Les résultats de cette requête sont visibles ci-dessous.

```console
     Day     | pageViews |   A    |   B   |    C    | viewedParkas
|-------------+-----------+--------+-------+---------+--------------
 2019-03-01  |   55317.0 | 8503.0 | 804.0 | 1578.0  |           73
 2019-03-02  |   55302.0 | 8600.0 | 854.0 | 1528.0  |           86
 2019-03-03  |   54613.0 | 8162.0 | 795.0 | 1568.0  |          100
 2019-03-04  |   54501.0 | 8479.0 | 832.0 | 1509.0  |          100
 2019-03-05  |   54941.0 | 8603.0 | 816.0 | 1514.0  |           73
 2019-03-06  |   54817.0 | 8434.0 | 855.0 | 1538.0  |           76
 2019-03-07  |   55201.0 | 8604.0 | 843.0 | 1517.0  |           64
 2019-03-08  |   55020.0 | 8490.0 | 849.0 | 1536.0  |           99
 2019-03-09  |   43186.0 | 6736.0 | 643.0 | 1150.0  |           52
 2019-03-10  |   48471.0 | 7542.0 | 772.0 | 1272.0  |           70
 2019-03-11  |   56307.0 | 8721.0 | 818.0 | 1571.0  |           81
 2019-03-12  |   55374.0 | 8653.0 | 843.0 | 1501.0  |           59
 2019-03-13  |   55046.0 | 8509.0 | 887.0 | 1556.0  |           65
 2019-03-14  |   55518.0 | 8551.0 | 848.0 | 1516.0  |           77
 2019-03-15  |   55329.0 | 8575.0 | 818.0 | 1607.0  |           96
 2019-03-16  |   55030.0 | 8651.0 | 815.0 | 1542.0  |           66
 2019-03-17  |   55143.0 | 8435.0 | 774.0 | 1572.0  |           65
 2019-03-18  |   54065.0 | 8211.0 | 816.0 | 1574.0  |          111
 2019-03-19  |   55097.0 | 8395.0 | 771.0 | 1498.0  |           86
 2019-03-20  |   55198.0 | 8472.0 | 863.0 | 1583.0  |           82
 2019-03-21  |   54978.0 | 8490.0 | 820.0 | 1580.0  |           83
 2019-03-22  |   55464.0 | 8561.0 | 820.0 | 1559.0  |           83
 2019-03-23  |   55384.0 | 8482.0 | 800.0 | 1139.0  |           82
 2019-03-24  |   55295.0 | 8594.0 | 841.0 | 1382.0  |           78
 2019-03-25  |   42069.0 | 6365.0 | 606.0 | 1509.0  |           62
 2019-03-26  |   49724.0 | 7629.0 | 724.0 | 1553.0  |           44
 2019-03-27  |   55111.0 | 8524.0 | 804.0 | 1524.0  |           94
 2019-03-28  |   55030.0 | 8439.0 | 822.0 | 1554.0  |           73
 2019-03-29  |   55281.0 | 8601.0 | 854.0 | 1580.0  |           73
 2019-03-30  |   55162.0 | 8538.0 | 846.0 | 1534.0  |           79
 2019-03-31  |   55437.0 | 8486.0 | 807.0 | 1649.0  |           68
 (31 rows)
```

## Étapes suivantes {#next-steps}

Grâce à la lecture de ce document, vous comprenez mieux comment utiliser Query Service avec [!DNL Experience Events] pour effectuer un suivi efficace des tendances comportementales parmi vos utilisateurs.

Pour en savoir plus sur d’autres cas d’utilisation basés sur les visiteurs qui utilisent [!DNL Experience Events], lisez les documents suivants :

- [Récupérez une liste des visiteurs organisée par nombre de pages vues.](./visitors-by-number-of-page-views.md)
- [Répertorier les sessions précédentes d’un visiteur.](./list-visitor-sessions.md)
- [Affichez un rapport de cumul d’un visiteur.](./roll-up-report-of-a-visitor.md)

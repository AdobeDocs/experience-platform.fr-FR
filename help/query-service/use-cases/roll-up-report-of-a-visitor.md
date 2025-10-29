---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;requêtes experienceevent;requête experienceevent;requête Experience Event;
title: Affichage d’un rapport de cumul pour un visiteur spécifique
description: Le document suivant fournit des exemples de requêtes impliquant des événements d’expérience dans Adobe Experience Platform Query Service.
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Affichage d’un rapport de cumul pour un visiteur spécifique

Ce document fournit un exemple SQL permettant d’agréger des données provenant de plusieurs propriétés Analytics pour un utilisateur spécifique et de les afficher ensemble dans un seul rapport. Avec Adobe Experience Platform Query Service, vous pouvez écrire des requêtes qui utilisent [!DNL Experience Events] pour capturer divers cas d’utilisation. Les événements d’expérience sont représentés par la classe ExperienceEvent du modèle de données d’expérience (XDM), qui capture un instantané non modifiable et non agrégé du système lorsqu’un utilisateur interagit avec un site web ou un service. Les événements d’expérience peuvent même être utilisés pour l’analyse de domaine temporel. Voir la [section étapes suivantes](#next-steps) pour d’autres cas d’utilisation qui impliquent des [!DNL Experience Events] pour générer des rapports de visiteur.

Vous trouverez plus d’informations sur XDM et [!DNL Experience Events] dans la [[!DNL XDM System] présentation](../../xdm/home.md). En combinant Query Service à [!DNL Experience Events], vous pouvez suivre efficacement les tendances comportementales parmi vos utilisateurs. Le document suivant fournit des exemples de requêtes impliquant des [!DNL Experience Events].

## Objectif

L’exemple SQL suivant montre comment afficher un rapport agrégé de différentes valeurs d’analyse pour un utilisateur spécifié.

```sql
SELECT 
endUserIds._experience.aaid.id, 
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
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

Les résultats de la requête sont affichés dans le tableau ci-dessous.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
|----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Étapes suivantes {#next-steps}

La lecture de ce document vous permet de mieux comprendre comment utiliser Query Service avec [!DNL Experience Events] pour afficher un rapport agrégé de valeurs d’analyse pour un utilisateur spécifié.

Consultez les cas d’utilisation suivants pour en savoir plus sur d’autres cas d’utilisation basés sur les visiteurs :

- [Récupérez une liste des visiteurs organisée par nombre de pages vues.](./visitors-by-number-of-page-views.md)
- [Répertorier les sessions précédentes d’un visiteur.](./list-visitor-sessions.md)
- [Créez un rapport de tendances des événements par jour.](./trended-report-of-events.md)

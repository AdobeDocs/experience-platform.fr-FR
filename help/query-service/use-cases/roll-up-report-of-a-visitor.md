---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;requêtes experienceevent;requête experienceevent;requête Experience Event;
title: Affichage d’un rapport de cumul pour un visiteur spécifique
description: Le document suivant fournit des exemples de requêtes impliquant des événements d’expérience dans Adobe Experience Platform Query Service.
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Affichage d’un rapport de cumul pour un visiteur spécifique

Ce document fournit un exemple SQL pour agréger des données provenant de plusieurs propriétés d’analyse pour un utilisateur spécifique et afficher ces données ensemble dans un rapport. Avec Adobe Experience Platform Query Service, vous pouvez écrire des requêtes qui utilisent [!DNL Experience Events] pour capturer divers cas d’utilisation. Les événements d’expérience sont représentés par la classe ExperienceEvent du modèle de données d’expérience (XDM), qui capture un instantané non agrégé et immuable du système lorsqu’un utilisateur interagit avec un site web ou un service. Les événements d’expérience peuvent même être utilisés pour l’analyse du domaine temporel. Pour plus d’informations sur les cas d’utilisation qui impliquent [!DNL Experience Events] pour générer des rapports sur les visiteurs, reportez-vous à la section [étapes suivantes](#next-steps) .

Vous trouverez plus d’informations sur XDM et [!DNL Experience Events] dans la [[!DNL XDM System] présentation](../../xdm/home.md). En combinant Query Service à [!DNL Experience Events], vous pouvez effectuer un suivi efficace des tendances comportementales parmi vos utilisateurs. Le document suivant fournit des exemples de requêtes impliquant [!DNL Experience Events].

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
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Étapes suivantes {#next-steps}

En lisant ce document, vous comprenez mieux comment utiliser Query Service avec [!DNL Experience Events] pour afficher un rapport agrégé de valeurs d’analyse pour un utilisateur spécifié.

Consultez les cas d’utilisation suivants pour en savoir plus sur d’autres cas d’utilisation basés sur les visiteurs :

- [Récupérez une liste de visiteurs organisée par nombre de pages vues.](./visitors-by-number-of-page-views.md)
- [Liste des sessions précédentes d’un visiteur.](./list-visitor-sessions.md)
- [Créez un rapport de tendance d’événements par jour.](./trended-report-of-events.md)

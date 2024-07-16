---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;requêtes experienceevent;requête experienceevent;requête Experience Event;
title: Liste des pages vues d’un utilisateur
description: Découvrez comment écrire des requêtes qui utilisent les événements d’expérience pour créer une liste des 100 dernières pages utilisées par un utilisateur spécifié.
exl-id: d831910d-d3a4-4a5a-b897-b09f0546dab0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 8%

---

# Répertorier les pages vues d’un utilisateur ou d’une utilisatrice

Ce document fournit un exemple du code SQL requis pour répertorier les pages vues par un utilisateur spécifié. Avec Adobe Experience Platform Query Service, vous pouvez écrire des requêtes qui utilisent [!DNL Experience Events] pour capturer divers cas d’utilisation. Les événements d’expérience sont représentés par la classe ExperienceEvent du modèle de données d’expérience (XDM), qui capture un instantané non agrégé et immuable du système lorsqu’un utilisateur interagit avec un site web ou un service. Les événements d’expérience peuvent même être utilisés pour l’analyse du domaine temporel. Pour plus d’informations sur les cas d’utilisation qui impliquent [!DNL Experience Events] pour générer des rapports sur les visiteurs, reportez-vous à la section [étapes suivantes](#next-steps) .

Vous trouverez plus d’informations sur XDM et [!DNL Experience Events] dans la [[!DNL XDM System] présentation](../../xdm/home.md). En combinant Query Service à [!DNL Experience Events], vous pouvez effectuer un suivi efficace des tendances comportementales parmi vos utilisateurs. Le document suivant fournit des exemples de requêtes impliquant [!DNL Experience Events].

## Objectif

L’exemple suivant liste les 100 dernières pages consultées par un utilisateur spécifique.

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

Les résultats de cette requête sont présentés ci-dessous.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## Étapes suivantes {#next-steps}

En lisant ce document, vous comprenez mieux comment utiliser Query Service avec [!DNL Experience Events] pour répertorier les pages vues en tant qu’utilisateur spécifié.

Consultez les cas d’utilisation suivants pour en savoir plus sur d’autres cas d’utilisation basés sur les visiteurs :

- [Récupérez une liste de visiteurs organisée par nombre de pages vues.](./visitors-by-number-of-page-views.md)
- [Affiche un rapport de cumul d’un visiteur.](./roll-up-report-of-a-visitor.md)
- [Créez un rapport de tendance d’événements par jour.](./trended-report-of-events.md)

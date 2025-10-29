---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;requêtes experienceevent;requête experienceevent;requête Experience Event;
title: Répertorier les visiteurs et visiteuses par nombre de pages vues
description: Découvrez comment écrire des requêtes qui utilisent des événements d’expérience pour récupérer une liste de visiteurs organisée par le nombre de pages vues.
exl-id: 6e8eed0c-838e-4cd0-ae8c-453114fbf4ea
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---

# Répertorier les visiteurs et visiteuses selon leur nombre de pages vues

Ce document fournit un exemple du langage SQL requis pour récupérer une liste de visiteurs organisée par le nombre de pages vues. Avec Adobe Experience Platform Query Service, vous pouvez écrire des requêtes qui utilisent [!DNL Experience Events] pour capturer divers cas d’utilisation. Les événements d’expérience sont représentés par la classe ExperienceEvent du modèle de données d’expérience (XDM), qui capture un instantané non modifiable et non agrégé du système lorsqu’un utilisateur interagit avec un site web ou un service. Les événements d’expérience peuvent même être utilisés pour l’analyse de domaine temporel. Voir la [section étapes suivantes](#next-steps) pour d’autres cas d’utilisation qui impliquent des [!DNL Experience Events] pour générer des rapports de visiteur.

Vous trouverez plus d’informations sur XDM et [!DNL Experience Events] dans la [[!DNL XDM System] présentation](../../xdm/home.md). En combinant Query Service à [!DNL Experience Events], vous pouvez suivre efficacement les tendances comportementales parmi vos utilisateurs. Le document suivant fournit des exemples de requêtes impliquant des [!DNL Experience Events].

## Objectif

L&#39;exemple suivant crée un rapport qui répertorie les 10 identifiants des utilisateurs qui ont consulté le plus de pages.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

Les résultats de la requête sont affichés dans le tableau ci-dessous.

```console
               id                  | pageViews
|-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## Étapes suivantes {#next-steps}

Grâce à la lecture de ce document, vous comprenez mieux comment utiliser Query Service avec [!DNL Experience Events] pour répertorier les utilisateurs qui ont consulté le plus de pages.

Consultez les cas d’utilisation suivants pour en savoir plus sur d’autres cas d’utilisation basés sur les visiteurs :

- [Répertorier les sessions précédentes d’un visiteur.](./list-visitor-sessions.md)
- [Affichez un rapport de cumul d’un visiteur.](./roll-up-report-of-a-visitor.md)
- [Créez un rapport de tendances des événements par jour.](./trended-report-of-events.md)

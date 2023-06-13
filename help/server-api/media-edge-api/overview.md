---
keywords: Experience Platform;bannière multimédia;rubriques les plus consultées;période
solution: Experience Platform
title: API Media Edge
description: Présentation des API Media Edge.
source-git-commit: 9d535c8d6524d61612581fbf82986bc5c5cf52de
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 4%

---


# Présentation de l’API Media Edge

Les API Media Edge sont créées sur Adobe Experience Platform (AEP) pour fournir des données de suivi d’événement multimédia dans le cadre de la fonction [Schémas XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Pour les clients Media Analytics, les fonctionnalités suivantes sont alors disponibles :

* Avec [Customer Journey Analytics (CJA)](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr), les clients peuvent obtenir des détails détaillés en temps quasi réel sur la durée, les démarrages et les arrêts pour évaluer et combiner les mesures multimédia. Toutes les mesures de création de rapports sont disponibles dans CJA pour les clients effectuant la migration depuis Adobe Analytics.

* Avec [Adobe Real-time Customer Data Platform (CDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=fr), les clients peuvent enrichir leurs profils en temps réel avec des données de consommation multimédia.

* Avec [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en), les clients peuvent optimiser les campagnes omnicanal et automatiser les parcours à l’aide de signaux de consommation multimédia.


## Optimisation des flux de données de suivi multimédia

Les [API Media Collection](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) et les API Media Edge fournissent des données de suivi multimédia en tant que services RESTful. Toutefois, l’utilisation du service Media Edge présente les avantages suivants :

* Il s’agit du moyen le plus simple d’incorporer des schémas XDM dans votre flux de données.

* Les appels sont dirigés d’un lecteur multimédia directement vers [Réseau Experience Edge Platform](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Il effectue le suivi le plus efficace des événements multimédia.

Le tableau suivant présente un service d’API d’Adobe possible pour divers cas d’analyse des médias :

| Cas d’utilisation | Service API |
| -------- | ------ |
| Solution AEP (CJA, RTDCP, AJO, etc.) | Media Edge |
| CDP + CJA | Media Edge |
| Solution Adobe Analytics + AEP | Media Edge |
| Adobe Analytics uniquement (suivi déjà effectué) | Collection Médias |

>[!NOTE]
>
> Le service d’API Media Collection pour Analytics reçoit toujours des données XDM, mais n’est pas optimisé dans la mesure où le service Media Edge l’est. Selon les données envoyées à partir du lecteur Media, certaines données Analytics uniquement peuvent également être acheminées via le service API Media Edge.

Le graphique suivant montre les flux de données des deux services API :


![Flux de données Media Analytics](../assets/edge-api-dataflow.png)


Pour plus d’informations sur l’utilisation des API Media Edge, consultez la documentation Prise en main .

Pour plus d’informations sur l’utilisation de Platform Edge, voir [Installation de Media Analytics avec Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).





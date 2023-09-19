---
solution: Experience Platform
title: API Media Edge
description: Vue d’ensemble des API Media Edge
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 96%

---


# Vue d’ensemble de l’API Media Edge

Les API Media Edge reposent sur Adobe Experience Platform et permettent de fournir des données de suivi d’événement multimédia dans le cadre des [Schémas XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Pour les clientes et clients Media Analytics, les fonctionnalités suivantes sont alors disponibles :

* Avec [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr), les clientes et clients peuvent obtenir des détails précis en temps quasi réel sur la durée, les démarrages et les arrêts afin d’évaluer et de combiner les mesures multimédia. Toutes les mesures de création de rapports sont disponibles dans Adobe Customer Journey Analytics pour les clientes et clients effectuant la migration à partir d’Adobe Analytics.

* Avec [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=fr), les clientse et clients peuvent enrichir leurs profils en temps réel à l’aide de données de consommation multimédia.

* Avec [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=fr), les clientes et clients peuvent optimiser les campagnes omnicanales et automatiser les parcours à l’aide de signaux de consommation multimédia.


## Optimiser les flux de données de suivi multimédia

Les [API Media Collection](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=fr&amp;media-tracking-data-flows=) et les API Media Edge fournissent des données de suivi multimédia en tant que services RESTful. L’utilisation du service Media Edge présente toutefois les avantages suivants :

* Il s’agit du moyen le plus simple d’incorporer des schémas XDM dans votre flux de données.

* Les appels sont dirigés d’un lecteur multimédia directement vers [Réseau Edge Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=fr).

* Il effectue un suivi efficace des événements multimédia avec un minimum d’appels inter-serveurs.

Le tableau suivant présente un service possible d’API Adobe pour divers cas de Media Analytics :

| Cas d’utilisation | Service d’API |
| -------- | ----------- |
| Solution Adobe Experience Platform | Media Edge |
| Real-time CDP + Customer Journey Analytics | Media Edge |
| Adobe Analytics + solution Adobe Experience Platform | Media Edge |
| Adobe Analytics uniquement (déjà suivi) | Media Collection |

>[!NOTE]
>
> Le service d’API Media Collection pour Analytics reçoit toujours des données XDM mais n’est pas optimisé dans la mesure où le service Media Edge l’est. Selon les données envoyées à partir du lecteur multimédia, certaines données Analytics uniquement peuvent également être acheminées via le service d’API Media Edge.

Le graphique suivant montre les flux de données des deux services d’API :

![Flux de données Media Analytics](../assets/edge-api-dataflow.png)

## Étapes suivantes

* Pour plus d’informations sur l’utilisation des API Media Edge, veuillez consulter la [documentation de prise en main](getting-started.md).

* Pour plus d’informations sur l’utilisation de Platform Edge, voir [Installation de Media Analytics avec Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=fr).





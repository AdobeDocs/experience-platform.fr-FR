---
title: Gestion de la duplication des événements dans Experience Platform
description: Découvrez comment Adobe Experience Platform gère la duplication des événements
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Gestion de la duplication des événements dans Adobe Experience Platform

Adobe Experience Platform est un système hautement distribué conçu pour optimiser la fiabilité tout en s’adaptant à des volumes de données toujours plus importants.

Pour la collecte de données en temps réel, les [événements d’expérience](/help/xdm/classes/experienceevent.md) sont collectés via l’Edge Network, à partir de sources côté client, telles que Web SDK ou [Mobile SDK](https://developer.adobe.com/client-sdks/home/), et transmis aux couches de traitement et de stockage Experience Platform. Ces calques composent des solutions telles qu’Experience Platform, [Real-Time CDP](/help/rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr) et [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr).

Pour minimiser la perte d’événements d’expérience, les SDK côté client et le service de diffusion interne d’Experience Platform attendent une confirmation qu’un événement a bien été collecté.

Si cette confirmation n’est pas reçue, les SDK côté client ou le service de diffusion interne d’Experience Platform déclenchent une nouvelle tentative et l’événement d’expérience est envoyé à nouveau.

Il s’agit d’une bonne pratique pour gérer les échecs transitoires. L’effet secondaire est la possibilité d’introduire des événements en double.

Pour mieux comprendre les bonnes pratiques de gestion des pannes transitoires, consultez cet article sur la [gestion des pannes transitoires](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Scénarios de duplication des événements {#scenarios}

La duplication d’événements peut se produire dans divers scénarios, notamment :

* Problèmes liés au réseau entre les SDK côté client et le [!DNL Edge Network]. Ces problèmes peuvent provenir de défaillances du fournisseur d’accès Internet, d’une perte de signal mobile ou d’autres défaillances du réseau, puisque la connectivité entre le client et Edge Network est assurée via l’Internet public.
* Mise à l’échelle automatique des événements Experience Platform internes. Parfois, les données peuvent être rééquilibrées en raison de la volatilité de l’infrastructure cloud.

La couche de collecte de données Adobe Experience Platform est conçue pour prendre en charge le traitement « au moins une fois ». Par conséquent, la duplication des événements peut se produire dans des situations limitées et rares.

Pour en savoir plus sur le traitement « au moins une fois », consultez cet article sur les [garanties de diffusion des messages](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Options de déduplication des événements {#deduplication}

Pour les scénarios métier sensibles aux événements en double, Experience Platform utilise plusieurs méthodes de déduplication des événements dans ses systèmes de stockage en aval, telles que celles décrites ci-dessous.

* La banque de profils de Real-Time CDP supprime les événements si un événement de même `_id` existe déjà dans le [!DNL Profile store]. Pour plus d’informations, consultez la documentation sur la [classe XDM ExperienceEvent](/help/xdm/classes/experienceevent.md).
* Customer Journey Analytics permet aux utilisateurs de configurer une mesure pour ne compter que les valeurs de manière non répétitive. Pour découvrir comment procéder, consultez la documentation sur les paramètres des composants de déduplication des mesures [metric](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=fr).
* Experience Platform Query Service prend en charge la déduplication des données lorsqu’il est nécessaire de supprimer une ligne entière d’un calcul ou d’ignorer un ensemble spécifique de champs, car seule une partie des données de la ligne est une information dupliquée. Pour plus d’informations, consultez la documentation sur [la déduplication des données dans Query Service](/help/query-service/key-concepts/deduplication.md).

>[!NOTE]
>
>Si vous rencontrez des problèmes de duplication d’événements en dehors des cas d’utilisation présentés ci-dessus, contactez votre représentant Adobe et fournissez des informations détaillées sur votre cas d’utilisation.

---
title: Gestion de la duplication des événements dans Experience Platform
description: Découvrez comment Adobe Experience Platform gère la duplication des événements
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
TQID: https://experienceleague.adobe.com/P7G0XROFmmnm0Z9VEAxt-lSw6UhenD4g7SBeV-5T7FY
product_v2: id: cb954087-f4fc-4456-afb9-e939cabcdc79id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: e98b7246-966c-4318-9e95-cad2f7a17dc7id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2: id: ba929a52-9339-4154-9487-317dc875a3c7id: c132d929-fa62-4271-803e-b823be07b914id: df64005d-8f9a-422e-ba4d-c6f6dc3454b4id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: a230274e-7e6e-49eb-b817-514495a710acid: abc02dd6-664f-446a-9aaa-675bc0f2fe4aid: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 506
ht-degree: 7%

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

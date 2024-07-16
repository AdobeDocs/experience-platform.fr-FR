---
title: Gestion de la duplication des événements dans Experience Platform
description: Découvrez comment Adobe Experience Platform gère la duplication des événements
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Gestion de la duplication des événements dans Adobe Experience Platform

Adobe Experience Platform est un système hautement distribué, conçu pour optimiser la fiabilité tout en s’adaptant à un volume de données toujours plus important.

Pour la collecte de données en temps réel, les [événements d’expérience](../xdm/classes/experienceevent.md) sont collectés via l’ [Edge Network](../web-sdk/home.md#edge-network), à partir de sources côté client, telles que [SDK Web](../web-sdk/home.md) ou [SDK mobile](https://developer.adobe.com/client-sdks/home/), et distribués aux couches de traitement et de stockage Experience Platform. Ces couches composent des solutions telles que Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr) et [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr).

Pour minimiser la perte d’événements d’expérience, les SDK côté client et le service de diffusion Experience Platform interne attendent une confirmation qu’un événement a bien été collecté.

Si cette confirmation n’est pas reçue, les SDK côté client ou le service de diffusion interne de Platform déclenchent une nouvelle tentative et l’événement d’expérience est envoyé à nouveau.

Il s’agit d’une bonne pratique pour gérer les échecs transitoires. L’effet secondaire est la possibilité d’introduire des événements en double.

Pour mieux comprendre les bonnes pratiques de gestion des échecs transitoires, reportez-vous à cet article sur la [gestion des erreurs transitoires](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Scénarios de duplication d’événements {#scenarios}

La duplication d’événements peut se produire dans divers scénarios, tels que :

* Problèmes liés au réseau entre les SDK côté client et [!DNL Edge Network]. Ces problèmes peuvent provenir de défaillances du fournisseur d’accès Internet, de la perte de signal mobile ou d’autres défaillances du réseau, puisque la connectivité entre le client et l’Edge Network est réalisée par le biais de l’Internet public.
* Événements de mise à l’échelle automatique de l’Experience Platform interne. Il arrive que les données soient rééquilibrées en raison de la volatilité de l’infrastructure cloud.

La couche de collecte de données Adobe Experience Platform est conçue pour prendre en charge le traitement &quot;au moins une fois&quot;. Par conséquent, la duplication d’événements peut se produire dans de rares cas et dans de rares cas.

Pour en savoir plus sur le traitement &quot;au moins une fois&quot;, consultez cet article sur les [garanties de diffusion des messages](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Options de déduplication des événements {#deduplication}

Pour les scénarios métier sensibles aux événements en double, Experience Platform utilise plusieurs méthodes de déduplication des événements dans ses systèmes de stockage en aval, comme ceux décrits ci-dessous.

* La banque de profils Real-Time CDP supprime les événements si un événement avec le même `_id` existe déjà dans le [!DNL Profile store]. Pour plus d’informations, consultez la documentation sur [XDM ExperienceEvent class](../xdm/classes/experienceevent.md) .
* Customer Journey Analytics permet aux utilisateurs de configurer une mesure afin de ne comptabiliser les valeurs que de manière non répétitive. Pour savoir comment le faire, consultez la documentation sur les [paramètres des composants de déduplication des mesures](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=fr).
* Experience Platform Query Service prend en charge le dédoublonnage des données lorsqu’il est nécessaire de supprimer une ligne entière d’un calcul ou d’ignorer un ensemble spécifique de champs, car seule une partie des données de la ligne est des informations en double. Pour plus d’informations, consultez la documentation relative à la [déduplication des données dans Query Service](../query-service/key-concepts/deduplication.md) .

>[!NOTE]
>
>Si vous rencontrez des problèmes de duplication d’événements en dehors des cas d’utilisation présentés ci-dessus, contactez votre représentant d’Adobe et fournissez des informations détaillées sur votre cas d’utilisation.

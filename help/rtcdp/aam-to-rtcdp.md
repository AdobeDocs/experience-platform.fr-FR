---
title: Évolution d’Audience Manager à Real-Time CDP
description: Ayez conscience des points à prendre en compte avant de planifier la migration d’Audience Manager vers Adobe Real-Time CDP.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 86%

---

# Évolution d’Audience Manager à Real-Time CDP

Tandis que votre organisation passe à Adobe Real-Time CDP, voici quelques points à prendre en compte pour préparer vos données et prendre conscience des différences majeures entre les deux technologies. Cet article s’adresse à une audience de professionnels et professionnelles.

![Diagramme d’évolution d’Audience Manager à Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Prenez en compte l’architecture des données dans Audience Manager.

À mesure que vous prenez en compte l’évolution d’Audience Manager vers Real-Time CDP, le moment est venu d’analyser vos [segments Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=fr) et de déterminer les [signaux](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=fr), [caractéristiques](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=fr) et [règles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=fr#segment-builder-section) qui constituent ces segments.

En outre, pensez aux sources de données que vous utilisez actuellement dans Audience Manager.

Adobe vous recommande de classer vos segments comme suit :

* Les segments qui peuvent être envoyés à l’Experience Platform par l’intermédiaire du [[!UICONTROL Connecteur Source d’Audience Manager]](/help/sources/connectors/adobe-applications/audience-manager.md), car ils ne comportent aucune dépendance de données, aucun problème de destination ou d’activation, et leurs règles de segmentation peuvent être créées par l’intermédiaire du [créateur de segments](/help/segmentation/ui/segment-builder.md) de Real-Time CDP.
* Segments qui comportent des règles qui peuvent être prises en charge, mais qui peuvent contenir des données qui ne seront pas disponibles dans Real-Time CDP.
* Segments qui ne peuvent pas être créés dans Real-Time CDP et qui ne disposent d’aucune fonctionnalité.

>[!TIP]
>
>Adobe Real-Time CDP offre [trois types d’évaluation des segments](/help/segmentation/home.md#evaluate-segments) : [!UICONTROL lot], [!UICONTROL streaming], et [!UICONTROL Edge]. Les clientes et clients qui utilisent des segments en temps réel dans Audience Manager peuvent être restreint(e)s par la limitation actuelle de 500 segments de streaming dans Real-Time CDP. En savoir plus sur les [mécanismes de sécurisation de la segmentation](/help/profile/guardrails.md).

## 2. Quels segments sont essentiels à l’envoi par l’intermédiaire du [!UICONTROL connecteur source d’Audience Manager] ?

En fonction de leurs critères d’évaluation, les segments qui n’ont aucune dépendance de données, aucune difficulté de destination ou d’activation et dont les règles de segmentation peuvent être créées par le biais de la collecte de données Real-Time CDP comme [SDK Web Adobe Experience Platform](/help/web-sdk/faq.md) à une date ultérieure doivent être envoyés via  le connecteur source Audience Manager.

## 3. Utiliserez-vous la destination [!UICONTROL Audiences Experience Cloud] pour rétablir les données dans Audience Manager ?

Les segments dont les règles qui peuvent être prises en charge dans Real-Time CDP mais qui ont des dépendances d’activation avec Audience Manager peuvent être envoyés à Audience Manager via la carte de destination [Audiences Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md).

## 4. Quelles destinations sont actuellement en place dans Audience Manager pour commencer à passer à Real-Time CDP ?

Adobe recommande vivement que les segments activés dans Audience Manager pour les [destinations basées sur les personnes](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr) soient transmises à Real-Time CDP via le [!UICONTROL connecteur source d’Audience Manager], pour procéder ensuite à l’activation via Real-Time CDP.

Toutes les destinations basées sur les personnes disponibles dans Audience Manager ([Facebook](/help/destinations/catalog/social/facebook.md), le [[!UICONTROL ciblage par liste de clients de Google]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md)) sont également disponibles dans Real-Time CDP.

D’autres partenaires de stratégie des médias et des données propriétaires, tels que [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md), et [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) sont disponibles.

Real-Time CDP prend actuellement en charge plus de 60 destinations en mode natif dans le [catalogue](/help/destinations/catalog/overview.md), dont plus de 20 sont des destinations publicitaires ou de réseaux sociaux prenant en charge la correspondance d’audience propriétaire.

## Étapes suivantes

Après avoir lu cette page, vous avez désormais un premier ensemble de points à prendre en compte lorsque vous commencerez à passer d’Audience Manager à Real-Time CDP.

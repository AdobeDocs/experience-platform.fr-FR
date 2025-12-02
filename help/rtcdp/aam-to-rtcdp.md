---
title: Évolution d’Audience Manager à Real-Time CDP
description: Tenez compte des points à prendre en compte avant de planifier la migration d’Audience Manager vers Adobe Real-Time CDP.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 67%

---

# Évolution d’Audience Manager à Real-Time CDP

Tandis que votre organisation passe à Adobe Real-Time CDP, voici quelques points à prendre en compte pour préparer vos données et prendre conscience des différences majeures entre les deux technologies. Cet article s’adresse à une audience de professionnels et professionnelles.

![Diagramme d’évolution d’Audience Manager à Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## &#x200B;1. Prenez en compte l’architecture des données dans Audience Manager.

À mesure que vous prenez en compte l’évolution d’Audience Manager vers Real-Time CDP, le moment est venu d’analyser vos [segments Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=fr) et de déterminer les [signaux](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=fr), [caractéristiques](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=fr) et [règles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=fr#segment-builder-section) qui constituent ces segments.

En outre, pensez aux sources de données que vous utilisez actuellement dans Audience Manager.

Adobe vous recommande de classer vos segments comme suit :

* Segments qui peuvent être envoyés à Experience Platform via le [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md), car ils n’ont aucune dépendance de données, aucun défi de destination ou d’activation, et dont les règles de segmentation peuvent être créées via le Real-Time CDP [créateur de segments](/help/segmentation/ui/segment-builder.md) ultérieurement.
* Segments qui comportent des règles qui peuvent être prises en charge, mais qui peuvent contenir des données qui ne seront pas disponibles dans Real-Time CDP.
* Segments qui ne peuvent pas être créés dans Real-Time CDP et dont la fonctionnalité est manquante.

>[!TIP]
>
>Adobe Real-Time CDP propose [trois types d’évaluation de segments](/help/segmentation/home.md#evaluate-segments) : [!UICONTROL Batch], [!UICONTROL Streaming] et [!UICONTROL Edge]. Les clientes et clients qui utilisent des segments en temps réel dans Audience Manager peuvent être restreint(e)s par la limitation actuelle de 500 segments de streaming dans Real-Time CDP. En savoir plus sur les [mécanismes de sécurisation de la segmentation](/help/profile/guardrails.md).

## &#x200B;2. Quels segments sont essentiels à l’envoi par l’intermédiaire de [!UICONTROL Audience Manager Source Connector] ?

En fonction de leurs critères d’évaluation, les segments qui n’ont aucune dépendance de données, aucune difficulté de destination ou d’activation et dont les règles de segmentation peuvent être créées par le biais de la collecte de données Real-Time CDP comme [SDK Web Adobe Experience Platform](/help/collection/js/faq.md) à une date ultérieure doivent être envoyés via  le connecteur source Audience Manager.

## &#x200B;3. Utiliserez-vous la destination [!UICONTROL Experience Cloud Audiences] pour rétablir les données dans Audience Manager ?

Les segments dont les règles qui peuvent être prises en charge dans Real-Time CDP mais qui ont des dépendances d’activation avec Audience Manager peuvent être envoyés à Audience Manager via la carte de destination [Audiences Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md).

## &#x200B;4. Quelles destinations sont actuellement en place dans Audience Manager pour commencer à passer à Real-Time CDP ?

Adobe recommande vivement que les segments activés dans Audience Manager vers des [destinations basées sur les personnes](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr) soient transmises à Real-Time CDP via l’[!UICONTROL Audience Manager Source Connector], pour être ensuite activés via Real-Time CDP.

Toutes les destinations basées sur les personnes disponibles dans Audience Manager ([Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md)) sont également disponibles dans Real-Time CDP.

D’autres partenaires de stratégie des médias et des données propriétaires tels que [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) et [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) sont disponibles.

Real-Time CDP prend actuellement en charge plus de 60 destinations en mode natif dans le [catalogue](/help/destinations/catalog/overview.md), dont plus de 20 sont des destinations publicitaires ou de réseaux sociaux prenant en charge la correspondance d’audience propriétaire.

## Étapes suivantes

Après avoir lu cette page, vous avez désormais un premier ensemble de points à prendre en compte lorsque vous commencerez à passer d’Audience Manager à Real-Time CDP.

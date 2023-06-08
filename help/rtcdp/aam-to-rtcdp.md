---
title: Evolution de l’Audience Manager à Real-Time CDP
description: Ayez conscience des points à prendre en compte avant de planifier la migration d’Audience Manager vers Real-Time CDP.
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Evolution de l’Audience Manager à Real-Time CDP

À mesure que votre entreprise évolue pour utiliser Adobe Real-Time CDP, découvrez ces points à prendre en compte pour préparer vos données et prendre conscience des différences critiques entre les deux technologies. Cet article s&#39;adresse à un public de praticiens.

![Audience Manager au diagramme d’évolution Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Considération de l’architecture des données dans Audience Manager

À mesure que vous considérez l’évolution de l’Audience Manager vers Real-Time CDP, le moment est venu d’analyser votre [Segments d’Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en) et déterminer ce que la variable [signals](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en), [traits](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en), et [rules](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section) qui constituent ces segments.

En outre, pensez aux sources de données que vous utilisez actuellement dans Audience Manager.

Adobe vous recommande de classer vos segments comme suit :

* Segments qui peuvent être envoyés à l’Experience Platform via le [[!UICONTROL Connecteur source d’Audience Manager]](/help/sources/connectors/adobe-applications/audience-manager.md), car ils n’ont aucune dépendance de données, aucun problème de destination ou d’activation, et leurs règles de segmentation peuvent être créées via la plateforme de données clients en temps réel. [créateur de segments](/help/segmentation/ui/segment-builder.md) plus tard.
* Les segments qui comportent des règles qui peuvent être prises en charge, mais qui peuvent contenir des données qui ne seront pas disponibles dans Real-Time CDP.
* Les segments qui ne peuvent pas être créés dans la plateforme des données clients en temps réel et qui ne disposent pas de fonctionnalités.

>[!TIP]
>
>Offres Adobe Real-Time CDP [trois types d’évaluation des segments](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Lot], [!UICONTROL Diffusion en continu], et [!UICONTROL Edge]. Les clients qui utilisent des segments en temps réel en Audience Manager peuvent être restreints par la limitation actuelle de 500 segments en continu dans Real-Time CDP. En savoir plus sur [barrières de sécurité de segmentation](/help/profile/guardrails.md).

## 2. Quels segments sont essentiels à l’envoi par l’intermédiaire de [!UICONTROL Connecteur source d’Audience Manager]?

En fonction de leurs critères d’évaluation, des segments qui n’ont aucune dépendance de données, aucun défi de destination ou d’activation et leurs règles de segmentation peuvent être créées par le biais de la collecte de données Real-Time CDP comme [SDK Web Adobe Experience Platform](/help/edge/web-sdk-faq.md) à une date ultérieure doit être envoyée via Audience Manager Source Connector.

## 3. Utilisez-vous la variable [!UICONTROL Audiences Experience Cloud] destination pour rétablir les données dans l’Audience Manager ?

Les segments qui comportent des règles qui peuvent être prises en charge dans Real-Time CDP mais qui ont des dépendances d’activation à l’Audience Manager peuvent être envoyés à l’Audience Manager via le [Audiences Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) carte de destination.

## 4. Quelles destinations avez-vous en Audience Manager aujourd’hui pour commencer à vous déplacer vers Real-Time CDP ?

Adobe recommande vivement que les segments activés dans l’Audience Manager soient [destinations basées sur les personnes](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en) sont transmises à Real-Time CDP via la fonction [!UICONTROL Connecteur source d’Audience Manager], pour ensuite l’activer via Real-Time CDP.

Toutes les destinations basées sur les personnes disponibles en Audience Manager - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Correspondance client Google]](/help/destinations/catalog/advertising/google-customer-match.md), [linkedIn](/help/destinations/catalog/social/linkedin.md) - sont également disponibles dans Real-Time CDP.

Autres partenaires de stratégie des médias et des données propriétaires, tels que [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Publicités Amazon](/help/destinations/catalog/advertising/amazon-ads.md), et [[!UICONTROL Le bureau de commerce]](/help/destinations/catalog/advertising/tradedesk.md) sont disponibles.

Real-Time CDP prend actuellement en charge plus de 60 destinations en mode natif dans le [catalogue](/help/destinations/catalog/overview.md), dont plus de 20 sont des destinations publicitaires ou sociales qui prennent en charge la correspondance d’audiences propriétaires.

## Étapes suivantes

Après avoir lu cette page, vous devez maintenant tenir compte d’un premier ensemble de points à prendre en compte lorsque vous commencez à passer de l’Audience Manager à Real-Time CDP.

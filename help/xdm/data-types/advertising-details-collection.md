---
title: Type De Données De Collecte Des Détails Advertising
description: Découvrez le type de données du modèle de données d’expérience (XDM) de la collecte de détails Advertising.
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
TQID: https://experienceleague.adobe.com/47Vp-vkRvsQVbD9E2-0vZhNgGt8D1dEI-wvIpsDQPnQ
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 499
ht-degree: 5%

---

# [!UICONTROL Détails Advertising &#x200B;] type de données de collection

[!UICONTROL Détails Advertising &#x200B;] la collecte est un type de données standard du modèle de données d’expérience (XDM) qui capture les attributs clés liés aux publicités. Elle contient des informations telles que l’ID de l’annonce, les ID de l’annonceur et de la campagne, la longueur, la position dans une séquence, les détails sur le lecteur qui effectue le rendu de l’annonce, etc. Vous pouvez utiliser ce type de données pour suivre et analyser divers aspects des performances et de l’engagement des publicités, et fournir des informations sur la manière dont les audiences interagissent avec différentes publicités et y répondent.

+++Sélectionnez cette option pour afficher un diagramme du type de données Collecte des détails Advertising .
![Diagramme du type de données de collecte de détails Advertising.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaCollection`, à savoir les champs que votre implémentation envoie au serveur principal des médias en flux continu. Adobe traite ces données et génère les champs de `mediaReporting` correspondants, qui sont ingérés dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

Chaque nom d’affichage contient un lien vers des informations supplémentaires sur sa variable d’implémentation. Les pages liées contiennent des détails sur les données collectées par Adobe, les valeurs d’implémentation, les paramètres réseau et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|---|---|---|---|---|
| [[!UICONTROL Publicitaire]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/advertiser) | `advertiser` | string | Non | Société ou marque dont le produit apparaît dans la publicité. |
| [[!UICONTROL ID de publicité]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/ad-id) | `name` | string | Oui | Identifiant de l’annonce publicitaire. Toute combinaison de nombres entiers et/ou de lettres. |
| [[!UICONTROL Campagne publicitaire]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/campaign-id) | `campaignID` | string | Non | Identifiant de la campagne publicitaire. |
| [[!UICONTROL ID de Creative publicitaire]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/creative-id) | `creativeID` | string | Non | Identifiant du contenu publicitaire. |
| [[!UICONTROL URL Ad Creative]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/creative-url) | `creativeURL` | string | Non | URL de la création publicitaire. |
| [[!UICONTROL Position de l’annonce publicitaire dans la capsule (début de l’annonce publicitaire)]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/ad-in-pod-position) | `podPosition` | Entier | Oui | Index de la publicité à l’intérieur du début de la coupure publicitaire parent. Par exemple, la première publicité a un index de 0 et la seconde un index de 1. |
| [[!UICONTROL Durée Ou Longueur De L’Annonce Publicitaire]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/ad-length) | `length` | Entier | Oui | Durée de la publicité en secondes. |
| [[!UICONTROL Nom de la publicité]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/ad-name) | `friendlyName` | string | Oui | Nom lisible par l’utilisateur de la publicité. |
| [[!UICONTROL ID d’emplacement publicitaire]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/placement-id) | `placementID` | string | Non | Identifiant d’emplacement de la publicité. |
| [[!UICONTROL Nom du lecteur de publicités]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/ad-player-name) | `playerName` | string | Oui | Nom du lecteur responsable du rendu de la publicité. |
| [[!UICONTROL ID du site publicitaire]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ads/site-id) | `siteID` | string | Non | Identifiant du site publicitaire. |

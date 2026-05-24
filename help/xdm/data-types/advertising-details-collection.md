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
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 413
ht-degree: 6%

---

# Type de données de la collecte de [!UICONTROL Advertising Details]

La collecte de [!UICONTROL Advertising Details] est un type de données standard du modèle de données d’expérience (XDM) qui capture les attributs clés liés aux publicités. Elle contient des informations telles que l’ID de l’annonce, les ID de l’annonceur et de la campagne, la longueur, la position dans une séquence, les détails sur le lecteur qui effectue le rendu de l’annonce, etc. Vous pouvez utiliser ce type de données pour suivre et analyser divers aspects des performances et de l’engagement des publicités, et fournir des informations sur la manière dont les audiences interagissent avec différentes publicités et y répondent. Ces informations sont utilisées pour effectuer le suivi de vos données de diffusion en continu.

+++Sélectionnez cette option pour afficher un diagramme du type de données Collecte des détails Advertising .
![Diagramme du type de données de collecte de détails Advertising.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur la vidéo et les données collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, les rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Ad Advertiser]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | string | Non | Société ou marque dont le produit apparaît dans la publicité. |
| [[!UICONTROL Ad Campaign]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | string | Non | Identifiant de la campagne publicitaire. |
| [[!UICONTROL Ad Creative ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | string | Non | Identifiant du contenu publicitaire. |
| [[!UICONTROL Ad Creative URL]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | string | Non | URL de la création publicitaire. |
| [[!UICONTROL Ad In Pod Position (Ad Start)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | Entier | Oui | Index de la publicité à l’intérieur du début de la publicité parent. Par exemple, la première publicité a un index de 0 et la seconde un index de 1. |
| [[!UICONTROL Ad Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | Entier | Oui | Durée de la publicité vidéo en secondes. |
| [[!UICONTROL Ad Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | string | Oui | Nom lisible par l’utilisateur de la publicité. Dans les rapports, « Nom de la publicité » est la classification et « Nom de la publicité (variable) » est l’eVar. |
| [[!UICONTROL Ad Placement ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | string | Non | Identifiant d’emplacement de la publicité. |
| [[!UICONTROL Ad Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | string | Oui | Nom du lecteur responsable du rendu de la publicité. |
| [[!UICONTROL Ad Site ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | string | Non | Identifiant du site publicitaire. |

{style="table-layout:auto"}

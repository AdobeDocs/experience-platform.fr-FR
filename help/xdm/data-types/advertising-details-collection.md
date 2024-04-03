---
title: Type de données de collecte des détails publicitaires
description: Découvrez le type de données XDM (Advertising Details Collection Experience Data Model).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Détails de la publicité] Type de données de collecte

[!UICONTROL Détails de la publicité] Collection est un type de données XDM (Experience Data Model) standard qui capture les attributs clés liés aux publicités. Il contient des informations telles que l’identifiant de la publicité, les identifiants de l’annonceur et de la campagne, la durée, la position dans une séquence, des détails sur le lecteur qui effectue le rendu de la publicité, etc. Vous pouvez utiliser ce type de données pour effectuer le suivi et l’analyse de divers aspects des performances et de l’engagement des publicités, et fournir des informations sur la manière dont les audiences interagissent avec différentes publicités et y répondent. Ces informations sont utilisées pour effectuer le suivi de vos données en continu.

+++Sélectionnez cette option pour afficher un diagramme du type de données Advertising Details Collection.
![Diagramme du type de données Advertising Details Collection.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Publicitaire publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | Chaîne | Non | Entreprise ou marque dont le produit apparaît dans la publicité. |
| [[!UICONTROL Campagne publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | Chaîne | Non | Identifiant de la campagne publicitaire. |
| [[!UICONTROL Identifiant publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | Chaîne | Non | Identifiant de l’élément créatif publicitaire. |
| [[!UICONTROL URL de création publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | Chaîne | Non | URL de l’élément créatif publicitaire. |
| [[!UICONTROL Position de la publicité dans la capsule (démarrage de la publicité)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | Entier | Oui | Index de la publicité dans le début de la publicité parente, par exemple, la première publicité comporte l’index 0 et la deuxième publicité l’index 1. |
| [[!UICONTROL Durée Ou Durée De La Publicité]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | Entier | Oui | Durée de la publicité vidéo en secondes. |
| [[!UICONTROL Nom de la publicité]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | Chaîne | Oui | Nom lisible par l’utilisateur de la publicité. Dans la création de rapports, « Nom de la publicité » est la classification et « Nom de la publicité (variable) » la variable eVar. |
| [[!UICONTROL Identifiant de référencement de publicité]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | Chaîne | Non | Identifiant de référencement de la publicité. |
| [[!UICONTROL Nom du lecteur de publicités]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | Chaîne | Oui | Nom du lecteur responsable du rendu de la publicité. |
| [[!UICONTROL Identifiant du site publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | Chaîne | Non | Identifiant du site de la publicité. |

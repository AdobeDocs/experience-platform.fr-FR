---
title: Type de données de collecte de détails Advertising
description: Découvrez le type de données XDM (Modèle de données d’expérience de collecte de détails d’Advertising).
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 14%

---

# [!UICONTROL Advertising Details] Type de données de collection

[!UICONTROL Advertising Details] La collection est un type de données standard Experience Data Model (XDM) qui capture les attributs clés liés aux publicités. Il contient des informations telles que l’identifiant de la publicité, les identifiants de l’annonceur et de la campagne, la durée, la position dans une séquence, des détails sur le lecteur qui effectue le rendu de la publicité, etc. Vous pouvez utiliser ce type de données pour effectuer le suivi et l’analyse de divers aspects des performances et de l’engagement des publicités, et fournir des informations sur la manière dont les audiences interagissent avec différentes publicités et y répondent. Ces informations sont utilisées pour effectuer le suivi de vos données en continu.

+++Sélectionnez cette option pour afficher un diagramme du type de données Collection de détails Advertising.
![Schéma du type de données Collection de détails Advertising.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Annonceur d’annonce]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#advertiser) | `advertiser` | Chaîne | Non | Entreprise ou marque dont le produit apparaît dans la publicité. |
| [[!UICONTROL Campagne publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#campaign-id) | `campaignID` | Chaîne | Non | Identifiant de la campagne publicitaire. |
| [[!UICONTROL ID de création publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#creative-id) | `creativeID` | Chaîne | Non | ID de la création publicitaire. |
| [[!UICONTROL URL de création publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#creative-url) | `creativeURL` | Chaîne | Non | URL de la création publicitaire. |
| [[!UICONTROL Position de la publicité dans la capsule (démarrage de la publicité)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#ad-start) | `podPosition` | Entier | Oui | Index de la publicité dans le début de la publicité parente, par exemple, la première publicité comporte l’index 0 et la deuxième publicité l’index 1. |
| [[!UICONTROL Longueur Ou Durée De La Publicité]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#ad-length) | `length` | Entier | Oui | Durée de la publicité vidéo en secondes. |
| [[!UICONTROL Nom de la publicité]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#ad-name) | `friendlyName` | Chaîne | Oui | Nom lisible par l’utilisateur de la publicité. Dans les rapports, &quot;Nom de la publicité&quot; est la classification et &quot;Nom de la publicité (variable)&quot; est l’eVar. |
| [[!UICONTROL Identifiant de référencement de la publicité]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#placement-id) | `placementID` | Chaîne | Non | Identifiant de référencement de la publicité. |
| [[!UICONTROL Nom du lecteur de publicités]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#ad-player-name) | `playerName` | Chaîne | Oui | Nom du lecteur responsable du rendu de la publicité. |
| [[!UICONTROL Identifiant du site publicitaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html?lang=fr#site-id) | `siteID` | Chaîne | Non | Identifiant du site de la publicité. |

{style="table-layout:auto"}

---
title: Type de données de rapports détaillés sur Advertising
description: Découvrez le type de données du modèle de données d’expérience de création de rapports (XDM) d’Advertising Details.
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
TQID: https://experienceleague.adobe.com/wkThCeraKu7iBC4JR2d4PnxSq41BdCpnnUwTIeHnO6k
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 570
ht-degree: 5%

---

# [!UICONTROL Détails Advertising &#x200B;] Type de données de rapport

[!UICONTROL Détails Advertising &#x200B;] la création de rapports est un type de données standard du modèle de données d’expérience (XDM) qui capture les attributs clés liés aux publicités. Elle contient des informations telles que l’ID de l’annonce, les ID de l’annonceur et de la campagne, la longueur, la position dans une séquence, les détails sur le lecteur qui effectue le rendu de l’annonce, etc. Vous pouvez utiliser ce type de données pour suivre et analyser divers aspects des performances et de l’engagement des publicités, et fournir des informations sur la manière dont les audiences interagissent avec différentes publicités et y répondent.

+++Sélectionnez cette option pour afficher un diagramme du type de données Rapports détaillés Advertising .
![Diagramme du type de données Rapports détaillés Advertising.](../images/data-types/advertising-details-information.png)
+++

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaReporting` : champs calculés par le serveur principal des médias en flux continu à partir des données `mediaCollection` envoyées par votre implémentation. Il s’agit des champs qu’Adobe ingère dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

Chaque nom d’affichage contient un lien vers des informations supplémentaires sur sa dimension ou sa mesure de reporting. Les pages liées contiennent des détails sur la manière dont Adobe calcule et signale ces données, y compris les répartitions par système de rapports.

| Nom d’affichage | Propriété | Type de données | Description |
|---|---|---|---|
| [[!UICONTROL Nom de la publicité]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/ad-name) | `friendlyName` | string | Nom lisible par l’utilisateur de la publicité. |
| [[!UICONTROL ID de publicité]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/ad) | `name` | chaîne | Identifiant de l’annonce publicitaire. Toute combinaison de nombres entiers et/ou de lettres. |
| [[!UICONTROL Durée Ou Longueur De L’Annonce Publicitaire]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/ad-length) | `length` | integer | Durée de la publicité en secondes. |
| [[!UICONTROL Position de l’annonce publicitaire dans la capsule (début de l’annonce publicitaire)]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/ad-in-pod-position) | `podPosition` | integer | Index de la publicité à l’intérieur du début de la coupure publicitaire parent. Par exemple, la première publicité a un index de 0 et la seconde un index de 1. |
| [[!UICONTROL Nom du lecteur de publicités]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/ad-player-name) | `playerName` | chaîne | Nom du lecteur responsable du rendu de la publicité. |
| [[!UICONTROL Publicitaire]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/advertiser) | `advertiser` | chaîne | Société ou marque dont le produit apparaît dans la publicité. |
| [[!UICONTROL Campagne publicitaire]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/campaign-id) | `campaignID` | chaîne | Identifiant de la campagne publicitaire. |
| [[!UICONTROL ID de Creative publicitaire]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/creative-id) | `creativeID` | chaîne | Identifiant du contenu publicitaire. |
| [[!UICONTROL ID du site publicitaire]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/site-id) | `siteID` | chaîne | Identifiant du site publicitaire. |
| [[!UICONTROL URL Ad Creative]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/creative-url) | `creativeURL` | chaîne | URL de la création publicitaire. |
| [[!UICONTROL ID d’emplacement publicitaire]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/dimensions/placement-id) | `placementID` | chaîne | Identifiant d’emplacement de la publicité. |
| [[!UICONTROL Publicité terminée]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/metrics/ad-completes) | `isCompleted` | booléen | Indique si la publicité est terminée. |
| [[!UICONTROL Annonce lancée]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/metrics/ad-starts) | `isStarted` | boolean | Indique si la publicité a commencé. |
| [[!UICONTROL Temps de lecture de la publicité]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/reporting/metrics/ad-time-spent) | `timePlayed` | entier | Durée totale (en secondes) passée à regarder la publicité (c’est-à-dire le nombre de secondes lues). |

Voir [advertisingdetails.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) dans le référentiel XDM public pour la définition complète du schéma.

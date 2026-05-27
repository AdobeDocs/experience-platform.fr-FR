---
title: Type de données de rapports détaillés sur Advertising
description: Découvrez le type de données du modèle de données d’expérience de création de rapports (XDM) d’Advertising Details.
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
TQID: https://experienceleague.adobe.com/wkThCeraKu7iBC4JR2d4PnxSq41BdCpnnUwTIeHnO6k
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 302
ht-degree: 9%

---

# Type de données [!UICONTROL Advertising Details] Reporting

[!UICONTROL Advertising Details] Reporting est un type de données standard du modèle de données d’expérience (XDM) qui capture les attributs clés liés aux publicités. Elle contient des informations telles que l’ID de l’annonce, les ID de l’annonceur et de la campagne, la longueur, la position dans une séquence, les détails sur le lecteur qui effectue le rendu de l’annonce, etc. Vous pouvez utiliser ce type de données pour suivre et analyser divers aspects des performances et de l’engagement des publicités, et fournir des informations sur la manière dont les audiences interagissent avec différentes publicités et y répondent.

+++Sélectionnez cette option pour afficher un diagramme du type de données Rapports détaillés Advertising .
![Diagramme du type de données Rapports détaillés Advertising.](../images/data-types/advertising-details-information.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Ad Name] | `friendlyName` | chaîne | Nom lisible par l’utilisateur de la publicité. Dans les rapports, « Nom de la publicité » est la classification et « Nom de la publicité (variable) » est l’eVar. |
| [!UICONTROL Ad ID] | `name` | chaîne | Identifiant de l’annonce publicitaire. Toute combinaison de nombres entiers et/ou de lettres. |
| [!UICONTROL Ad Length Or Duration] | `length` | entier | Durée de la publicité vidéo en secondes. |
| [!UICONTROL Ad In Pod Position (Ad Start)] | `podPosition` | entier | Index de la publicité à l’intérieur du début de la publicité parent. Par exemple, la première publicité a un index de 0 et la seconde un index de 1. |
| [!UICONTROL Ad Player Name] | `playerName` | chaîne | Nom du lecteur responsable du rendu de la publicité. |
| [!UICONTROL Ad Advertiser] | `advertiser` | chaîne | Société ou marque dont le produit apparaît dans la publicité. |
| [!UICONTROL Ad Campaign] | `campaignID` | chaîne | Identifiant de la campagne publicitaire. |
| [!UICONTROL Ad Creative ID] | `creativeID` | chaîne | Identifiant du contenu publicitaire. |
| [!UICONTROL Ad Site ID] | `siteID` | chaîne | Identifiant du site publicitaire. |
| [!UICONTROL Ad Creative URL] | `creativeURL` | chaîne | URL de la création publicitaire. |
| [!UICONTROL Ad Placement ID] | `placementID` | chaîne | Identifiant d’emplacement de la publicité. |
| [!UICONTROL Ad Completed] | `isCompleted` | booléen | Indique si la publicité est terminée. |
| [!UICONTROL Ad Started] | `isStarted` | booléen | Indique si la publicité a commencé. |
| [!UICONTROL Ad Time Played] | `timePlayed` | entier | Durée totale (en secondes) passée à regarder la publicité (c’est-à-dire le nombre de secondes lues). |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)

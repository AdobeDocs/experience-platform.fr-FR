---
title: Type de données d’informations sur les détails de publicité
description: Découvrez le type de données XDM (Advertising Details Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 11%

---

# [!UICONTROL Informations sur les publicités] type de données

[!UICONTROL Informations sur les publicités] est un type de données XDM (Experience Data Model) standard qui capture les attributs clés liés aux publicités. Il contient des informations telles que l’identifiant de la publicité, les identifiants de l’annonceur et de la campagne, la durée, la position dans une séquence, des détails sur le lecteur qui effectue le rendu de la publicité, etc. Vous pouvez utiliser ce type de données pour effectuer le suivi et l’analyse de divers aspects des performances et de l’engagement des publicités, et fournir des informations sur la manière dont les audiences interagissent avec différentes publicités et y répondent.

+++Sélectionnez cette option pour afficher un diagramme du type de données Informations sur les détails de publicité.
![Schéma du type de données Informations sur les détails de publicité.](../images/data-types/advertising-details-information.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Nom de la publicité] | `friendlyName` | chaîne | **Obligatoire** Nom lisible par l’utilisateur de la publicité. Dans la création de rapports, « Nom de la publicité » est la classification et « Nom de la publicité (variable) » la variable eVar. |
| [!UICONTROL Identifiant de publicité] | `name` | chaîne | Identifiant de la publicité. Nombre entier et/ou combinaison de lettres. |
| [!UICONTROL Durée Ou Durée De La Publicité] | `length` | nombre entier | **Obligatoire** Durée de la publicité vidéo en secondes. |
| [!UICONTROL Position de la publicité dans la capsule (démarrage de la publicité)] | `podPosition` | nombre entier | **Obligatoire** Index de la publicité dans le début de la publicité parente, par exemple, la première publicité comporte l’index 0 et la deuxième publicité l’index 1. |
| [!UICONTROL Nom du lecteur de publicités] | `playerName` | chaîne | **Obligatoire** Nom du lecteur responsable du rendu de la publicité. |
| [!UICONTROL Publicitaire publicitaire] | `advertiser` | chaîne | Entreprise ou marque dont le produit apparaît dans la publicité. |
| [!UICONTROL Campagne publicitaire] | `campaignID` | chaîne | Identifiant de la campagne publicitaire. |
| [!UICONTROL Identifiant publicitaire] | `creativeID` | chaîne | Identifiant de l’élément créatif publicitaire. |
| [!UICONTROL Identifiant du site publicitaire] | `siteID` | chaîne | Identifiant du site de la publicité. |
| [!UICONTROL URL de création publicitaire] | `creativeURL` | chaîne | URL de l’élément créatif publicitaire. |
| [!UICONTROL Identifiant de référencement de publicité] | `placementID` | chaîne | Identifiant de référencement de la publicité. |
| [!UICONTROL Publicité terminée] | `isCompleted` | booléen | Permet d’effectuer le suivi de la fin de la publicité. |
| [!UICONTROL Publicité lancée] | `isStarted` | booléen | Permet d’effectuer le suivi du démarrage de la publicité. |
| [!UICONTROL Durée de lecture de la publicité] | `timePlayed` | nombre entier | Durée totale, en secondes, passée à regarder la publicité (c’est-à-dire le nombre de secondes lues). |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)

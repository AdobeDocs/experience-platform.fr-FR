---
title: Type de données de rapport Détails Advertising
description: Découvrez le type de données XDM (Advertising Details Reporting Experience Data Model).
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Détails Advertising] Type de données de rapport

[!UICONTROL Détails Advertising] La création de rapports est un type de données XDM (Experience Data Model) standard qui capture les attributs clés liés aux publicités. Il contient des informations telles que l’identifiant de la publicité, les identifiants de l’annonceur et de la campagne, la durée, la position dans une séquence, des détails sur le lecteur qui effectue le rendu de la publicité, etc. Vous pouvez utiliser ce type de données pour effectuer le suivi et l’analyse de divers aspects des performances et de l’engagement des publicités, et fournir des informations sur la manière dont les audiences interagissent avec différentes publicités et y répondent.

+++Sélectionnez cette option pour afficher un diagramme du type de données Rapports de détails Advertising.
![ Diagramme du type de données Rapports de détails Advertising.](../images/data-types/advertising-details-information.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Nom de la publicité] | `friendlyName` | Chaîne | Nom lisible par l’utilisateur de la publicité. Dans les rapports, &quot;Nom de la publicité&quot; est la classification et &quot;Nom de la publicité (variable)&quot; est l’eVar. |
| [!UICONTROL Identifiant de publicité] | `name` | Chaîne | Identifiant de la publicité. Tout nombre entier et/ou combinaison de lettres. |
| [!UICONTROL Longueur Ou Durée De La Publicité] | `length` | Entier | Durée de la publicité vidéo en secondes. |
| [!UICONTROL Position de la publicité dans la capsule (démarrage de la publicité)] | `podPosition` | Entier | Index de la publicité dans le début de la publicité parente, par exemple, la première publicité comporte l’index 0 et la deuxième publicité l’index 1. |
| [!UICONTROL Nom du lecteur de publicités] | `playerName` | Chaîne | Nom du lecteur responsable du rendu de la publicité. |
| [!UICONTROL Annonceur d’annonce] | `advertiser` | Chaîne | Entreprise ou marque dont le produit apparaît dans la publicité. |
| [!UICONTROL Campagne publicitaire] | `campaignID` | Chaîne | Identifiant de la campagne publicitaire. |
| [!UICONTROL Identifiant créatif publicitaire] | `creativeID` | Chaîne | ID de la création publicitaire. |
| [!UICONTROL Identifiant du site publicitaire] | `siteID` | Chaîne | Identifiant du site de la publicité. |
| [!UICONTROL URL de création publicitaire] | `creativeURL` | Chaîne | URL de la création publicitaire. |
| [!UICONTROL Identifiant de référencement de publicité] | `placementID` | Chaîne | Identifiant de référencement de la publicité. |
| [!UICONTROL Publicité terminée] | `isCompleted` | Booléen | Permet d’effectuer le suivi de la fin de la publicité. |
| [!UICONTROL Démarrage de la publicité] | `isStarted` | Booléen | Permet d’effectuer le suivi du démarrage de la publicité. |
| [!UICONTROL Durée de lecture de la publicité] | `timePlayed` | Entier | Durée totale, en secondes, passée à regarder la publicité (c’est-à-dire le nombre de secondes lues). |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)

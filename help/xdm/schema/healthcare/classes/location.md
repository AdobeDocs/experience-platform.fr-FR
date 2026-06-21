---
title: Classe d’emplacement
description: Découvrez la classe d’emplacement dans le modèle de données d’expérience (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 1d100981-49fb-4f02-b2c6-324f9c541f76
TQID: https://experienceleague.adobe.com/UoWyJvA7DYVPxUbw67ycqmaCyNZap99gqtNB-XyoL9w
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 150
ht-degree: 8%

---

# Classe [!UICONTROL Location]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Location] capture les informations de localisation d’événement en direct, telles qu’une salle de voyage ou une salle de sport.

![Structure de classe d’emplacement](../../../images/healthcare/classes/location.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Identifiant] | `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de déterminer l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il n’est pas nécessaire de lui fournir une valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’ID uniques si vous le souhaitez. |
| [!UICONTROL Identifiant d’emplacement] | `locationID` | [!UICONTROL Chaîne] | Identifiant unique de l’emplacement. |
| [!UICONTROL Nom du lieu] | `locationName` | [!UICONTROL Chaîne] | Nom de l’emplacement. |

La classe peut être étendue avec le groupe de champs [[!UICONTROL Location] ](../field-groups/location.md) pour décrire d’autres détails sur un emplacement.

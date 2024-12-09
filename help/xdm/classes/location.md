---
title: Classe d’emplacement
description: Découvrez la classe Location dans Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 8%

---

# Classe [!UICONTROL Location]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Location] capture les informations d’emplacement d’événement en direct, telles qu’une salle de voyage ou une salle de sport.

![Structure de classe d’emplacement](../images/classes/location.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Identifiant] | `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Comme ce champ est généré par le système, il n’est pas nécessaire de lui fournir une valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| [!UICONTROL Identifiant d’emplacement] | `locationID` | [!UICONTROL Chaîne] | Identifiant unique de l’emplacement. |
| [!UICONTROL Nom de l’emplacement] | `locationName` | [!UICONTROL Chaîne] | Nom de l’emplacement. |

La classe peut être étendue avec le groupe de champs [[!UICONTROL Location]](../field-groups/location/healthcare-location.md) pour décrire plus de détails sur un emplacement.

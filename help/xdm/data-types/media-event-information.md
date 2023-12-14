---
title: Type de données des informations sur l’événement multimédia
description: Découvrez le type de données XDM (Media Event Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 6%

---

# [!UICONTROL Informations sur les événements multimédia] type de données

[!UICONTROL Informations sur l’événement multimédia] est un type de données XDM (Experience Data Model) standard qui décrit les informations de détails du média relatives à l’événement d’expérience.

![Schéma du type de données Informations sur l’événement multimédia.](../images/data-types/media-event-information.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | Informations détaillées sur le média relatives à l’événement d’expérience. |
| `mediaEventTimestamp` | [!UICONTROL Chaîne] | Heure à laquelle un événement multimédia s’est produit. |
| `mediaEventType` | [!UICONTROL Chaîne] | Type d’événement multimédia. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)

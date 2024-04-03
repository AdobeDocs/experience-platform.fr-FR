---
title: Type de données des informations sur l’événement multimédia
description: Découvrez le type de données XDM (Media Event Information Experience Data Model).
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# [!UICONTROL Informations sur l’événement multimédia] type de données

[!UICONTROL Informations sur l’événement multimédia] est un type de données XDM (Experience Data Model) standard qui décrit les informations de détails du média relatives à l’événement d’expérience.

![Schéma du type de données Informations sur l’événement multimédia.](../images/data-types/media-event-information.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Informations détaillées sur le média relatives à l’événement d’expérience. Ce type de données est utilisé pour les deux types [collecte de données multimédia](./media-collection-details.md) et [création de rapports de données multimédia](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL Chaîne] | Heure à laquelle un événement multimédia s’est produit. |
| `mediaEventType` | [!UICONTROL Chaîne] | Type d’événement multimédia. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)

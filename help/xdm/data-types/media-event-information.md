---
title: Type de données d’informations sur l’événement multimédia
description: Découvrez le type de données Modèle de données d’expérience (XDM) d’informations sur les événements multimédia.
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
TQID: https://experienceleague.adobe.com/U8KhaDwXjJBeEbwY4POi490-73wyekcruu9jFi0rD1s
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 106
ht-degree: 3%

---

# Type de données [!UICONTROL Media Event Information]

[!UICONTROL Media Event Information] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les informations détaillées sur les médias liées à l’événement d’expérience.

![Diagramme du type de données Informations sur l’événement multimédia.](../images/data-types/media-event-information.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Informations détaillées sur le média relatives à l’événement d’expérience. Ce type de données est utilisé pour la [collecte de données multimédia](./media-collection-details.md) et la [création de rapports sur les données multimédia](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL String] | Heure à laquelle un événement multimédia s’est produit. |
| `mediaEventType` | [!UICONTROL String] | Type d’événement multimédia. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)

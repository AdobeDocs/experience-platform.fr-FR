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
source-git-commit: 74579d9ca311b241313a3d89b564f217cd3476c7
workflow-type: tm+mt
source-wordcount: 127
ht-degree: 10%

---

# [!UICONTROL Informations sur l’événement multimédia] type de données

[!UICONTROL  Informations sur l’événement multimédia ] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les détails de l’événement multimédia liés à l’événement d’expérience.

![Diagramme du type de données Informations sur l’événement multimédia.](../images/data-types/media-event-information.png)

| Propriété | Type de données | Description |
|---|---|---|
| `mediaCollection` | [!UICONTROL mediaDetails] | Détails du média liés à l’événement d’expérience. Ce type de données est utilisé pour la [collecte de données multimédia](./media-collection-details.md) et la [création de rapports sur les données multimédia](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL Chaîne] | Heure à laquelle un événement multimédia s’est produit, au format [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) (`yyyy-MM-dd'T'HH:mm:ssXXX`). |
| `mediaEventType` | [!UICONTROL Chaîne] | Type d’événement multimédia. Valeurs acceptées : `media.sessionStart`, `media.adBreakStart`, `media.adStart`, `media.adComplete`, `media.adBreakComplete`, `media.play`, `media.pauseStart`, `media.ping`, `media.bufferStart`, `media.bitrateChange`, `media.statesUpdate`, `media.error`, `media.chapterStart`, `media.chapterComplete`, `media.sessionComplete`, `media.sessionEnd`, `media.downloaded`,,. |

Voir [mediaevent.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json) dans le référentiel XDM public pour obtenir la définition complète du schéma.

---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;Schéma;XDM;champs;schémas;Schémas;contexte du lieu;placeContext;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données contextuelles de l’emplacement
description: En savoir plus sur le type de données XDM Placer le contexte .
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
TQID: https://experienceleague.adobe.com/fDSEqraUtNlCosMh-AOWlaRtU2Qt3kyvuJw3tAu4st4
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 74579d9ca311b241313a3d89b564f217cd3476c7
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 5%

---

# [!UICONTROL Contexte de l’emplacement] type de données

[!UICONTROL Contexte du lieu] est un type de données XDM standard qui décrit le lieu d’un événement observé, y compris des informations sur le point ciblé et les coordonnées géographiques.

![](../images/data-types/place-context.png){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaction du point ciblé]](./poi-interaction.md) | Décrit en détail l’interaction avec le point d’intérêt. |
| `activePOIs` | Tableau de [[!UICONTROL détails du point ciblé]](./poi-details.md) | Décrit les points d’intérêt qui ont provoqué l’événement. |
| `geo` | [[!UICONTROL Géo]](./geo.md) | Décrit l’emplacement géographique où l’expérience a été diffusée. |
| `localTime` | DateTime | Heure locale de l’événement, sous la forme d’un horodatage [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) sans décalage de fuseau horaire (`yyyy-MM-dd'T'HH:mm:ss`). Si un décalage de fuseau horaire est inclus, la valeur est convertie en UTC lors de l’ingestion et le décalage n’est pas conservé. Pour conserver le décalage, enregistrez-le à la place dans `localTimezoneOffset`. |
| `localTimezoneOffset` | Entier | Décalage du fuseau horaire local en minutes par rapport à UTC, en suivant la même convention que les [`Date.getTimezoneOffset()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getTimezoneOffset) de JavaScript. Les fuseaux horaires en avance sur l’UTC sont négatifs (par exemple, UTC+5:30 est `-330`). Cette valeur inclut le décalage DST actuel, le cas échéant. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)

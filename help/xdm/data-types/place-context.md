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
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 173
ht-degree: 5%

---

# Type de données [!UICONTROL Place context]

[!UICONTROL Place context] est un type de données XDM standard qui décrit le lieu d’un événement observé, y compris les informations sur le point ciblé et les coordonnées géographiques.

![](../images/data-types/place-context.png){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Décrit en détail l’interaction avec le point d’intérêt. |
| `activePOIs` | Tableau de [[!UICONTROL Point of interest details]](./poi-details.md) | Décrit les points d’intérêt qui ont provoqué l’événement. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Décrit l’emplacement géographique où l’expérience a été diffusée. |
| `localTime` | DateTime | Horodatage au format [RFC 3339](https://tools.ietf.org/html/rfc3339) indiquant l’heure locale à l’aide de avec un décalage de fuseau horaire indiqué. Le modèle de mise en forme est `yyyy-MM-dd'T'HH:mm:ssXXX` (par exemple, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Entier | Décalage horaire local actuel en minutes par rapport à UTC pour la valeur `localTime`. Cela doit inclure le décalage DST actuel, le cas échéant. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)

---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;contexte de lieu;placeContext;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données contextuelles de l’emplacement
description: En savoir plus sur le type de données XDM Placer le contexte .
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 4%

---

# [!UICONTROL Contexte de l’emplacement] type de données

[!UICONTROL Contexte du lieu] est un type de données XDM standard qui décrit le lieu d’un événement observé, y compris des informations sur le point ciblé et les coordonnées géographiques.

![](../images/data-types/place-context.png){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaction du point ciblé]](./poi-interaction.md) | Décrit en détail l’interaction avec le point d’intérêt. |
| `activePOIs` | Tableau de [[!UICONTROL détails du point ciblé]](./poi-details.md) | Décrit les points d’intérêt qui ont provoqué l’événement. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Décrit l’emplacement géographique où l’expérience a été diffusée. |
| `localTime` | DateTime | Horodatage au format [RFC 3339](https://tools.ietf.org/html/rfc3339) indiquant l’heure locale à l’aide de avec un décalage de fuseau horaire indiqué. Le modèle de mise en forme est `yyyy-MM-dd'T'HH:mm:ssXXX` (par exemple, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Nombre entier | Décalage horaire local actuel en minutes par rapport à UTC pour la valeur `localTime`. Cela doit inclure le décalage DST actuel, le cas échéant. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)

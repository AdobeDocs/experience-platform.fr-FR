---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;schéma;contexte de lieu;contexte de lieu;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données contextuelles de l’emplacement
description: Découvrez le type de données XDM de contexte d’emplacement.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 4%

---

# Type de données [!UICONTROL Placer le contexte]

[!UICONTROL Contexte d’emplacement] est un type de données XDM standard qui décrit l’emplacement d’un événement observé, y compris les informations de point ciblé et les coordonnées géographiques.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaction avec le point ciblé]](./poi-interaction.md) | Décrit les détails de l’interaction du point ciblé (POI). |
| `activePOIs` | Tableau des [[!UICONTROL détails du point ciblé]](./poi-details.md) | Décrit les points ciblés à l’origine de l’événement. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Décrit l’emplacement géographique où l’expérience a été diffusée. |
| `localTime` | DateTime | Horodatage au format [RFC 3339](https://tools.ietf.org/html/rfc3339), indiquant l’heure locale utilisée avec un décalage de fuseau horaire donné. Le modèle de formatage est `yyyy-MM-dd'T'HH:mm:ssXXX` (par exemple, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Nombre entier | Décalage de fuseau horaire local actuel en minutes par rapport à UTC pour la valeur `localTime`. Cela devrait inclure le décalage d’heure d’été actuel, le cas échéant. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)

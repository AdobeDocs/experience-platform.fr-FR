---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;schéma;contexte de lieu;contexte de lieu;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données contextuelles de l’emplacement
description: Ce document fournit un aperçu du type de données XDM de contexte d’emplacement.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 14%

---

# [!UICONTROL Contexte de l’emplacement] type de données

[!UICONTROL Contexte de l’emplacement] est un type de données XDM standard qui décrit l’emplacement d’un événement observé, y compris les informations de point ciblé et les coordonnées géographiques.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaction avec le point ciblé]](./poi-interaction.md) | Décrit les détails de l’interaction du point ciblé (POI). |
| `activePOIs` | Tableau de [[!UICONTROL Détails des points ciblés]](./poi-details.md) | Décrit les points ciblés à l’origine de l’événement. |
| `geo` | [[!UICONTROL Géo]](./geo.md) | Décrit l’emplacement géographique où l’expérience a été diffusée. |
| `localTime` | DateTime | Un horodatage dans [RFC 3339](https://tools.ietf.org/html/rfc3339) format , indiquant l’heure locale utilisée avec un décalage de fuseau horaire donné. Le modèle de formatage est le suivant : `yyyy-MM-dd'T'HH:mm:ssXXX` (par exemple, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Nombre entier | Le décalage de fuseau horaire local actuel en minutes par rapport au fuseau horaire UTC pour la variable `localTime` . Cela devrait inclure le décalage d’heure d’été actuel, le cas échéant. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)

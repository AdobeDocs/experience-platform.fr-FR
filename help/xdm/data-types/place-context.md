---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; contexte ; lieu ; contexte ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Placer le type de données contextuelles
topic: overview
description: Ce document présente un aperçu du type de données XDM de contexte d’emplacement.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 6%

---


# [!UICONTROL Placer le type de données ] contextuelles

[!UICONTROL Placer ] contextuel est un type de données XDM standard qui décrit l&#39;emplacement d&#39;un événement observé, y compris les informations de point d&#39;intérêt et les coordonnées géographiques.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaction avec le point d’intérêt]](./poi-interaction.md) | Décrit des détails sur l’interaction des points d’intérêt. |
| `activePOIs` | Tableau des [[!UICONTROL détails du point d&#39;intérêt]](./poi-details.md) | Décrit les points d’intérêt qui ont provoqué le événement. |
| `geo` | [[!UICONTROL Géo]](./geo.md) | Décrit l’emplacement géographique où l’expérience a été fournie. |
| `localTime` | DateTime | Horodatage au format [RFC 3339](https://tools.ietf.org/html/rfc3339), indiquant l’heure locale utilisée avec un décalage de fuseau horaire indiqué. Le modèle de formatage est `yyyy-MM-dd'T'HH:mm:ssXXX` (par exemple, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Entier | Décalage actuel du fuseau horaire local en minutes par rapport à l&#39;heure UTC pour la valeur `localTime`. Cela devrait inclure le décalage actuel de l’heure d’été, le cas échéant. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
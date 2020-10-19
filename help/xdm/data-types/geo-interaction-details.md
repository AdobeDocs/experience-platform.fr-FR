---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Type de données des détails de l’interaction géographique
topic: overview
description: Ce document présente un aperçu du type de données XDM Détails de l’interaction géographique.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---


# [!UICONTROL Type de données des détails] de l’interaction géographique

[!UICONTROL Les détails] de l’interaction géographique sont un type de données XDM standard qui décrit l’état actuel de l’inclusion dans une zone géographiquement définie.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forme géographique]](./geo-shape.md) | Décrit la forme géographique de la zone avec laquelle l’interaction a lieu. Ce champ peut décrire une zone, un cercle ou un polygone. |
| `deviceGeoAccuracy` | Double | Précision du dispositif ou mécanisme de mesure géographique, mesurée en mètres. |
| `distanceToCenter` | Double | La distance au centre de la zone géographique dans le cas d&#39;un cercle géographique, mesurée en mètres. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)

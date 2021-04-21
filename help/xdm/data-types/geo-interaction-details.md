---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; balise ; détails de l'interaction ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données Détails de l’interaction géographique
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM Détails de l’interaction géographique.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 5%

---

# [!UICONTROL Type de données ] détaillé de l’interaction géographique

[!UICONTROL Les ] détails de l’interaction géographique correspondent à un type de données XDM standard qui décrit l’état actuel de l’inclusion dans une zone géographiquement définie.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forme géographique]](./geo-shape.md) | Décrit la forme géographique de la zone avec laquelle l’interaction a lieu. Ce champ peut décrire une zone, un cercle ou un polygone. |
| `deviceGeoAccuracy` | Double | Précision du dispositif ou mécanisme de mesure géographique, mesurée en mètres. |
| `distanceToCenter` | Doublon | La distance au centre de la zone géographique dans le cas d&#39;un cercle géographique, mesurée en mètres. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)

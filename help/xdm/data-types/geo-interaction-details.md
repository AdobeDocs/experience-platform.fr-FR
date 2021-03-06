---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;balise;détails d’interaction;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Détails de l’interaction géographique
topic-legacy: overview
description: Ce document présente le type de données XDM Détails de l’interaction géographique .
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 6%

---

# [!UICONTROL Type de données ] détaillé des interactions géographiques

[!UICONTROL Les ] détails de l’interaction géographique correspondent à un type de données XDM standard qui décrit l’état actuel de l’inclusion dans une zone définie géographiquement.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forme géographique]](./geo-shape.md) | Décrit la forme géographique de la zone avec laquelle l’interaction s’est déroulée. Ce champ peut décrire une boîte, un cercle ou un polygone. |
| `deviceGeoAccuracy` | Double | Précision de l’appareil ou du mécanisme de géolocalisation, mesuré en mètres. |
| `distanceToCenter` | Double | Distance au centre de la zone géographique dans le cas d’un cercle géographique, mesurée en mètres. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)

---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; géo ; coordonnées ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données Coordonnées géographiques
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM des coordonnées géographiques.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 15%

---

# [!UICONTROL Type de données ] Coordonnées géographiques

[!UICONTROL Geo ] Coordinatesis est un type de données XDM standard qui décrit les coordonnées géographiques d&#39;un lieu. Ce type de données est basé sur la spécification publique documentée sur [schéma.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.description` | Chaîne | Description de ce que les coordonnées identifient. |
| `_schema.elevation` | Double | L&#39;élévation spécifique de la coordonnée définie. La valeur doit être conforme à la référence [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) et est mesurée en mètres. |
| `_schema.latitude` | Doublon | Coordonnée verticale signée du point géographique. |
| `_schema.longitude` | Doublon | Coordonnée horizontale signée du point géographique. |
| `_id` | Chaîne | Identifiant unique généré par le système pour les coordonnées. |

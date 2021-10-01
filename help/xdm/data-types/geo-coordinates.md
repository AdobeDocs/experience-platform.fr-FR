---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;géo;coordonnées;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Coordonnées géographiques
topic-legacy: overview
description: Ce document présente le type de données XDM Coordonnées géographiques.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 15%

---

# [!UICONTROL Type Geo ] Coordinatesdata

[!UICONTROL La ] coordination géographique désigne un type de données XDM standard qui décrit les coordonnées géographiques d’un lieu. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.description` | Chaîne | Description de ce que les coordonnées identifient. |
| `_schema.elevation` | Double | Élévation spécifique de la coordonnée définie. La valeur doit être conforme à la référence [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. |
| `_schema.latitude` | Double | Coordonnée verticale signée du point géographique. |
| `_schema.longitude` | Double | Coordonnée horizontale signée du point géographique. |
| `_id` | Chaîne | Identifiant unique généré par le système pour les coordonnées. |

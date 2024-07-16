---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;géo;coordonnées;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Coordonnées géographiques
description: Découvrez le type de données XDM Coordonnées géographiques.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 13%

---

# Type de données [!UICONTROL Geo Coordinates]

[!UICONTROL Geo Coordinates] est un type de données XDM standard qui décrit les coordonnées géographiques d’un lieu. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.description` | Chaîne | Description de ce que les coordonnées identifient. |
| `_schema.elevation` | Double | Élévation spécifique de la coordonnée définie. La valeur doit être conforme à la référence [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. |
| `_schema.latitude` | Double | Coordonnée verticale signée du point géographique. |
| `_schema.longitude` | Double | Coordonnée horizontale signée du point géographique. |
| `_id` | Chaîne | Identifiant unique généré par le système pour les coordonnées. |

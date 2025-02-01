---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;géo;coordonnées;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données des coordonnées géographiques
description: Découvrez le type de données XDM Coordonnées géographiques .
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 12%

---

# [!UICONTROL Coordonnées géographiques] type de données

[!UICONTROL Coordonnées géographiques] est un type de données XDM standard qui décrit les coordonnées géographiques d’un lieu. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoCoordinates).

![](../images/data-types/geo-coordinates.png){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.description` | Chaîne | Description de ce que les coordonnées identifient. |
| `_schema.elevation` | Double | Altitude spécifique de la coordonnée définie. La valeur doit être conforme au système [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et est mesurée en mètres. |
| `_schema.latitude` | Double | Coordonnée verticale signée du point géographique. |
| `_schema.longitude` | Double | Coordonnée horizontale signée du point géographique. |
| `_id` | Chaîne | Identifiant unique généré par le système pour les coordonnées. |

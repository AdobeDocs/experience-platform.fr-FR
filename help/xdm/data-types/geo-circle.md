---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;géo;cercle;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de cercle géographique
description: Découvrez le type de données XDM Geo Circle.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 17%

---

# Type de données [!UICONTROL Cercle géographique]

[!UICONTROL Cercle géographique] est un type de données XDM standard qui décrit une région géographique circulaire, selon un rayon particulier centré sur un ensemble spécifique de coordonnées. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoCircle).

![](../images/data-types/geo-circle.png){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordonnées géographiques]](./geo-coordinates.md) | Décrit les coordonnées géographiques du centre du cercle. |
| `_schema.description` | Chaîne | Description du contenu du cercle. |
| `_schema.radius` | Double | Longueur du rayon du cercle. Cette valeur est conforme au système [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et est mesurée en mètres. |
| `_id` | Chaîne | Identifiant unique généré par le système pour le cercle. |

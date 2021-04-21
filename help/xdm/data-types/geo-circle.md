---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;geo;circle;datatype;data-type;data type;data type;
solution: Experience Platform
title: Type de données du cercle géographique
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM du cercle géographique.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 23%

---

# [!UICONTROL Type de données Geo ] Circledata

[!UICONTROL Geo ] Circlette est un type de données XDM standard qui décrit une région géographique circulaire, à partir d&#39;un rayon spécifique centré sur un ensemble spécifique de coordonnées. Ce type de données est basé sur la spécification publique documentée sur [schéma.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordonnées géographiques]](./geo-coordinates.md) | Décrit les coordonnées géographiques du centre du cercle. |
| `_schema.description` | Chaîne | Description de ce que contient le cercle. |
| `_schema.radius` | Double | Longueur du rayon du cercle. Cette valeur est conforme à la référence [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. |
| `_id` | Chaîne | Identifiant unique généré par le système pour le cercle. |

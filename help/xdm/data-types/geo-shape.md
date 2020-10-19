---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;geo shape;datatype;data-type;data type;
solution: Experience Platform
title: Type de données de forme géo
topic: overview
description: Ce document présente un aperçu du type de données XDM de la forme géographique.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 39%

---


# [!UICONTROL Type de données de la forme] géographique

[!UICONTROL Geo Shape] est un type de données XDM standard qui décrit la forme d&#39;une zone géographique. Ce type de données est basé sur la spécification publique documentée sur [schéma.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.box` | Tableau de coordonnées [[!UICONTROL géographiques]](./geo-coordinates.md) | Décrit une zone géographique délimitée par un rectangle formé de deux coordonnées. La première coordonnée est l’angle inférieur du rectangle et la seconde l’angle supérieur. |
| `_schema.circle` | Tableau de coordonnées [[!UICONTROL géographiques]](./geo-coordinates.md) | Décrit une région circulaire avec un rayon spécifique centré sur une coordonnée géographique. |
| `_schema.polygon` | [[!UICONTROL Cercle géographique]](./geo-circle.md) | Série d’au moins quatre coordonnées dans laquelle la première et la dernière coordonnée sont identiques. |
| `_schema.description` | Chaîne | Description de la forme définie. |
| `_schema.elevation` | Double | Élévation spécifique ou minimale de la forme. Cette valeur est conforme à la référence [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. Combinée avec `ceiling`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |
| `_id` | Chaîne | Identificateur unique généré par le système pour la forme. |
| `ceiling` | Double | Élévation maximale de la forme. Cette propriété n’est valide que si elle est utilisée en combinaison avec `elevation`. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters. Combinée avec `elevation`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |

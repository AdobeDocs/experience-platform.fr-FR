---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; géo ; géo ; forme de données ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données de forme géo
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM de la forme géographique.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 36%

---

# [!UICONTROL Type ] de données GeoShapedata

[!UICONTROL Geo ] Shapeis est un type de données XDM standard qui décrit la forme d&#39;une zone géographique. Ce type de données est basé sur la spécification publique documentée sur [schéma.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.box` | Tableau de [[!UICONTROL coordonnées géographiques]](./geo-coordinates.md) | Décrit une zone géographique délimitée par un rectangle formé de deux coordonnées. La première coordonnée est l’angle inférieur du rectangle et la seconde l’angle supérieur. |
| `_schema.circle` | Tableau de [[!UICONTROL coordonnées géographiques]](./geo-coordinates.md) | Décrit une région circulaire avec un rayon spécifique centré sur une coordonnée géographique. |
| `_schema.polygon` | [[!UICONTROL Cercle géographique]](./geo-circle.md) | Série d’au moins quatre coordonnées dans laquelle la première et la dernière coordonnée sont identiques. |
| `_schema.description` | Chaîne | Description de la forme définie. |
| `_schema.elevation` | Double | Élévation spécifique ou minimale de la forme. Cette valeur est conforme à la référence [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. Combinée avec `ceiling`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |
| `_id` | Chaîne | Identificateur unique généré par le système pour la forme. |
| `ceiling` | Doublon | Élévation maximale de la forme. Cette propriété n&#39;est valide que si elle est utilisée en combinaison avec `elevation`. La valeur est conforme à la référence [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) et est mesurée en mètres. Combinée avec `elevation`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |

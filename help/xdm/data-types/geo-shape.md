---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;géo;forme géographique;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de forme géographique
description: Découvrez le type de données XDM Geo Shape.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 31%

---

# Type de données [!UICONTROL Geo Shape]

[!UICONTROL Geo Shape] est un type de données XDM standard qui décrit la forme d’une zone géographique. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.box` | Tableau des [[!UICONTROL coordonnées géographiques]](./geo-coordinates.md) | Décrit une zone géographique délimitée par un rectangle formé de deux coordonnées. La première coordonnée est le coin inférieur du rectangle, la seconde l’angle supérieur. |
| `_schema.circle` | Tableau des [[!UICONTROL coordonnées géographiques]](./geo-coordinates.md) | Décrit une région circulaire avec un rayon spécifique centré sur une coordonnée géographique. |
| `_schema.polygon` | [[!UICONTROL Cercle géo]](./geo-circle.md) | Série de quatre coordonnées ou plus dont les coordonnées première et finale sont identiques. |
| `_schema.description` | Chaîne | Description de ce qui est défini par la forme. |
| `_schema.elevation` | Double | Élévation spécifique ou minimale de la forme. Cette valeur est conforme à la référence [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. Combinée avec `ceiling`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |
| `_id` | Chaîne | Identifiant unique généré par le système pour la forme. |
| `ceiling` | Double | Élévation maximale de la forme. Cette propriété n’est valide que lorsqu’elle est utilisée en combinaison avec `elevation`. La valeur est conforme à la référence [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. Combinée avec `elevation`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |

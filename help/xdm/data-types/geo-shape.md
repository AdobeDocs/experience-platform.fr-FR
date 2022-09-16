---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;géo;forme géographique;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de forme géographique
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM de la forme géographique.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 34%

---

# [!UICONTROL Forme géographique] type de données

[!UICONTROL Forme géographique] est un type de données XDM standard qui décrit la forme d’une zone géographique. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.box` | Tableau de [[!UICONTROL Coordonnées géographiques]](./geo-coordinates.md) | Décrit une zone géographique délimitée par un rectangle formé de deux coordonnées. La première coordonnée est le coin inférieur du rectangle, la seconde l’angle supérieur. |
| `_schema.circle` | Tableau de [[!UICONTROL Coordonnées géographiques]](./geo-coordinates.md) | Décrit une région circulaire avec un rayon spécifique centré sur une coordonnée géographique. |
| `_schema.polygon` | [[!UICONTROL Cercle géographique]](./geo-circle.md) | Série d’au moins quatre coordonnées dans laquelle la première et la dernière coordonnée sont identiques. |
| `_schema.description` | Chaîne | Description de la forme définie. |
| `_schema.elevation` | Double | Élévation spécifique ou minimale de la forme. Cette valeur est conforme à la référence [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. Combinée avec `ceiling`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |
| `_id` | Chaîne | Identifiant unique généré par le système pour la forme. |
| `ceiling` | Double | Élévation maximale de la forme. Cette propriété n’est valide que lorsqu’elle est utilisée conjointement avec `elevation`. La valeur est conforme à la variable [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum et est mesuré en mètres. Combinée avec `elevation`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |

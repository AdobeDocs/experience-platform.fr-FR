---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;géo;forme géographique;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de forme géographique
description: En savoir plus sur le type de données XDM de forme géographique.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
TQID: https://experienceleague.adobe.com/2D0Z7wkA8uFm7UV26vfK46-bU6WetUzx3Qh6T5iuKv4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 244
ht-degree: 34%

---

# Type de données [!UICONTROL Geo Shape]

[!UICONTROL Geo Shape] est un type de données XDM standard qui décrit la forme d’une zone géographique. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoShape).

![](../images/data-types/geo-shape.png){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.box` | Tableau de [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Décrit une zone géographique délimitée par un rectangle formé par deux coordonnées. La première coordonnée est le coin inférieur du rectangle, et la seconde coordonnée est le coin supérieur. |
| `_schema.circle` | Tableau de [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Décrit une zone circulaire ayant un rayon donné, centrée sur une coordonnée géographique. |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | Série d’au moins quatre coordonnées dans laquelle la première et la dernière coordonnée sont identiques. |
| `_schema.description` | Chaîne | Description de ce que la forme définit. |
| `_schema.elevation` | Double | Élévation spécifique ou minimale de la forme. Cette valeur est conforme à la référence [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. Combinée avec `ceiling`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |
| `_id` | Chaîne | Identifiant unique généré par le système pour la forme. |
| `ceiling` | Double | Élévation maximale de la forme. Cette propriété n’est valide que lorsqu’elle est utilisée en combinaison avec `elevation`. La valeur est conforme au système [&#128279;](https://gisgeography.com/wgs84-world-geodetic-system/) et est mesurée en mètres. Combinée avec `elevation`, vous pouvez utiliser cette propriété pour exprimer un cadre de sélection tridimensionnel pour un emplacement. |

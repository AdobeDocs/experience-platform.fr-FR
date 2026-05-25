---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;géo;cercle;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de cercle géographique
description: Découvrez le type de données XDM Geo Circle.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
TQID: https://experienceleague.adobe.com/HyRugrJeTrQHUiCVGvvXlzt91lQebXNttDx7ye4dohs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 127
ht-degree: 21%

---

# Type de données [!UICONTROL Geo Circle]

[!UICONTROL Geo Circle] est un type de données XDM standard qui décrit une région géographique circulaire, selon un rayon particulier centré sur un ensemble spécifique de coordonnées. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoCircle).

![](../images/data-types/geo-circle.png){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Décrit les coordonnées géographiques du centre du cercle. |
| `_schema.description` | Chaîne | Description du contenu du cercle. |
| `_schema.radius` | Double | Longueur du rayon du cercle. Cette valeur est conforme à la référence [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. |
| `_id` | Chaîne | Identifiant unique généré par le système pour le cercle. |

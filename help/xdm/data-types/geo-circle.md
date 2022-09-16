---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;géo;cercle;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données du cercle géographique
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM Geo Circle.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 21%

---

# [!UICONTROL Cercle géographique] type de données

[!UICONTROL Cercle géographique] est un type de données XDM standard qui décrit une région géographique circulaire, selon un rayon spécifique centré sur un ensemble spécifique de coordonnées. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordonnées géographiques]](./geo-coordinates.md) | Décrit les coordonnées géographiques du centre du cercle. |
| `_schema.description` | Chaîne | Description de ce que contient le cercle. |
| `_schema.radius` | Double | Longueur du rayon du cercle. Cette valeur est conforme à la référence [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) et elle est mesurée en mètres. |
| `_id` | Chaîne | Identifiant unique généré par le système pour le cercle. |

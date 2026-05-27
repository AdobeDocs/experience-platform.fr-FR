---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;géo;coordonnées;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données des coordonnées géographiques
description: Découvrez le type de données XDM Coordonnées géographiques .
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
TQID: https://experienceleague.adobe.com/rgrantL-dNZVgLYOWDfADMDANh9Ambta-yK5UprSI4U
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 127
ht-degree: 12%

---

# Type de données [!UICONTROL Geo Coordinates]

[!UICONTROL Geo Coordinates] est un type de données XDM standard qui décrit les coordonnées géographiques d’un lieu. Ce type de données est basé sur la spécification publique documentée sur [schema.org](https://schema.org/GeoCoordinates).

![](../images/data-types/geo-coordinates.png){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema.description` | Chaîne | Description de ce que les coordonnées identifient. |
| `_schema.elevation` | Double | Altitude spécifique de la coordonnée définie. La valeur doit être conforme au système [](https://gisgeography.com/wgs84-world-geodetic-system/) et est mesurée en mètres. |
| `_schema.latitude` | Double | Coordonnée verticale signée du point géographique. |
| `_schema.longitude` | Double | Coordonnée horizontale signée du point géographique. |
| `_id` | Chaîne | Identifiant unique généré par le système pour les coordonnées. |

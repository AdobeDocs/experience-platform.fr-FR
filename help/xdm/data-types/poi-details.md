---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;champs;schémas;schémas;poi;détails du point ciblé;détails du point ciblé;type de données;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Détails du point ciblé
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM Point ciblé Details .
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 15%

---

# [!UICONTROL Type de données des ] détails du point ciblé

[!UICONTROL Les ] détails du point ciblé correspondent à un type de données XDM standard qui décrit les données géographiques dans lesquelles un événement a été observé.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Balise]](./beacon.md) | Décrit les détails de la balise principaux pour l’interaction du point ciblé. |
| `geoInteractionDetails` | [[!UICONTROL Détails des interactions géographiques]](./geo-interaction-details.md) | Décrit les détails géographiques principaux pour l’interaction du point ciblé. |
| `category` | Chaîne | Catégorie générale affectée à l’organisation des points ciblés par l’administrateur des définitions des points ciblés. |
| `distanceToPOICenter` | Double | Distance estimée depuis le centre du point ciblé en mètres. |
| `locatingType` | Chaîne | Mécanisme utilisé pour déterminer la position. Les valeurs acceptées sont les suivantes : <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Chaîne | Nom donné au point ciblé. |
| `poiID` | Chaîne | Identifiant unique du point ciblé. |
| `type` | Chaîne | Type général du point ciblé qui utilise un schéma de saisie sélectionné par l’administrateur des définitions des points ciblés. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)

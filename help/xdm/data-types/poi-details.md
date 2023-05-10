---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;champs;schémas;schémas;poi;détails du point ciblé;détails du point ciblé;type de données;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Détails du point ciblé
description: Ce document fournit un aperçu du type de données XDM Point ciblé Details .
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 26%

---

# [!UICONTROL Détails des points ciblés] type de données

[!UICONTROL Détails des points ciblés] est un type de données XDM standard qui décrit les données géographiques où un événement a été observé.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Repère]](./beacon.md) | Décrit les détails de la balise principaux pour l’interaction du point ciblé. |
| `geoInteractionDetails` | [[!UICONTROL Informations sur l’interaction géographique]](./geo-interaction-details.md) | Décrit les détails géographiques principaux pour l’interaction du point ciblé. |
| `category` | Chaîne | Catégorie générale affectée à l’organisation des points ciblés par l’administrateur des définitions des points ciblés. |
| `distanceToPOICenter` | Double | Distance estimée depuis le centre du point ciblé en mètres. |
| `locatingType` | Chaîne | Mécanisme utilisé pour déterminer la position. Les valeurs acceptées sont les suivantes : <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Chaîne | Nom donné au point ciblé. |
| `poiID` | Chaîne | Identifiant unique du point ciblé. |
| `type` | Chaîne | Type général du point ciblé qui utilise un schéma de saisie sélectionné par l’administrateur des définitions des points ciblés. |

{style="table-layout:auto"}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)

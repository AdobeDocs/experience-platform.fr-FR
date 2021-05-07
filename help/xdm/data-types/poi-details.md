---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; poi ; détails de la correspondance ; point d’intérêt ; détails du point d’intérêt ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données des détails du point ciblé
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM Point Of Interest Details.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 13%

---

# [!UICONTROL Type de données ] détaillé des points ciblés

[!UICONTROL Le point d&#39;intérêt ] décrit en détail un type de données XDM standard qui décrit les données géographiques où un événement a été observé.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Balise]](./beacon.md) | Décrit les détails de la balise principal pour l’interaction POI. |
| `geoInteractionDetails` | [[!UICONTROL Détails de l’interaction géographique]](./geo-interaction-details.md) | Décrit les détails géographiques principaux pour l’interaction POI. |
| `category` | Chaîne | Catégorie générale affectée à l’organisation des points d’intérêt par l’administrateur des définitions des points d’intérêt. |
| `distanceToPOICenter` | Double | La distance estimée du centre de la PDV en mètres. |
| `locatingType` | Chaîne | Mécanisme utilisé pour déterminer l’emplacement. Les valeurs acceptées sont les suivantes : <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Chaîne | Nom attribué à l’objet de propriété intellectuelle. |
| `poiID` | Chaîne | Identificateur unique de l’API. |
| `type` | Chaîne | Type général du point ciblé qui utilise un schéma de saisie sélectionné par l’administrateur des définitions des points ciblés. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)

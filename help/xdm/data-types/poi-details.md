---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;poi details;point of interest;point of interest details;datatype;data-type;data type;
solution: Experience Platform
title: Type de données des détails du point ciblé
topic: overview
description: Ce document présente un aperçu du type de données XDM Point Of Interest Details.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 16%

---


# [!UICONTROL Type de données des détails] du point d’intérêt

[!UICONTROL Les détails] du point d&#39;intérêt sont un type de données XDM standard qui décrit les données géographiques où un événement a été observé.

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

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
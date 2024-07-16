---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;champs;schémas;schémas;poi;détails du point ciblé;détails du point ciblé;type de données;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Détails du point ciblé
description: Découvrez le type de données XDM des détails du point ciblé.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 16%

---

# [!UICONTROL Détails du point ciblé] type de données

[!UICONTROL Détails du point ciblé] est un type de données XDM standard qui décrit les données géographiques où un événement a été observé.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Balise]](./beacon.md) | Décrit les détails de la balise active pour l’interaction du point ciblé. |
| `geoInteractionDetails` | [[!UICONTROL Détails de l’interaction géographique]](./geo-interaction-details.md) | Décrit les détails géographiques actifs pour l’interaction du point ciblé. |
| `category` | Chaîne | Catégorie générale affectée à l’organisation des points ciblés par l’administrateur des définitions des points ciblés. |
| `distanceToPOICenter` | Double | Distance estimée depuis le centre du point ciblé en mètres. |
| `locatingType` | Chaîne | Mécanisme utilisé pour déterminer la position. Les valeurs acceptées sont les suivantes : <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Chaîne | Nom donné au point ciblé. |
| `poiID` | Chaîne | Identifiant unique du point ciblé. |
| `type` | Chaîne | Type général du point ciblé qui utilise un schéma de saisie sélectionné par l’administrateur des définitions des points ciblés. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)

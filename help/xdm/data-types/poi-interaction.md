---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;champs;schémas;schémas;points ciblés;interaction;point ciblé;type de données;type de données;type de données;type de données
solution: Experience Platform
title: Type de données d’interaction du point ciblé
topic-legacy: overview
description: Ce document présente le type de données XDM de l’interaction Point ciblé.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 4%

---

# [!UICONTROL Type ] interactiondata de point ciblé

[!UICONTROL Les ] interactions avec les points ciblés sont un type de données XDM standard qui décrit le périphérique sans fil qui communique des informations d’identité aux applications mobiles à mesure que les périphériques mobiles entrent en portée.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Détails des points ciblés]](./poi-details.md) | Décrit les détails du point ciblé qui a provoqué l’événement. |
| `poiEntries` | Objet | Décrit le nombre de fois où une personne est entrée dans le point ciblé. Contient deux propriétés : <ul><li>`id`: Identifiant unique de la mesure.</li><li>`value`: Valeur quantifiable de la mesure.</li></ul> |
| `poiExits` | Objet | Décrit le nombre de fois où une personne a quitté le point ciblé. Contient deux propriétés : <ul><li>`id`: Identifiant unique de la mesure.</li><li>`value`: Valeur quantifiable de la mesure.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)

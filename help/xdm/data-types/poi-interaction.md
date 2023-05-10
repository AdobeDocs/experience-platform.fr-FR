---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;champs;schémas;schémas;points ciblés;interaction;point ciblé;type de données;type de données;type de données;type de données
solution: Experience Platform
title: Type de données d’interaction du point ciblé
description: Ce document présente le type de données XDM de l’interaction Point ciblé.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 12%

---

# [!UICONTROL Interaction avec le point ciblé] type de données

[!UICONTROL Interaction avec le point ciblé] est un type de données XDM standard qui décrit l’appareil sans fil qui communique des informations d’identité aux applications mobiles à mesure que les appareils mobiles sont en portée.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Détails sur le point ciblé]](./poi-details.md) | Décrit les détails du point ciblé qui a provoqué l’événement. |
| `poiEntries` | Objet | Décrit le nombre de fois où une personne est entrée dans le point ciblé. Contient deux propriétés : <ul><li>`id`: Identifiant unique de la mesure.</li><li>`value`: Valeur quantifiable de la mesure.</li></ul> |
| `poiExits` | Objet | Décrit le nombre de fois où une personne a quitté le point ciblé. Contient deux propriétés : <ul><li>`id`: Identifiant unique de la mesure.</li><li>`value`: Valeur quantifiable de la mesure.</li></ul> |

{style="table-layout:auto"}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)

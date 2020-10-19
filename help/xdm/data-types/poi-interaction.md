---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;interaction;point of interest;point-of-interest;datatype;data-type;data type;
solution: Experience Platform
title: Type de données d’interaction Point d’intérêt
topic: overview
description: Ce document présente un aperçu du type de données XDM de l’interaction Point ciblé.
translation-type: tm+mt
source-git-commit: 032adc72db7f094b268f14e8f7d48810830a84e4
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---


# [!UICONTROL Type de données d’interaction] Point d’intérêt

[!UICONTROL L&#39;interaction] Point d&#39;intérêt est un type de données XDM standard qui décrit le périphérique sans fil qui communique les informations d&#39;identité aux applications mobiles lorsque les périphériques mobiles sont compris dans la plage définie.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Détails du point d’intérêt]](./poi-details.md) | Décrit les détails de l’API à l’origine du événement. |
| `poiEntries` | Objet | Décrit le nombre de fois où une personne est entrée dans le PDV. Contient deux propriétés : <ul><li>`id`: Identificateur unique de la mesure.</li><li>`value`: Valeur quantifiable de la mesure.</li></ul> |
| `poiExits` | Objet | Décrit le nombre de fois où une personne a quitté le point d’accès. Contient deux propriétés : <ul><li>`id`: Identificateur unique de la mesure.</li><li>`value`: Valeur quantifiable de la mesure.</li></ul> |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)

---
keywords: Experience Platform ; accueil ; sujets populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; point d’intérêt ; point d’intérêt ; type de données ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données d’interaction Point ciblé
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM de l’interaction Point ciblé.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 3%

---

# [!UICONTROL Type de données d&#39;] interaction point d&#39;intérêt

[!UICONTROL Les ] interactions Point of interest sont un type de données XDM standard qui décrit le périphérique sans fil qui communique des informations d&#39;identité aux applications mobiles à mesure que les périphériques mobiles sont compris dans la plage définie.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Détails du point d’intérêt]](./poi-details.md) | Décrit les détails de l’API à l’origine du événement. |
| `poiEntries` | Objet | Décrit le nombre de fois où une personne est entrée dans le PDV. Contient deux propriétés : <ul><li>`id`: Identificateur unique de la mesure.</li><li>`value`: Valeur quantifiable de la mesure.</li></ul> |
| `poiExits` | Objet | Décrit le nombre de fois où une personne a quitté le point d’accès. Contient deux propriétés : <ul><li>`id`: Identificateur unique de la mesure.</li><li>`value`: Valeur quantifiable de la mesure.</li></ul> |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)

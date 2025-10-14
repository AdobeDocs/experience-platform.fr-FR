---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;point d’intérêt;interaction;point ciblé;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d’interaction du point ciblé
description: Découvrez le type de données XDM de l’interaction du point ciblé.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL Interaction du point ciblé] type de données

[!UICONTROL Interaction de point ciblé] est un type de données XDM standard qui décrit l’appareil sans fil qui communique des informations d’identité aux applications mobiles lorsque des appareils mobiles arrivent à portée.

![](../images/data-types/poi-interaction.png){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Détails du point ciblé]](./poi-details.md) | Décrit les détails du point d’intérêt qui a provoqué l’événement. |
| `poiEntries` | Objet | Décrit le nombre de fois qu’une personne a accédé au point d’intérêt. Contient deux propriétés : <ul><li>`id` : identifiant unique de la mesure.</li><li>`value` : valeur quantifiable de la mesure.</li></ul> |
| `poiExits` | Objet | Décrit le nombre de fois qu’une personne a quitté le point d’intérêt. Contient deux propriétés : <ul><li>`id` : identifiant unique de la mesure.</li><li>`value` : valeur quantifiable de la mesure.</li></ul> |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)

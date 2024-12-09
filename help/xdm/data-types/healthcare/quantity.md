---
title: Type de données de quantité
description: Découvrez le type de données Quantity Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 11%

---

# Type de données [!UICONTROL Quantity]

[!UICONTROL Quantity] est un type de données XDM (Experience Data Model) standard qui fournit une quantité mesurée ou mesurable. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données Quantité](../../images/data-types/healthcare/quantity.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Forme codée de l’unité. |
| [!UICONTROL Comparateur] | `comparator` | Chaîne | Opérateur de comparaison. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL Système] | `system` | Chaîne | Système qui définit le formulaire d’unité codée, représenté sous la forme d’un URI. |
| [!UICONTROL Unit] | `unit` | Chaîne | Représentation de l’unité. |
| [!UICONTROL Valeur] | `value` | Double | Valeur numérique. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)

---
title: Type de données d’adresse
description: Découvrez le type de données du modèle de données d’expérience d’adresse (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 10%

---

# Type de données [!UICONTROL Address]

[!UICONTROL Address] est un type de données XDM (Experience Data Model) standard qui décrit une adresse exprimée à l’aide de conventions postales (par opposition au GPS ou à d’autres formats de définition d’emplacement). Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données d’adresse](../../images/data-types/healthcare/address.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../healthcare/period.md) | Période pendant laquelle l’adresse était/est en cours d’utilisation. |
| [!UICONTROL Ville] | `city` | Chaîne | Nom de la ville. |
| [!UICONTROL Country] | `country` | Chaîne | Code de pays décrit dans la norme internationale ISO 3166. Le code peut être alpha-2 ou alpha-3. |
| [!UICONTROL District] | `district` | Chaîne | Nom du district. |
| [!UICONTROL Line] | `line` | Chaîne | Nom, numéro, direction, boîte de réception ou autre. |
| [!UICONTROL Postal Code] | `postalCode` | Chaîne | Code postal. |
| [!UICONTROL État] | `state` | Chaîne | Sous-unité d’un pays. Les abréviations sont acceptables. |
| [!UICONTROL Texte] | `text` | Chaîne | Représentation textuelle de l’adresse. |
| [!UICONTROL Type] | `type` | Chaîne | Type d’adresse. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL Utiliser] | `use` | Chaîne | L’objet de l’adresse. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)

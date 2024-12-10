---
title: Type de données du point de contact
description: Découvrez le type de données du modèle de données d’expérience (XDM) du point de contact.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: bbb9a5e1-b0d5-4c07-93a9-c1573dacad73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# Type de données [!UICONTROL Point de contact]

[!UICONTROL Contact Point] est un type de données XDM (Experience Data Model) standard qui décrit les coordonnées d’une personne. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de point de contact](../../../images/healthcare/data-types/contact-point.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../data-types/period.md) | Période pendant laquelle le point de contact a été/est en cours d’utilisation. |
| [!UICONTROL Classement] | `rank` | Nombre entier | Classement indiquant la préférence d’utilisation du point de contact. La valeur minimale est `1` et la valeur maximale est `2147483647` où `1` est la plus haute spécificité. |
| [!UICONTROL Système] | `system` | Chaîne | Système par lequel ils peuvent être contactés. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL Utiliser] | `use` | Chaîne | L’objet du point de contact. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL Valeur] | `value` | Chaîne | Les détails du point de contact. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)

---
title: Type de données de point de contact
description: Découvrez le type de données du modèle de données d’expérience du point de contact (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: bbb9a5e1-b0d5-4c07-93a9-c1573dacad73
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 6%

---

# Type de données [!UICONTROL Contact Point]

[!UICONTROL Contact Point] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les détails de contact d’une personne. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données du point de contact](../../../images/healthcare/data-types/contact-point.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Période pendant laquelle le point de contact a été/est utilisé. |
| [!UICONTROL Rank] | `rank` | Entier | Classement indiquant l’utilisation préférée du point de contact. La valeur minimale est `1` et la valeur maximale est `2147483647` où `1` est la spécificité la plus élevée. |
| [!UICONTROL System] | `system` | Chaîne | Système par lequel ils peuvent être contactés. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL Use] | `use` | Chaîne | Objectif du point de contact. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL Value] | `value` | Chaîne | Détails du point de contact. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)

---
title: Type de données de période
description: Découvrez le type de données du modèle de données d’expérience de la période (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 8%

---

# Type de données [!UICONTROL Period]

[!UICONTROL Period] est un type de données standard du modèle de données d’expérience (XDM) qui fournit une période définie par une date/heure de début et de fin. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de la période](../../../images/healthcare/data-types/period.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL End] | `end` | DateTime | Date et heure de fin. |
| [!UICONTROL Start] | `start` | DateTime | Date et heure de début. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)

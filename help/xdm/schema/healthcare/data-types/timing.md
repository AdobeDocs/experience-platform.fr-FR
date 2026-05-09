---
title: Type de données de minutage
description: Découvrez le type de données Modèle de données d’expérience de minutage (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 6%

---

# Type de données [!UICONTROL Timing]

[!UICONTROL Timing] est un type de données standard du modèle de données d’expérience (XDM) qui décrit un planning qui fournit des informations sur un événement qui peut se produire plusieurs fois. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de minutage](../../../images/healthcare/data-types/timing.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Event] | `event` | Tableau de date et heure | Lorsque l’événement se produit. |
| [!UICONTROL Repeat] | `repeat` | [[!UICONTROL Repeat]](../data-types/repeat.md) | Informations sur le moment où l’événement se produit. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Le code relatif à l’événement. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)

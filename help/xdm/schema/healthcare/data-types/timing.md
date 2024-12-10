---
title: Type de données de minutage
description: Découvrez le type de données du modèle de données d’expérience de minutage (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 9%

---

# Type de données [!UICONTROL Timing]

[!UICONTROL Timing] est un type de données XDM (Experience Data Model) standard qui décrit un planning de minutage qui fournit des informations sur un événement qui peut se produire plusieurs fois. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure du type de données minutage](../../../images/healthcare/data-types/timing.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Événement] | `event` | Tableau de DateTime | Lorsque l’événement se produit. |
| [!UICONTROL Répéter] | `repeat` | [[!UICONTROL Répéter]](../data-types/repeat.md) | Informations sur le moment où l’événement se produit. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Code associé à l’événement. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)

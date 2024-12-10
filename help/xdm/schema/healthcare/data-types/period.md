---
title: Type de données de période
description: Découvrez le type de données du modèle de données d’expérience de période (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 12%

---

# Type de données [!UICONTROL Period]

[!UICONTROL Period] est un type de données XDM (Experience Data Model) standard qui fournit une période définie par une date/heure de début et de fin. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de période](../../../images/healthcare/data-types/period.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Fin] | `end` | DateTime | Date et heure de fin. |
| [!UICONTROL Début] | `start` | DateTime | Date et heure de début. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)

---
title: Type de données de période
description: Découvrez le type de données du modèle de données d’expérience de période (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 12%

---

# Type de données [!UICONTROL Period]

[!UICONTROL Period] est un type de données XDM (Experience Data Model) standard qui fournit une période définie par une date/heure de début et de fin. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de période](../../images/data-types/healthcare/period.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Fin] | `end` | DateTime | Date et heure de fin. |
| [!UICONTROL Début] | `start` | DateTime | Date et heure de début. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)

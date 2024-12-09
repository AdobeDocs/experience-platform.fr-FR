---
title: Type de données de durée
description: Découvrez le type de données du modèle de données d’expérience de durée (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# Type de données [!UICONTROL Durée]

[!UICONTROL Durée] est un type de données XDM (Experience Data Model) standard qui décrit une durée. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de durée](../../images/data-types/healthcare/duration.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Forme codée de l’unité de temps. |
| [!UICONTROL Système] | `system` | Chaîne | Système qui décrit l’unité codée, représentée sous la forme d’un URI. |
| [!UICONTROL Unit] | `unit` | Chaîne | Unité de temps représentée en millisecondes, secondes, minutes, heures, jours, semaines, mois ou années. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `ms` (millisecondes) </li> <li> `s` (secondes) </li> <li> `min` (minutes) </li> <li> `h` (heures) </li>  <li> `d` (jours) </li> <li> `wk` (semaines) </li> <li> `mo` (mois) </li> <li> `a` (années) </li> |
| [!UICONTROL Valeur] | `value` | Double | Valeur numérique de l’unité de temps. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)

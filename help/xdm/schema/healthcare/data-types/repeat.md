---
title: Type de données répété
description: Découvrez le type de données Répéter le modèle de données d’expérience (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 9d40bc1d-33d1-4c33-a143-13fdcf8dc255
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 7%

---

# Type de données [!UICONTROL Repeat]

[!UICONTROL Répéter] est un type de données XDM (Experience Data Model) standard qui fournit un ensemble de règles qui décrivent quand un événement est planifié. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Répéter la structure de type de données](../../../images/healthcare/data-types/reference.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Période limite] | `boundsPeriod` | [[!UICONTROL Période]](../data-types/period.md) | Heures de début et de fin. |
| [!UICONTROL Plage limite] | `boundsRange` | [[!UICONTROL Plage]](../data-types/range.md) | Limite de plage. |
| [!UICONTROL Durée de liaison] | `boundsDuration` | [[!UICONTROL Durée]](../data-types/duration.md) | Limite de durée. |
| [!UICONTROL Count] | `count` | Nombre entier | Nombre de répétitions, avec une valeur minimale de `0`. |
| [!UICONTROL Nombre maximal] | `countMax` | Nombre entier | Nombre maximal de répétitions, avec une valeur minimale de `0`. |
| [!UICONTROL Jour De La Semaine] | `dayOfWeek` | Tableau de chaînes | Tableau de chaînes détaillant les jours disponibles. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Durée] | `duration` | Double | Durée. |
| [!UICONTROL Durée maximale] | `durationMax` | Double | Durée maximale. |
| [!UICONTROL Unité de durée] | `durationUnit` | Chaîne | Unité de durée. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `s` (secondes) </li> <li> `min` (minutes) </li> <li> `h` (toutes les heures) </li> <li> `d` (quotidien) </li>  <li> `wk` (hebdomadaire) </li> <li> `mo` (mensuel) </li> <li> `a` (annuel)</li> |
| [!UICONTROL Fréquence] | `frequency` | Double | Nombre de répétitions qui doivent se produire au cours d’une période, avec une valeur minimale de `0`. |
| [!UICONTROL Fréquence maximale] | `frequencyMax` | Double | Nombre maximal de répétitions qui doivent se produire avec un point, avec une valeur minimale de `0`. |
| [!UICONTROL Décalage] | `offset` | Nombre entier | La ou les minutes jusqu’à l’événement (avant ou après). |
| [!UICONTROL Période] | `period` | Double | Durée pendant laquelle la fréquence s’applique. |
| [!UICONTROL Période maximale] | `periodMax` | Double | Limite supérieure de la période. |
| [!UICONTROL Unité de période] | `periodUnit` | Chaîne | Unité de temps. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `s` (secondes) </li> <li> `min` (minutes) </li> <li> `h` (toutes les heures) </li> <li> `d` (quotidien) </li>  <li> `wk` (hebdomadaire) </li> <li> `mo` (mensuel) </li> <li> `a` (annuel)</li> |
| [!UICONTROL Heure De La Journée] | `timeOfDay` | Tableau de chaînes | Heure de la journée à laquelle l’action doit se produire. |
| [!UICONTROL When] | `when` | Tableau de chaînes | Code de la période de l’action. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)

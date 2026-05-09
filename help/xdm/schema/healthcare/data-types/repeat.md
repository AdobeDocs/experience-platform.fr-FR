---
title: Répéter le type de données
description: Découvrez le type de données du modèle de données d’expérience de répétition (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 9d40bc1d-33d1-4c33-a143-13fdcf8dc255
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 5%

---

# Type de données [!UICONTROL Repeat]

[!UICONTROL Repeat] est un type de données standard du modèle de données d’expérience (XDM) qui fournit un ensemble de règles qui décrivent quand un événement est planifié. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Répéter la structure du type de données](../../../images/healthcare/data-types/reference.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Bound Period] | `boundsPeriod` | [[!UICONTROL Period]](../data-types/period.md) | Heures de début et de fin. |
| [!UICONTROL Bound Range] | `boundsRange` | [[!UICONTROL Range]](../data-types/range.md) | La limite de la plage. |
| [!UICONTROL Bound Duration] | `boundsDuration` | [[!UICONTROL Duration]](../data-types/duration.md) | La limite de durée. |
| [!UICONTROL Count] | `count` | Entier | Nombre de répétitions avec une valeur minimale de `0`. |
| [!UICONTROL Maximum Count] | `countMax` | Entier | Nombre maximal de répétitions, avec une valeur minimale de `0`. |
| [!UICONTROL Day Of Week] | `dayOfWeek` | Tableau de chaînes | Tableau de chaînes détaillant les jours disponibles. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Duration] | `duration` | Double | La durée. |
| [!UICONTROL Maximum Duration] | `durationMax` | Double | Durée maximale. |
| [!UICONTROL Duration Unit] | `durationUnit` | Chaîne | Unité de durée. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `s` (secondes) </li> <li> `min` (minutes) </li> <li> `h` (par heure) </li> <li> `d` (quotidien) </li>  <li> `wk` (hebdomadaire) </li> <li> `mo` (mensuel) </li> <li> `a` (annuel)</li> |
| [!UICONTROL Frequency] | `frequency` | Double | Nombre de répétitions devant se produire au cours d’une période, avec une valeur minimale de `0`. |
| [!UICONTROL Maximum Frequency] | `frequencyMax` | Double | Nombre maximal de répétitions qui doivent se produire avec un point, avec une valeur minimale de `0`. |
| [!UICONTROL Offset] | `offset` | Entier | Minute(s) avant l’événement (avant ou après). |
| [!UICONTROL Period] | `period` | Double | Durée pendant laquelle la fréquence s’applique. |
| [!UICONTROL Maximum Period] | `periodMax` | Double | Limite supérieure de la période. |
| [!UICONTROL Period Unit] | `periodUnit` | Chaîne | Unité de temps. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `s` (secondes) </li> <li> `min` (minutes) </li> <li> `h` (par heure) </li> <li> `d` (quotidien) </li>  <li> `wk` (hebdomadaire) </li> <li> `mo` (mensuel) </li> <li> `a` (annuel)</li> |
| [!UICONTROL Time Of Day] | `timeOfDay` | Tableau de chaînes | Heure de la journée à laquelle l’action doit se produire. |
| [!UICONTROL When] | `when` | Tableau de chaînes | Code de la période de l’action. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)

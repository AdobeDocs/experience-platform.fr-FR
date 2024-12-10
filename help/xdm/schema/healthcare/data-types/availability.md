---
title: Type de données de disponibilité
description: Découvrez le type de données Disponibilité du modèle de données d’expérience (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 18c0b767-adf0-480e-9cf2-63e21d05b362
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 9%

---

# Type de données [!UICONTROL Disponibilité]

[!UICONTROL Disponibilité] est un type de données XDM (Experience Data Model) standard qui décrit les données de disponibilité d’un article. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de disponibilité](../../../images/healthcare/data-types/availability/availability.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Durée disponible] | `availableTime` | Tableau d’objets | Heures pendant lesquelles l’élément est disponible. Pour plus d’informations, consultez la [section ci-dessous](#available-time) . |
| [!UICONTROL Heure non disponible] | `notAvailableTime` | Chaîne | Heures pendant lesquelles l’élément n’est pas disponible, avec une raison fournie. Pour plus d’informations, consultez la [section ci-dessous](#not-available-time) . |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.schema.json)

## `availableTime` {#available-time}

`availableTime` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![Structure de temps disponible](../../../images/healthcare/data-types/availability/available-time.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Toute la journée] | `allDay` | Booléen | Valeur booléenne indiquant si l’élément est toujours disponible. |
| [!UICONTROL Heure de fin disponible] | `availableEndTime` | Chaîne | L’heure de la journée à laquelle l’élément cesse d’être disponible. Cela est ignoré si `allDay` est `true`. |
| [!UICONTROL Heure de début disponible] | `availableStartTime` | Chaîne | Heure à laquelle l’élément commence à être disponible. Cela est ignoré si `allDay` est `true`. |
| [!UICONTROL Jours De La Semaine] | `daysOfWeek` | Tableau de chaînes | Tableau de chaînes détaillant les jours disponibles. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |

## `notAvailableTime` {#not-available-time}

`notAvailableTime` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![Structure de temps non disponible](../../../images/healthcare/data-types/availability/not-available-time.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Durant] | `during` | [[!UICONTROL Période]](../data-types/period.md) | La période pendant laquelle l’élément cesse d’être disponible. |
| [!UICONTROL Description] | `description` | Chaîne | La raison pour laquelle l’élément n’est pas disponible. |

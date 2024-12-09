---
title: Type de données de personne
description: Découvrez le type de données du modèle de données d’expérience de personne (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 8%

---

# Type de données [!UICONTROL Person]

[!UICONTROL Person] est un type de données XDM (Experience Data Model) standard qui fournit des informations sur un enregistrement de personne générique. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données Personne](../../images/data-types/healthcare/person/person.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | Tableau de [[!UICONTROL Address]](../healthcare/address.md) | Une ou plusieurs adresses pour la personne. |
| [!UICONTROL Communication] | `communication` | Tableau d’objets | Une langue qui peut être utilisée pour communiquer avec la personne au sujet de sa santé. Pour plus d’informations, consultez la [section ci-dessous](#communication) . |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../healthcare/identifier.md) | Identifiant humain de cette personne. |
| [!UICONTROL Détails du lien de personne] | `link` | Tableau d’objets | Lien vers une ressource qui concerne la même personne. Pour plus d’informations, consultez la [section ci-dessous](#link) . |
| [!UICONTROL Gestion de l’organisation] | `managingOrganization` | [[!UICONTROL Référence]](../healthcare/reference.md) | L’organisation qui est le gardien du dossier du patient. |
| [!UICONTROL État civil] | `maritalStatus` | [[!UICONTROL Concept codeable]](../healthcare/codeable-concept.md) | État civil (civil) d’une personne |
| [!UICONTROL Nom] | `name` | Tableau de [[!UICONTROL Nom de l’homme]](../healthcare/human-name.md) | Noms associés à une personne. |
| [!UICONTROL Détails du contact] | `telecom` | Tableau de [[!UICONTROL Point de contact]] | Les coordonnées par lesquelles la personne peut être contactée. |
| [!UICONTROL Est Actif] | `active` | Booléen | Indique si l’enregistrement de la personne est en cours d’utilisation. |
| [!UICONTROL Date de naissance] | `birthDate` | Date | Date de naissance de la personne. |
| [!UICONTROL Indicateur déposé] | `deceasedBoolean` | Booléen | Indique si la personne est décédée ou non. |
| [!UICONTROL Heure de date de décès] | `deceasedDateTime` | DateTime | Date et heure du décès si la personne est décédée. |
| [!UICONTROL Genre] | `gender` | Chaîne | Identité de genre de la personne. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

## `communication` {#communication}

`communication` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure de communication](../../images/data-types/healthcare/person/communication.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Langue] | `language` | [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | La langue qui peut être utilisée pour communiquer avec la personne au sujet de sa santé. |
| [!UICONTROL Is Preferred Language] | `preferred` | Booléen | Indique si la langue est leur langue préférée ou non. |

## `link` {#link}

`link` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure de lien](../../images/data-types/healthcare/person/link.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Target] | `target` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | La ressource à laquelle cette personne est associée. |
| [!UICONTROL Assurance] | `assurance` | Chaîne | Niveau d’assurance associé au lien. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `level1` </li> <li> `level2` </li> <li> `level3` </li> <li> `level4` </li> |

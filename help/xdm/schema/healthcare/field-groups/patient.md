---
title: Groupe de champs de schéma patient
description: En savoir plus sur le groupe de champs de schéma Patient.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: eba7deb3-4785-4d05-86ef-0f6691fcd2c5
TQID: https://experienceleague.adobe.com/-gpIsx49AjgzLMvXTbNQzYvCtVqobsFm2hJnXscoQoc
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 541
ht-degree: 7%

---

# [!UICONTROL Patient] groupe de champs de schéma

[!UICONTROL Patient] groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md). Il fournit un `healthcarePatient` de champ de type objet unique qui recueille les données démographiques et d’autres détails administratifs sur une personne ou un animal recevant des soins ou d’autres services liés à la santé.

![Structure du groupe de champs](../../../images/healthcare/field-groups/patient/patient.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Address] | `address` | Tableau de [[!UICONTROL Address]](../data-types/address.md) | Informations sur l’adresse du patient. |
| [!UICONTROL Communication] | `communication` | Tableau d’objets | Un langage qui peut être utilisé pour communiquer avec le patient sur son état de santé. Pour plus d’informations, consultez la [section ci-dessous](#communication). |
| [!UICONTROL Patient Contacts] | `contact` | Tableau d’objets | Partie de contact du patient, tel qu&#39;un tuteur, un partenaire ou un ami. Pour plus d’informations, consultez la [section ci-dessous](#contact). |
| [!UICONTROL General Practitioner] | `generalPractioner` | Tableau de [[!UICONTROL Reference]](../data-types/reference.md) | Le principal prestataire de soins du patient. |
| [!UICONTROL Identifier] | `identifier` | Tableau de [[!UICONTROL Identifier]](../data-types/identifier.md) | Identifiant du patient. |
| [!UICONTROL Patient Link Details] | `link` | Tableau d’objets | Un lien vers la ressource d&#39;un patient ou d&#39;une personne apparentée qui concerne la même personne. Pour plus d’informations, consultez la [section ci-dessous](#link). |
| [!UICONTROL Managing Organization] | `managingOrganization` | [[!UICONTROL Reference]](../data-types/reference.md) | Organisation gardienne du dossier du patient. |
| [!UICONTROL Marital Status] | `maritalStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | État civil du patient. |
| [!UICONTROL Name] | `name` | Tableau de [[!UICONTROL Human name]](../data-types/human-name.md) | Nom associé au patient. |
| [!UICONTROL Contact Details] | `telecom` | Tableau de [[!UICONTROL Contact Point]](../data-types/contact-point.md) | Coordonnées, telles qu’un numéro de téléphone ou une adresse e-mail, permettant de contacter le patient. |
| [!UICONTROL Is Active] | `active` | Booléen | Indique si le dossier du patient est en cours d&#39;utilisation. |
| [!UICONTROL Birth Date] | `birthDate` | Date | Date de naissance du patient. |
| [!UICONTROL Deceased Indicator] | `deceasedBoolean` | Booléen | Indique si le patient est décédé ou non. |
| [!UICONTROL Deceased Date Time] | `deceasedDateTime` | DateTime | Date et heure du décès du patient. |
| [!UICONTROL Gender] | `gender` | Chaîne | Identité sexuelle de la personne. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |
| [!UICONTROL Is Part Of Multiple Birth] | `multipleBirthBoolean` | Booléen | Indique si le patient fait partie d’une grossesse multiple. |
| [!UICONTROL Birth Number] | `multipleBirthInteger` | Entier | Numéro de naissance dans la séquence. |

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.schema.json)

## `communication` {#communication}

`communication` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![ structure de communication ](../../../images/healthcare/field-groups/patient/communication.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Language] | `language` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Langue pouvant être utilisée pour communiquer avec la personne au sujet de sa santé. |
| [!UICONTROL Is Preferred Language] | `preferred` | Booléen | Indique si la langue est leur langue préférée ou non. |

## `contact` {#contact}

`contact` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![structure de contact](../../../images/healthcare/field-groups/patient/contact.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Contact Address] | `address` | [[!UICONTROL Address]](../data-types/address.md) | Adresse de la personne de contact. |
| [!UICONTROL Contact Name] | `name` | [[!UICONTROL Human Name]](../data-types/human-name.md) | Nom de la personne de contact. |
| [!UICONTROL Contact Organization] | `organization` | [[!UICONTROL Reference]](../data-types/reference.md) | Organisation associée à la personne de contact. |
| [!UICONTROL Contact Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Période au cours de laquelle le contact a été utilisé ou est en cours d’utilisation. |
| [!UICONTROL Relationship'] | `relationship` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | La relation entre le patient et la personne de contact. |
| [!UICONTROL Contact Details] | `telecom` | Tableau d’objets | Coordonnées de la personne de contact. Pour plus d’informations, consultez la [section ci-dessous](#telecom). |
| [!UICONTROL Gender] | `gender` | Chaîne | Identité sexuelle de la personne. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

### `telecom` {#telecom}

`telecom` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![structure télécom](../../../images/healthcare/field-groups/patient/telecom.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Contact Point] | `contactPoint` | [[!UICONTROL Contact point]](../data-types/contact-point.md) | Coordonnées de la personne. |

## `link` {#link}

`link` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![structure du lien](../../../images/healthcare/field-groups/patient/link.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Other] | `other` | [[!UICONTROL Reference]](../data-types/reference.md) | Un lien vers la ressource d&#39;un patient ou d&#39;une personne apparentée qui concerne la même personne. |
| [!UICONTROL Type] | `type` | Chaîne | Type de lien entre les deux ressources patient. |

---
title: Type de données des détails de contact étendu
description: Découvrez le type de données XDM (Extended Contact Detail Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4ac9b3d7-acc8-4a82-b34f-ec63a8bf12e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 8%

---

# Type de données [!UICONTROL Extended Contact Detail]

[!UICONTROL Extended Contact Detail] est un type de données standard Experience Data Model (XDM) qui décrit les informations d’un contact étendu. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données Détails du contact étendu](../../../images/healthcare/data-types/extended-contact-detail.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | [[!UICONTROL Adresse]](../data-types/address.md) | Adresse du contact. |
| [!UICONTROL Nom] | `name` | Tableau de [[!UICONTROL Nom de l’homme]](../data-types/human-name.md) | Nom de la ou des personnes à contacter. |
| [!UICONTROL Organisation] | `organization` | [[!UICONTROL Référence]](../data-types/reference.md) | L’organisation qui gère/surveille les détails du contact. |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../data-types/period.md) | La période pendant laquelle le contact est ou était valide pour l’utilisation. |
| [!UICONTROL Rôle] | `purpose` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Type de contact. |
| [!UICONTROL Telecom] | `telecom` | Tableau de [[!UICONTROL Point de contact]](../data-types/contact-point.md) | Les coordonnées. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)

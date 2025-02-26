---
title: Identifier le type de données
description: Découvrez le type de données Identifier le modèle de données d’expérience (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 0664f52d-bea6-4aa1-b2a5-de0bd6d5edd9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# Type de données [!UICONTROL Identifiant]

[!UICONTROL Identifiant] est un type de données XDM (Experience Data Model) standard qui fournit un identifiant destiné au calcul. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données d’identifiant](../../../images/healthcare/data-types/identifier.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../data-types/period.md) | La période pendant laquelle l’ID est ou a été valide pour utilisation. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Description de l’identifiant. |
| [!UICONTROL Assigner] | `assigner` | Chaîne | L’organisation qui a émis l’ID. |
| [!UICONTROL Système] | `system` | Chaîne | Espace de noms de la valeur de l’identifiant, représenté sous la forme d’un URI. |
| [!UICONTROL Utiliser] | `use` | Chaîne | L’utilisation de l’identifiant. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL Valeur] | `value` | Chaîne | La valeur unique de l’ID. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

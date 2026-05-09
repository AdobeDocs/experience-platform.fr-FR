---
title: Type de données d’identifiant
description: Découvrez le type de données Identifier le modèle de données d’expérience (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 0664f52d-bea6-4aa1-b2a5-de0bd6d5edd9
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 7%

---

# Type de données [!UICONTROL Identifier]

[!UICONTROL Identifier] est un type de données standard du modèle de données d’expérience (XDM) qui fournit un identifiant destiné au calcul. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de l’identifiant](../../../images/healthcare/data-types/identifier.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Période pendant laquelle l’ID est ou était valide pour être utilisé. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Description de l’identifiant. |
| [!UICONTROL Assigner] | `assigner` | Chaîne | Organisation qui a émis l’ID. |
| [!UICONTROL System] | `system` | Chaîne | Espace de noms de la valeur d’identifiant, représentée sous la forme d’un URI. |
| [!UICONTROL Use] | `use` | Chaîne | Utilisation de l’identifiant. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL Value] | `value` | Chaîne | Valeur unique de l’ID. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

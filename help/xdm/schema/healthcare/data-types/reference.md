---
title: Type de données de référence
description: Découvrez le type de données Modèle de données d’expérience de référence (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: eb724dbb-2918-43b5-8e50-c8aabfe6e96c
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 8%

---

# Type de données [!UICONTROL Reference]

[!UICONTROL Reference] est un type de données standard du modèle de données d’expérience (XDM) qui fournit une référence d’une ressource à une autre. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de référence](../../../images/healthcare/data-types/reference.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Identifier] | `identifier` | [[!UICONTROL Identifier]](../data-types/identifier.md) | La référence logique lorsque la référence littérale est inconnue. |
| [!UICONTROL Display] | `display` | Chaîne | Texte secondaire de la référence. |
| [!UICONTROL Reference] | `reference` | Chaîne | Référence littérale, relative, interne ou URL absolue. |
| [!UICONTROL Type] | `type` | Chaîne | Type auquel la référence fait référence, représenté sous la forme d’un URI. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)

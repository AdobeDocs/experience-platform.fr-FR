---
title: Type de données de référence codable
description: Découvrez le type de données du modèle de données d’expérience de référence codable (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# Type de données [!UICONTROL Codeable Reference]

[!UICONTROL Codeable Reference] est un type de données standard du modèle de données d’expérience (XDM) qui décrit une référence à une ressource ou à un concept. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure de type de données de référence codable](../../../images/healthcare/data-types/codeable-reference.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Concept] | `concept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Référence à un concept (par classe). |
| [!UICONTROL Reference] | `reference` | [[!UICONTROL Reference]](../data-types/reference.md) | Référence à une ressource. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)

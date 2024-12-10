---
title: Type de données de référence codeable
description: Découvrez le type de données XDM (Codeable Reference Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# [!UICONTROL Référence codeable] type de données

[!UICONTROL Référence codeable] est un type de données XDM (Experience Data Model) standard qui décrit une référence à une ressource ou à un concept. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de référence codeable](../../../images/healthcare/data-types/codeable-reference.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Concept] | `concept` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Référence à un concept (par classe). |
| [!UICONTROL Référence] | `reference` | [[!UICONTROL Référence]](../data-types/reference.md) | Référence à une ressource. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)

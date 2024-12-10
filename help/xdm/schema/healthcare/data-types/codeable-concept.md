---
title: Type de données de concept codé
description: Découvrez le type de données XDM (Codeable Concept Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# Type de données [!UICONTROL Codeable Concept]

[!UICONTROL Concept codeable] est un type de données XDM (Experience Data Model) standard qui décrit une référence d’une ressource à une autre. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données Concept codeable](../../../images/healthcare/data-types/codeable-concept.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Coding] | `coding` | Tableau de [[!UICONTROL Coding]](../data-types/coding.md) | Code défini par un système terminologique. |
| [!UICONTROL Texte] | `text` | Chaîne | Représentation en texte brut du concept. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)

---
title: Type De Données De Concept Codable
description: Découvrez le type de données du modèle de données d’expérience (XDM) Codable Concept.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 7%

---

# Type de données [!UICONTROL Codeable Concept]

[!UICONTROL Codeable Concept] est un type de données standard du modèle de données d’expérience (XDM) qui décrit une référence d’une ressource à une autre. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure de type de données Concept codable](../../../images/healthcare/data-types/codeable-concept.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Coding] | `coding` | Tableau de [[!UICONTROL Coding]](../data-types/coding.md) | Code défini par un système terminologique. |
| [!UICONTROL Text] | `text` | Chaîne | Représentation en texte brut du concept. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)

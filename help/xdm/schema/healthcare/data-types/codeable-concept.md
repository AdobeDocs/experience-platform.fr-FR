---
title: Type De Données De Concept Codable
description: Découvrez le type de données du modèle de données d’expérience (XDM) Codable Concept.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
TQID: https://experienceleague.adobe.com/NGQ1TQA12L3DILwGzF5vTd9tCcdkuvsV-rkyQwVZ4JU
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 127
ht-degree: 7%

---

# Type de données [!UICONTROL Concept codable]

[!UICONTROL Concept codable] est un type de données standard des modèles de données d’expérience (XDM) qui décrit une référence d’une ressource à une autre. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure de type de données Concept codable](../../../images/healthcare/data-types/codeable-concept.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Codage] | `coding` | Tableau de [[!UICONTROL codage]](../data-types/coding.md) | Code défini par un système terminologique. |
| [!UICONTROL Texte] | `text` | Chaîne | Représentation en texte brut du concept. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)

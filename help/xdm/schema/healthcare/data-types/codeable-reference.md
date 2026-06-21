---
title: Type de données de référence codable
description: Découvrez le type de données du modèle de données d’expérience de référence codable (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
TQID: https://experienceleague.adobe.com/ClRmOQ-uJWM0p3tiTtL8npCbgkY0O3p9q99nSkREsic
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 126
ht-degree: 6%

---

# [!UICONTROL Référence codable] type de données

[!UICONTROL Référence codable] est un type de données standard du modèle de données d’expérience (XDM) qui décrit une référence à une ressource ou à un concept. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure de type de données de référence codable](../../../images/healthcare/data-types/codeable-reference.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Concept] | `concept` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Référence à un concept (par classe). |
| [!UICONTROL Référence] | `reference` | [[!UICONTROL Référence]](../data-types/reference.md) | Référence à une ressource. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)

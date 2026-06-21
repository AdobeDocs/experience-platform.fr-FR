---
title: Type de données de minutage
description: Découvrez le type de données Modèle de données d’expérience de minutage (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
TQID: https://experienceleague.adobe.com/dQjdUh7cZkhp0mKxO1xqMqYJJCWMnNeN5q-6MZOIIIk
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 135
ht-degree: 7%

---

# Type de données [!UICONTROL Timing]

[!UICONTROL Minutage] est un type de données standard du modèle de données d’expérience (XDM) qui décrit un planning qui fournit des informations sur un événement qui peut se produire plusieurs fois. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de minutage](../../../images/healthcare/data-types/timing.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Événement] | `event` | Tableau de date et heure | Lorsque l’événement se produit. |
| [!UICONTROL Répéter] | `repeat` | [[!UICONTROL Répéter]](../data-types/repeat.md) | Informations sur le moment où l’événement se produit. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Le code relatif à l’événement. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)

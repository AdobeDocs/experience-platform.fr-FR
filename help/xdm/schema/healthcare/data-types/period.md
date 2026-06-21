---
title: Type de données de période
description: Découvrez le type de données du modèle de données d’expérience de la période (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
TQID: https://experienceleague.adobe.com/JW-PbFNMBjczn0Dk2-FnlM1-qUjFfzZO7Wpdd0fdG34
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 121
ht-degree: 9%

---

# [!UICONTROL Période] type de données

[!UICONTROL Période] est un type de données standard du modèle de données d’expérience (XDM) qui fournit une période définie par une date/heure de début et de fin. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de la période](../../../images/healthcare/data-types/period.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Fin] | `end` | DateTime | Date et heure de fin. |
| [!UICONTROL Début] | `start` | DateTime | Date et heure de début. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)

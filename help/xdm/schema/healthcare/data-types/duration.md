---
title: Type de données de durée
description: Découvrez le type de données du modèle de données d’expérience (XDM) de durée.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 01aac0d0-0503-4f8b-a306-cf3c187a76e0
TQID: https://experienceleague.adobe.com/l7GgwGWnX9-t7-WzVtiBkIDsFoV3cUAmAZ-nZse0LIw
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 176
ht-degree: 7%

---

# [!UICONTROL Durée] type de données

[!UICONTROL Durée] est un type de données standard des modèles de données d’expérience (XDM) qui décrit une durée. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de durée](../../../images/healthcare/data-types/duration.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Forme codée de l’unité de temps. |
| [!UICONTROL Système] | `system` | Chaîne | Système qui décrit l’unité codée, représentée sous la forme d’un URI. |
| [!UICONTROL Unité] | `unit` | Chaîne | Unité de temps représentée en millisecondes, secondes, minutes, heures, jours, semaines, mois ou années. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `ms` (ms) </li> <li> `s` (secondes) </li> <li> `min` (minutes) </li> <li> `h` (heures) </li>  <li> `d` (jours) </li> <li> `wk` (semaines) </li> <li> `mo` (mois) </li> <li> `a` (années) </li> |
| [!UICONTROL Valeur] | `value` | Double | Valeur numérique pour l’unité de temps. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)

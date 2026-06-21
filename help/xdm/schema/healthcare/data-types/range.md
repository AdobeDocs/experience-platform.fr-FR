---
title: Type de données de plage
description: Découvrez le type de données Modèle de données d’expérience de plage (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 66f8b574-04d9-435f-8743-4ff89c4c0079
TQID: https://experienceleague.adobe.com/wBFhJ7IX7jlGNWui41-hD6eNRcwQK0cwZghxV9dlWnQ
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 118
ht-degree: 6%

---

# [!UICONTROL Plage] type de données

[!UICONTROL Plage] est un type de données standard du modèle de données d’expérience (XDM) qui fournit un ensemble de valeurs liées par des valeurs faibles et élevées. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de plage](../../../images/healthcare/data-types/range.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Élevé] | `high` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | La limite la plus élevée. |
| [!UICONTROL Faible] | `low` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | La limite la plus basse. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)

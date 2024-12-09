---
title: Type de données de plage
description: Découvrez le type de données du modèle de données d’expérience de plage (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 8%

---

# Type de données [!UICONTROL Range]

[!UICONTROL Range] est un type de données XDM (Experience Data Model) standard qui fournit un ensemble de valeurs liées par des valeurs faibles et élevées. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de plage](../../images/data-types/healthcare/range.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL High] | `high` | [[!UICONTROL Quantité simple]](../healthcare/simple-quantity.md) | Limite la plus élevée. |
| [!UICONTROL Low] | `low` | [[!UICONTROL Quantité simple]](../healthcare/simple-quantity.md) | Limite la plus basse. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)

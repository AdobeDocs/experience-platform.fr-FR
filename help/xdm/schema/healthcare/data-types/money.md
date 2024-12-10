---
title: Type de données Money
description: Découvrez le type de données Money Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b910a45-01d5-404b-9710-a2fad9885452
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 18%

---

# Type de données [!UICONTROL Money]

[!UICONTROL Money] est un type de données XDM (Experience Data Model) standard qui fournit une quantité d’utilité économique dans une devise reconnue. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données Money](../../../images/healthcare/data-types/money.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Devise] | `currency` | Chaîne | Code de devise ISO 4217. |
| [!UICONTROL Valeur] | `value` | Double | Valeur numérique. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)

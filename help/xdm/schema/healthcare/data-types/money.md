---
title: Type de données Money
description: Découvrez le type de données Modèle de données d’expérience monétaire (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 8b910a45-01d5-404b-9710-a2fad9885452
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 8%

---

# Type de données [!UICONTROL Money]

[!UICONTROL Money] est un type de données XDM (Modèle de données d’expérience) standard qui fournit une quantité d’utilité économique dans une devise reconnue. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données Money](../../../images/healthcare/data-types/money.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Currency] | `currency` | Chaîne | Code de devise ISO 4217. |
| [!UICONTROL Value] | `value` | Double | Valeur numérique. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)

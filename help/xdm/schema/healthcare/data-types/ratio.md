---
title: Type de données de ratio
description: Découvrez le type de données du modèle de données d’expérience de ratio (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# Type de données [!UICONTROL Ratio]

[!UICONTROL Ratio] est un type de données XDM (Experience Data Model) standard qui fournit un ratio de deux valeurs [[!UICONTROL Quantity]](../data-types/quantity.md) par le biais d’un numérateur et d’un dénominateur. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de ratio](../../../images/healthcare/data-types/ratio.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Denominator] | `denominator` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | La valeur du dénominateur. |
| [!UICONTROL Numérateur] | `numerator` | [[!UICONTROL Quantity]](../data-types/quantity.md) | La valeur du numérateur. |

>[!NOTE]
>
> Les `denominator` et `numerator` ont des types de données différents en raison de la spécification créée conformément à la version 5 de HL7 FHIR.

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)

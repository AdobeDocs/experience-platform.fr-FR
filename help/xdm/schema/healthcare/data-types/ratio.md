---
title: Type de données de rapport
description: Découvrez le type de données du modèle de données d’expérience sur les rapports (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# Type de données [!UICONTROL Ratio]

[!UICONTROL Ratio] est un type de données standard du modèle de données d’expérience (XDM) qui fournit un rapport de deux valeurs [[!UICONTROL Quantity]](../data-types/quantity.md) par le biais d’un numérateur et d’un dénominateur. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de rapport](../../../images/healthcare/data-types/ratio.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Denominator] | `denominator` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | Valeur du dénominateur. |
| [!UICONTROL Numerator] | `numerator` | [[!UICONTROL Quantity]](../data-types/quantity.md) | Valeur du numérateur. |

>[!NOTE]
>
> Les `denominator` et `numerator` ont des types de données différents en raison de la spécification créée conformément à la version 5 du FHIR HL7.

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)

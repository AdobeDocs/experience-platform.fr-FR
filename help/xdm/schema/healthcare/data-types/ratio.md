---
title: Type de données de rapport
description: Découvrez le type de données du modèle de données d’expérience sur les rapports (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
TQID: https://experienceleague.adobe.com/23kAL-Qjyp4NGy-HPUhoNwv--dX1O3NHn9h8B9VHuFI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 5%

---

# Type de données [!UICONTROL Ratio]

[!UICONTROL Rapport] est un type de données standard du modèle de données d’expérience (XDM) qui fournit un rapport de deux valeurs [[!UICONTROL Quantité]](../data-types/quantity.md) via un numérateur et un dénominateur. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de rapport](../../../images/healthcare/data-types/ratio.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Dénominateur] | `denominator` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | Valeur du dénominateur. |
| [!UICONTROL Numérateur] | `numerator` | [[!UICONTROL Quantité]](../data-types/quantity.md) | Valeur du numérateur. |

>[!NOTE]
>
> Les `denominator` et `numerator` ont des types de données différents en raison de la spécification créée conformément à la version 5 du FHIR HL7.

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)

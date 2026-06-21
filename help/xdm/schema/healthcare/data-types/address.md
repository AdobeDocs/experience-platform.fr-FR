---
title: Type de données d’adresse
description: Découvrez le type de données Modèle de données d’expérience de l’adresse (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 21213bd5-00f4-43cc-80cf-2c0dcf878a23
TQID: https://experienceleague.adobe.com/rlqSPpf27sfe7TyO7UsCmqjstZ0Mz47uR5qoG2wmf4g
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 8%

---

# Type de données [!UICONTROL Address]

[!UICONTROL Adresse] est un type de données standard du modèle de données d’expérience (XDM) qui décrit une adresse exprimée à l’aide de conventions postales (par opposition au GPS ou à d’autres formats de définition d’emplacement). Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de l’adresse](../../../images/healthcare/data-types/address.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../data-types/period.md) | Période au cours de laquelle l’adresse a été/est utilisée. |
| [!UICONTROL Ville] | `city` | Chaîne | Nom de la ville. |
| [!UICONTROL Pays] | `country` | Chaîne | Code pays décrit dans la norme internationale ISO 3166. Le code peut être alpha-2 ou alpha-3. |
| [!UICONTROL District] | `district` | Chaîne | Nom du district. |
| [!UICONTROL Line] | `line` | Chaîne | Nom, numéro, direction, case postale ou équivalent de la rue. |
| [!UICONTROL Code postal] | `postalCode` | Chaîne | Code postal. |
| [!UICONTROL État] | `state` | Chaîne | Sous-unité d’un pays. Les abréviations sont acceptables. |
| [!UICONTROL Texte] | `text` | Chaîne | Représentation textuelle de l’adresse. |
| [!UICONTROL Type] | `type` | Chaîne | Type d’adresse. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL Utiliser] | `use` | Chaîne | Objet de l’adresse. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)

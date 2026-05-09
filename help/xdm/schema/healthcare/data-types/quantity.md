---
title: Type de données de quantité
description: Découvrez le type de données du modèle de données d’expérience Quantity (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 881fe8a4-0253-4b75-9833-b97bb50cc87e
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 8%

---

# Type de données [!UICONTROL Quantity]

[!UICONTROL Quantity] est un type de données standard du modèle de données d’expérience (XDM) qui fournit une quantité mesurée ou mesurable. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données Quantité](../../../images/healthcare/data-types/quantity.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Forme codée de l’unité. |
| [!UICONTROL Comparator] | `comparator` | Chaîne | Opérateur de comparaison. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL System] | `system` | Chaîne | Système qui définit le formulaire unitaire codé, représenté sous la forme d’un URI. |
| [!UICONTROL Unit] | `unit` | Chaîne | Représentation de l’unité. |
| [!UICONTROL Value] | `value` | Double | Valeur numérique. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)

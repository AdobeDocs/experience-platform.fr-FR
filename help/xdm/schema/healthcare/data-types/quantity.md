---
title: Type de données de quantité
description: Découvrez le type de données du modèle de données d’expérience Quantity (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 881fe8a4-0253-4b75-9833-b97bb50cc87e
TQID: https://experienceleague.adobe.com/BVN3txQTtu8hga-gsZzWYKWt3FUFvsQLWxcptLTCwus
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 154
ht-degree: 9%

---

# Type de données [!UICONTROL Quantité]

[!UICONTROL Quantité] est un type de données standard du modèle de données d’expérience (XDM) qui fournit une quantité mesurée ou mesurable. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données Quantité](../../../images/healthcare/data-types/quantity.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Forme codée de l’unité. |
| [!UICONTROL Comparateur] | `comparator` | Chaîne | Opérateur de comparaison. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL Système] | `system` | Chaîne | Système qui définit le formulaire unitaire codé, représenté sous la forme d’un URI. |
| [!UICONTROL Unité] | `unit` | Chaîne | Représentation de l’unité. |
| [!UICONTROL Valeur] | `value` | Double | Valeur numérique. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)

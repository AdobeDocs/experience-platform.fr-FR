---
title: Type de données Quantité simple
description: Découvrez le type de données du modèle de données d’expérience (XDM) Quantité simple.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 92d3d6a8-1d0f-43a4-a93f-8df79605c4e6
TQID: https://experienceleague.adobe.com/zmB81Wk3qkrFy3pHXKJtviQuNEvtbTLTsN0m9EDWpaY
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 139
ht-degree: 10%

---

# Type de données [!UICONTROL Quantité simple]

[!UICONTROL  Quantité simple ] est un type de données standard du modèle de données d’expérience (XDM) qui fournit une quantité mesurée ou mesurable. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure de type de données Quantité simple](../../../images/healthcare/data-types/simple-quantity.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Forme codée de l’unité. |
| [!UICONTROL Système] | `system` | Chaîne | Système qui définit le formulaire unitaire codé, représenté sous la forme d’un URI. |
| [!UICONTROL Unité] | `unit` | Chaîne | Représentation de l’unité. |
| [!UICONTROL Valeur] | `value` | Double | Valeur numérique. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)

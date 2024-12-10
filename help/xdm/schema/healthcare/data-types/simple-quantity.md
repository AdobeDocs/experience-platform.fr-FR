---
title: Type de données Quantité simple
description: Découvrez le type de données XDM (Simple Quantity Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 92d3d6a8-1d0f-43a4-a93f-8df79605c4e6
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---

# Type de données [!UICONTROL Quantité simple]

[!UICONTROL Quantité simple] est un type de données XDM (Experience Data Model) standard qui fournit une quantité mesurée ou mesurable. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données Quantité simple](../../../images/healthcare/data-types/simple-quantity.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Forme codée de l’unité. |
| [!UICONTROL Système] | `system` | Chaîne | Système qui définit un formulaire unitaire codé, représenté sous la forme d’un URI. |
| [!UICONTROL Unit] | `unit` | Chaîne | Représentation de l’unité. |
| [!UICONTROL Valeur] | `value` | Double | Valeur numérique. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)

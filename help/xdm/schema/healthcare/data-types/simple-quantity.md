---
title: Type de données Quantité simple
description: Découvrez le type de données du modèle de données d’expérience (XDM) Quantité simple.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 92d3d6a8-1d0f-43a4-a93f-8df79605c4e6
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 9%

---

# Type de données [!UICONTROL Simple Quantity]

[!UICONTROL Simple Quantity] est un type de données standard du modèle de données d’expérience (XDM) qui fournit une quantité mesurée ou mesurable. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure de type de données Quantité simple](../../../images/healthcare/data-types/simple-quantity.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Forme codée de l’unité. |
| [!UICONTROL System] | `system` | Chaîne | Système qui définit le formulaire unitaire codé, représenté sous la forme d’un URI. |
| [!UICONTROL Unit] | `unit` | Chaîne | Représentation de l’unité. |
| [!UICONTROL Value] | `value` | Double | Valeur numérique. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)

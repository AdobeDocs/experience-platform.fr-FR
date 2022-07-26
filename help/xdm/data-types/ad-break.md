---
title: Type de données de coupure publicitaire
description: Ce document présente un aperçu du type de données XDM (Ad break Experience Data Model).
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 17%

---

# [!UICONTROL Coupure publicitaire] type de données

[!UICONTROL Coupure publicitaire] est un type de données XDM (Experience Data Model) standard qui décrit la manière dont une publicité minutée est insérée dans un élément multimédia minuté.

![Structure du type de données](../images/data-types/ad-break.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc.title` | Chaîne | Nom convivial de la coupure publicitaire. |
| `_id` | Chaîne | Identifiant unique de la coupure publicitaire. |
| `offset` | Nombre entier | Décalage, en secondes, de la coupure publicitaire à partir du début du contenu Principal. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)

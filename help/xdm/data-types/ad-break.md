---
title: Type de données de coupure publicitaire
description: Ce document présente un aperçu du type de données XDM (Ad break Experience Data Model).
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
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

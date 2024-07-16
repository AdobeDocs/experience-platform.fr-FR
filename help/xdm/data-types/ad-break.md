---
title: Type de données de coupure publicitaire
description: Découvrez le type de données du modèle de données d’expérience (XDM) de coupure publicitaire.
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 21%

---

# Type de données [!UICONTROL coupure publicitaire]

[!UICONTROL Saut de publicité] est un type de données XDM (Experience Data Model) standard qui décrit la manière dont une publicité minutée est insérée dans un élément multimédia minuté.

![Structure de type de données](../images/data-types/ad-break.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc.title` | Chaîne | Nom convivial de la coupure publicitaire. |
| `_id` | Chaîne | Identifiant unique de la coupure publicitaire. |
| `offset` | Nombre entier | Décalage, en secondes, de la coupure publicitaire par rapport au début du contenu principal. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)

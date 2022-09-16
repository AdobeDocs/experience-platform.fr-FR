---
title: Type de données Impressions
description: Ce document fournit un aperçu du type de données XDM Impressions.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 7%

---

# [!UICONTROL Impressions] type de données

[!UICONTROL Impressions] est un type de données XDM standard qui décrit une impression marketing, qui est une mesure utilisée pour quantifier le nombre d’affichages ou d’engagements numériques pour un élément de contenu tel qu’une publicité, une publication numérique ou une page web.

![](../images/data-types/impressions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `ID` | Chaîne | Identifiant unique de l’impression. |
| `displays` | Nombre entier | Nombre de fois où l’élément d’impression a été affiché pour un client. |
| `selected` | Nombre entier | Nombre de fois où l’élément d’impression a été sélectionné ou a fait l’objet d’un clic. |
| `type` | Chaîne | Type d’impression. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)

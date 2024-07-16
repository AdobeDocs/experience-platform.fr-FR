---
title: Type de données d’impression
description: Découvrez le type de données XDM Impressions.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 6%

---

# Type de données [!UICONTROL Impressions]

[!UICONTROL Impressions] est un type de données XDM standard qui décrit une impression marketing, qui est une mesure utilisée pour quantifier le nombre d’affichages ou d’engagements numériques pour un élément de contenu tel qu’une publicité, une publication numérique ou une page web.

![](../images/data-types/impressions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `ID` | Chaîne | Identifiant unique de l’impression. |
| `displays` | Nombre entier | Nombre de fois où l’élément d’impression a été affiché pour un client. |
| `selected` | Nombre entier | Nombre de fois où l’élément d’impression a été sélectionné ou a fait l’objet d’un clic. |
| `type` | Chaîne | Type d’impression. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)

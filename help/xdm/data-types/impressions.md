---
title: Type de données d’impressions
description: Découvrez le type de données XDM Impressions.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
TQID: https://experienceleague.adobe.com/W5OxAJdDaOnGBkgLxT1t0gN98PgpUBpH9faLO-WpCZc
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 135
ht-degree: 5%

---

# Type de données [!UICONTROL Impressions]

[!UICONTROL Impressions] est un type de données XDM standard qui décrit une impression marketing, qui est une mesure utilisée pour quantifier le nombre de vues ou d’engagements numériques pour un élément de contenu tel qu’une publicité, une publication numérique ou une page web.

![](../images/data-types/impressions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `ID` | Chaîne | ID unique de l’impression. |
| `displays` | Entier | Nombre de fois où l’élément d’impression a été affiché pour un client. |
| `selected` | Entier | Nombre de fois où l’élément d’impression a été sélectionné. |
| `type` | Chaîne | Type d’impression. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)

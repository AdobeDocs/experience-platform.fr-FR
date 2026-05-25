---
title: Type de données de panier
description: Découvrez le type de données du modèle de données d’expérience du panier (XDM).
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
TQID: https://experienceleague.adobe.com/nLecQnTD7NRmR4pWkqqPJM0GuJWrhqPzA9P3geuVgTc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 129
ht-degree: 13%

---

# Type de données [!UICONTROL Cart]

[!UICONTROL Cart] est un type de données standard du modèle de données d’expérience (XDM) qui fournit des propriétés liées à un panier. Utilisez ce type de données pour capturer l’identifiant unique attribué par le vendeur (`Cart ID`) et la source (`Cart Source`) dans laquelle un ou plusieurs produits ont été ajoutés au panier.

![Diagramme du type de données [!UICONTROL Cart].](../images/data-types/cart.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL Cart ID] | `cartID` | chaîne | Identifiant unique attribué au panier par le vendeur. |
| [!UICONTROL Cart Source] | `cartSource` | chaîne | Emplacement d’où un ou plusieurs produits ont été ajoutés au panier. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)

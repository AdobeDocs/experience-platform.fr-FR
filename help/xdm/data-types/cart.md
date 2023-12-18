---
title: Type de données du panier
description: Découvrez le type de données Modèle de données d’expérience du panier (XDM).
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 7%

---

# [!UICONTROL Panier] type de données

[!UICONTROL Panier] est un type de données XDM (Experience Data Model) standard qui fournit des propriétés liées à un panier. Utilisez ce type de données pour capturer l’identifiant unique attribué par le vendeur (`Cart ID`) et la source (`Cart Source`) où un ou plusieurs produits ont été ajoutés au panier.

![Un diagramme de [!UICONTROL Panier] type de données.](../images/data-types/cart.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL Identifiant du panier] | `cartID` | chaîne | Identifiant unique attribué par le vendeur au panier. |
| [!UICONTROL Source du panier] | `cartSource` | chaîne | À partir duquel un ou plusieurs produits ont été ajoutés au panier. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)

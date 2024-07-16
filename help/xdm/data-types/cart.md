---
title: Type de données du panier
description: Découvrez le type de données Modèle de données d’expérience du panier (XDM).
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 15%

---

# Type de données [!UICONTROL Panier]

[!UICONTROL Panier] est un type de données XDM (Experience Data Model) standard qui fournit des propriétés liées à un panier. Utilisez ce type de données pour capturer l’identifiant unique attribué par le vendeur (`Cart ID`) et la source (`Cart Source`) où un ou plusieurs produits ont été ajoutés au panier.

![Schéma du type de données [!UICONTROL Cart].](../images/data-types/cart.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL ID de panier] | `cartID` | Chaîne | Identifiant unique attribué au panier par le vendeur. |
| [!UICONTROL Source de panier] | `cartSource` | Chaîne | À partir duquel un ou plusieurs produits ont été ajoutés au panier. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)

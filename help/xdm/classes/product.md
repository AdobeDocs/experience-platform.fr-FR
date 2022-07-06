---
title: Classe de produits
description: Ce document présente la classe Product dans le modèle de données d’expérience (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 21%

---

# [!UICONTROL Produit] class

Dans le modèle de données d’expérience (XDM), la variable [!UICONTROL Produit] capture l’ensemble minimal de propriétés qui définissent un produit de vente au détail.

![](../images/classes/product.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `productListPrice` | [Devise](../data-types/currency.md) | Décrit le prix par défaut du produit avant les ventes et les remises. |
| `_id` | Chaîne | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `productDescription` | Chaîne | Description du produit. |
| `productID` | Chaîne | Identifiant unique du produit. |
| `productLastModifiedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) date et heure de la dernière modification de ce produit pour toutes les mises à jour. |
| `productManufacturedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) date et heure de la création de ce produit. |
| `productName` | Chaîne | Nom du produit. |
| `productRating` | Chaîne | Évaluation de la révision par le client du produit. |

{style=&quot;table-layout:auto&quot;}

## Groupes de champs compatibles {#field-groups}

Adobe fournit plusieurs groupes de champs standard à utiliser avec le [!UICONTROL Produit] classe . Voici une liste de groupes de champs couramment utilisés pour la classe :

* [[!UICONTROL Catalogue de produits]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Catégorie de produits]](../field-groups/product/product-category.md)

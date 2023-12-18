---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;adresse;xdm:address;datatype;type de données;type de données;
solution: Experience Platform
title: Type de données d’élément de liste de produits
description: Découvrez le type de données XDM de l’élément de liste de produits.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 7%

---

# [!UICONTROL Élément de liste de produits] type de données

[!UICONTROL Élément de liste de produits] est un type de données XDM standard qui décrit un produit sélectionné par un client avec des options, des tarifs et un contexte d’utilisation spécifiques pour un moment spécifique.

Les valeurs capturées dans ce type de données peuvent différer de l’enregistrement du produit. Par exemple, l’enregistrement de produit contient des détails du système d’informations sur les produits qui sont cohérents pour tous les clients, où l’article de liste de produits présente le prix réel offert au client au moment de l’achat, qui peut varier en raison des campagnes de vente ou des prix saisonniers.

![](../images/data-types/product-list-item.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `selectedOptions` | Tableau d’objets | Contient les options personnalisées sélectionnées pour un produit configurable. Chaque élément de liste est un objet avec les propriétés suivantes :<ul><li>`attribute`: nom de l’attribut configurable.</li><li>`value`: valeur de l’attribut .</li></ul> |
| `SKU` | [!UICONTROL Chaîne] | Unité de gestion des stocks (SKU), l’identifiant unique d’un produit défini par le fournisseur. |
| `_id` | [!UICONTROL Chaîne] | Identifiant de l’élément de ligne pour cette entrée de produit. Le produit lui-même est identifié via `product`. |
| `currencyCode` | [!UICONTROL Chaîne] | La variable [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) code de devise alphabétique utilisé pour évaluer le produit. |
| `discountAmount` | [!UICONTROL Double] | Si le produit est actualisé, cela représente la différence entre le prix normal et le prix spécial du produit. |
| `name` | [!UICONTROL Chaîne] | Nom d’affichage du produit tel qu’il est présenté à l’utilisateur pour cette consultation de produit. |
| `priceTotal` | [!UICONTROL Double] | Prix total de l’article de ligne de produit. |
| `product` | [!UICONTROL Chaîne] (URI) | L’URI `$id` du schéma XDM qui capture le produit lui-même. |
| `productAddMethod` | [!UICONTROL Chaîne] | Méthode utilisée par le visiteur pour ajouter un élément de produit à la liste. |
| `productImageUrl` | [!UICONTROL Chaîne] | URL de l’image principale du produit. |
| `quantity` | [!UICONTROL Entier] | Nombre d’unités du produit que le client a indiqué. |
| `unitOfMeasureCode` | [!UICONTROL Chaîne] | Le standard [code unité de mesure](https://ucum.org/ucum) pour le produit, en fonction de la variable `quantity` . |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données des adresses postales, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)

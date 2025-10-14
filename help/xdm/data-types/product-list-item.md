---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;adresse;xdm:address;datatype;type de données;type de données;
solution: Experience Platform
title: Type de données d’élément de liste de produits
description: Découvrez le type de données XDM de l’élément de liste de produits.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: ba6c6eb2c6b0fc1dfc4e7440fd16a85bc7b46457
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 21%

---

# Type de données [!UICONTROL Product list item]

[!UICONTROL Product list item] est un type de données XDM standard qui décrit un produit sélectionné par un client avec des options, une tarification et un contexte d’utilisation spécifiques pour un moment spécifique.

Les valeurs capturées dans ce type de données peuvent différer de l’enregistrement du produit. Par exemple, l’enregistrement de produit contient des détails du système d’informations sur les produits qui sont cohérents pour tous les clients, où l’article de liste de produits présente le prix réel offert au client au moment de l’achat, qui peut varier en raison des campagnes de vente ou des prix saisonniers.

![](../images/data-types/product-list-item.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `selectedOptions` | Tableau d’objets | Contient les options personnalisées sélectionnées pour un produit configurable. Chaque élément de liste est un objet avec les propriétés suivantes :<ul><li>`attribute` : nom de l’attribut configurable.</li><li>`value` : valeur de l’attribut.</li></ul> |
| `SKU` | [!UICONTROL Chaîne] | Unité de stock (SKU), identifiant unique d’un produit défini par le vendeur. |
| `_id` | [!UICONTROL Chaîne] | Identifiant de l’élément de ligne pour cette entrée de produit. Le produit lui-même est identifié via `product`. |
| `currencyCode` | [!UICONTROL Chaîne] | Code de devise alphabétique [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) utilisé pour évaluer le produit. |
| `discountAmount` | [!UICONTROL Double] | Si le produit est actualisé, cela représente la différence entre le prix normal et le prix spécial du produit. |
| `name` | [!UICONTROL Chaîne] | Nom d’affichage du produit tel qu’il est présenté à l’utilisateur pour cette vue. |
| `priceTotal` | [!UICONTROL Double] | Prix total de l’élément de ligne du produit. |
| `product` | [!UICONTROL String] (URI) | Identifiant XDM du produit lui-même. |
| `productAddMethod` | [!UICONTROL Chaîne] | Méthode utilisée par le visiteur pour ajouter un élément de produit à la liste. |
| `productImageUrl` | [!UICONTROL Chaîne] | URL de l’image principale du produit. |
| `quantity` | [!UICONTROL Entier] | Nombre d’unités du produit que le client a indiqué. |
| `unitOfMeasureCode` | [!UICONTROL Chaîne] | Le [code d’unité de mesure &#x200B;](https://ucum.org/ucum) standard pour le produit en rapport avec la propriété `quantity`. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données des adresses postales, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)

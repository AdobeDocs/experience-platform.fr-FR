---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;adresse;xdm:address;datatype;type de données;type de données;
solution: Experience Platform
title: Type de données d’élément de liste de produits
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM de l’élément de liste de produits.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 17%

---

# [!UICONTROL Élément de liste de produits] type de données

[!UICONTROL Élément de liste de produits] est un type de données XDM standard qui décrit un produit sélectionné par un client avec des options, des tarifs et un contexte d’utilisation spécifiques pour un moment spécifique.

Les valeurs capturées dans ce type de données peuvent différer de l’enregistrement du produit. Par exemple, l’enregistrement de produit contient des détails du système d’informations sur les produits qui sont cohérents pour tous les clients, où l’article de liste de produits présente le prix réel offert au client au moment de l’achat, qui peut varier en raison des campagnes de vente ou des prix saisonniers.

![](../images/data-types/product-list-item.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `SKU` | [!UICONTROL Chaîne] | Unité de gestion des stocks (SKU), l’identifiant unique d’un produit défini par le fournisseur. |
| `_id` | [!UICONTROL Chaîne] | Identifiant de l’élément de ligne pour cette entrée de produit. Le produit lui-même est identifié via `product`. |
| `currencyCode` | [!UICONTROL Chaîne] | Le [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) code de devise alphabétique utilisé pour évaluer le produit. |
| `name` | [!UICONTROL Chaîne] | Nom d’affichage du produit tel qu’il est présenté à l’utilisateur pour cette consultation de produit. |
| `priceTotal` | [!UICONTROL Double] | Prix total de l’article de ligne de produit. |
| `product` | [!UICONTROL Chaîne] (URI) | L’URI `$id` du schéma XDM qui capture le produit lui-même. |
| `productAddMethod` | [!UICONTROL Chaîne] | Méthode utilisée par le visiteur pour ajouter un produit à la liste. |
| `quantity` | [!UICONTROL Nombre entier] | Nombre d’unités du produit que le client a indiqué. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données des adresses postales, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)

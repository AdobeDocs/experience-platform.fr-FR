---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;commerce;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Commerce
description: Ce document fournit un aperçu du type de données XDM (Commerce Experience Data Model).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 16%

---

# [!UICONTROL Commerce] type de données

[!UICONTROL Commerce] est un type de données XDM (Experience Data Model) standard qui décrit les enregistrements liés aux activités d’achat et de vente.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `order` | [[!UICONTROL Commande]](./order.md) | Décrit la commande passée pour un ou plusieurs produits. |
| `cartAbandons` | [[!UICONTROL Mesure]](./measure.md) | Utilisé pour décrire lorsqu’une liste de produits a été identifiée comme n’étant plus accessible ou ne pouvant plus être achetée par l’utilisateur. |
| `checkouts` | [[!UICONTROL Mesure]](./measure.md) | Action pendant le processus de passage en caisse d’une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s’il existe plusieurs étapes dans un processus de passage en caisse. S’il existe plusieurs étapes, les informations sur l’heure de l’événement et la page ou l’expérience référencée sont utilisées pour identifier l’étape et les événements individuels représentés dans l’ordre. |
| `inStorePurchase` | [[!UICONTROL Mesure]](./measure.md) | Décrit une valeur associée à un achat en magasin pour une utilisation Analytics. |
| `productListAdds` | [[!UICONTROL Mesure]](./measure.md) | L’ajout d’un produit à la liste de produits, par exemple un produit ajouté à un panier. |
| `productListOpens` | [[!UICONTROL Mesure]](./measure.md) | Initialisations d’une nouvelle liste de produits, par exemple un panier en cours de création. |
| `productListRemovals` | [[!UICONTROL Mesure]](./measure.md) | Suppression ou suppression d’une entrée de produit d’une liste de produits, telle qu’un produit supprimé d’un panier. |
| `productListReopens` | [[!UICONTROL Mesure]](./measure.md) | Liste de produits précédemment abandonnée qui a été réactivée par l’utilisateur. |
| `productListViews` | [[!UICONTROL Mesure]](./measure.md) | Décrit le moment où une ou plusieurs vues d’une liste de produits se sont produites. |
| `productViews` | [[!UICONTROL Mesure]](./measure.md) | Décrit le moment où une ou plusieurs vues d’un produit ont eu lieu. |
| `purchases` | [[!UICONTROL Mesure]](./measure.md) | Permet d’effectuer le suivi d’une commande acceptée. L’événement d’achat est la seule action requise dans une conversion commerciale. Une liste de produits doit être référencée pour l’événement d’achat. |
| `saveForLaters` | [[!UICONTROL Mesure]](./measure.md) | Une liste de produits est enregistrée pour une utilisation ultérieure, telle qu’une liste de souhaits. |

{style="table-layout:auto"}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)

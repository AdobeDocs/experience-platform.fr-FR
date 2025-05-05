---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;commerce;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Commerce
description: Découvrez le type de données du modèle de données d’expérience Commerce (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 11%

---

# Type de données [!UICONTROL Commerce]

[!UICONTROL Commerce] est un type de données XDM (Experience Data Model) standard qui décrit les enregistrements liés aux achats et ventes.

![Schéma du type de données [!UICONTROL Commerce].](../images/data-types/commerce.png)

| Nom d’affichage | Propriété | Type de données | Description |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL Commande] | `order` | [[!UICONTROL Commande]](./order.md) | Décrit la commande passée pour un ou plusieurs produits. |
| [!UICONTROL Identifiant de promotion] | `promotionID` | [!UICONTROL string] | Identifiant de promotion de la commande passée, le cas échéant. |
| [!UICONTROL Abandons de panier] | `cartAbandons` | [[!UICONTROL Mesure]](./measure.md) | Décrit lorsqu’une liste de produits a été identifiée comme n’étant plus accessible ou ne pouvant plus être achetée par l’utilisateur. |
| [!UICONTROL Passages en caisse] | `checkouts` | [[!UICONTROL Mesure]](./measure.md) | Action pendant le processus de passage en caisse d’une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s’il existe plusieurs étapes dans un processus de passage en caisse. S’il existe plusieurs étapes, les informations sur l’heure de l’événement et la page ou l’expérience référencée sont utilisées pour identifier l’étape et les événements individuels représentés dans l’ordre. |
| [!UICONTROL Ajout d’une liste de produits (panier)] | `productListAdds` | [[!UICONTROL Mesure]](./measure.md) | L’ajout d’un produit à la liste de produits, par exemple un produit ajouté à un panier. |
| [!UICONTROL Ouverture d’une liste de produits (panier)] | `productListOpens` | [[!UICONTROL Mesure]](./measure.md) | Initialisations d’une nouvelle liste de produits, par exemple un panier en cours de création. |
| [!UICONTROL &#x200B; Retraits de la liste de produits (panier)] | `productListRemovals` | [[!UICONTROL Mesure]](./measure.md) | Suppression ou suppression d’une entrée de produit d’une liste de produits, telle qu’un produit supprimé d’un panier. |
| [!UICONTROL Réouverture de la liste de produits (panier)] | `productListReopens` | [[!UICONTROL Mesure]](./measure.md) | Liste de produits précédemment abandonnée et réactivée par l’utilisateur. |
| [!UICONTROL Consultations de la liste de produits (panier)] | `productListViews` | [[!UICONTROL Mesure]](./measure.md) | Décrit lorsqu’une ou plusieurs vues d’une liste de produits se sont produites. La ou les vues d’une liste de produits se sont produites. |
| [!UICONTROL Consultations produits] | `productViews` | [[!UICONTROL Mesure]](./measure.md) | Décrit le moment où une ou plusieurs vues d’un produit ont eu lieu. |
| [!UICONTROL Achats] | `purchases` | [[!UICONTROL Mesure]](./measure.md) | Permet d’effectuer le suivi d’une commande acceptée. L’événement d’achat est la seule action requise dans une conversion commerciale. Une liste de produits doit être référencée pour l’événement d’achat. |
| [!UICONTROL Enregistrer pour plus tard] | `saveForLaters` | [[!UICONTROL Mesure]](./measure.md) | Décrit quand une liste de produits est enregistrée pour une utilisation ultérieure, telle qu’une liste de souhaits. |
| [!UICONTROL Achat en magasin] | `inStorePurchase` | [[!UICONTROL Mesure]](./measure.md) | Indique un achat &quot;inStore&quot;. Ces informations sont enregistrées pour une utilisation Analytics. |
| [!UICONTROL Panier] | `cart` | [[!UICONTROL cart]](./cart.md) | Propriétés du panier qui contient un ou plusieurs produits. |
| [!UICONTROL Expédition] | `shipping` | [[!UICONTROL shipping]](./shipping.md) | Informations sur l’expédition d’un ou de plusieurs produits. |
| [!UICONTROL Facturation] | `billing` | [[!UICONTROL billing]](#billing) | Informations de facturation pour un ou plusieurs paiements. |
| [!UICONTROL Achat instantané] | `instantPurchase` | [[!UICONTROL Mesure]](./measure.md) | Décrit le moment où un produit a été acheté instantanément, en ignorant éventuellement le panier ou en passant en caisse. |
| [!UICONTROL Ouverture de la liste de demandes] | `requisitionListOpens` | [[!UICONTROL Mesure]](./measure.md) | Indique l’initialisation d’une nouvelle liste de demandes d’achat. |
| [!UICONTROL Suppressions de la liste de demandes] | `requisitionListDeletes` | [[!UICONTROL Mesure]](./measure.md) | Indique la suppression de la liste des demandes d’achat. |
| [!UICONTROL Ajout De Liste De Requêtes] | `requisitionListAdds` | [[!UICONTROL Mesure]](./measure.md) | Indique l’ajout d’un ou de plusieurs produits à une liste de demandes d’achat. |
| [!UICONTROL &#x200B; Retraits de la liste de demandes] | `requisitionListRemovals` | [[!UICONTROL Mesure]](./measure.md) | Indique la suppression d’un ou de plusieurs produits d’une liste de produits de demande d’achat. |
| [!UICONTROL Liste des demandes] | `requisitionList` | [[!UICONTROL requisitionlist]](./requisition-list.md) | Propriétés de la liste de demandes créée par le client. |
| [!UICONTROL Périmètre] | `commerceScope` | [[!UICONTROL commercescope]](./commerce-scope.md) | Identifiants d’étendue de commerce de l’endroit où un événement s’est produit (affichage en magasin, magasin, site web, etc.). |

{style="table-layout:auto"}

## Type de données [!UICONTROL billing] {#billing}

[!UICONTROL billing] est un type de données XDM (Experience Data Model) standard qui contient des informations sur les détails de facturation. Plus précisément, il se concentre sur l’adresse de facturation.

![Schéma du type de données de facturation.](../images/data-types/billing.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL Adresse de facturation] | `address` | [[!UICONTROL Adresse postale]](./postal-address.md) | Adresse de facturation. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données [!UICONTROL Commerce], reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)

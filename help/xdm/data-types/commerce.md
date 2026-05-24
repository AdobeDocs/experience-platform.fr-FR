---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;commerce;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données Commerce
description: Découvrez le type de données du modèle de données d’expérience (XDM) Commerce.
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
TQID: https://experienceleague.adobe.com/zZfPy8gAFFH262LPQpLqBVtquxPbtUpQmkkpvkSYXGI
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 490
ht-degree: 7%

---

# Type de données [!UICONTROL Commerce]

[!UICONTROL Commerce] est un type de données XDM (modèle de données d’expérience) standard qui décrit les enregistrements liés à l’achat et à la vente.

![Diagramme du type de données [!UICONTROL Commerce].](../images/data-types/commerce.png)

| Nom d’affichage | Propriété | Type de données | Description |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL Order] | `order` | [[!UICONTROL Order]](./order.md) | Décrit la commande passée pour un ou plusieurs produits. |
| [!UICONTROL Promotion ID] | `promotionID` | [!UICONTROL string] | Identifiant de promotion de la commande passée, le cas échéant. |
| [!UICONTROL Cart Abandons] | `cartAbandons` | [[!UICONTROL Measure]](./measure.md) | Décrit lorsqu’une liste de produits a été identifiée comme n’étant plus accessible ou ne pouvant plus être achetée par l’utilisateur. |
| [!UICONTROL Checkouts] | `checkouts` | [[!UICONTROL Measure]](./measure.md) | Action pendant le processus de passage en caisse d’une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s’il existe plusieurs étapes dans un processus de passage en caisse. S’il existe plusieurs étapes, les informations sur l’heure de l’événement et la page ou l’expérience référencée sont utilisées pour identifier l’étape et les événements individuels représentés dans l’ordre. |
| [!UICONTROL Product List (Cart) Adds] | `productListAdds` | [[!UICONTROL Measure]](./measure.md) | Ajout d’un produit à la liste des produits, par exemple un produit ajouté à un panier. |
| [!UICONTROL Product List (Cart) Opens] | `productListOpens` | [[!UICONTROL Measure]](./measure.md) | Initialisations d’une nouvelle liste de produits, telle que la création d’un panier. |
| [!UICONTROL Product List (Cart) Removals] | `productListRemovals` | [[!UICONTROL Measure]](./measure.md) | Retrait ou suppression d’une entrée de produit d’une liste de produits, tel qu’un produit retiré d’un panier. |
| [!UICONTROL Product List (Cart) Reopens] | `productListReopens` | [[!UICONTROL Measure]](./measure.md) | Liste de produits précédemment abandonnés et réactivés par l’utilisateur. |
| [!UICONTROL Product List (Cart) Views] | `productListViews` | [[!UICONTROL Measure]](./measure.md) | Décrit le moment où une ou plusieurs vues d’une liste de produits se sont produites.Une liste de produits a été consultée une ou plusieurs fois. |
| [!UICONTROL Product Views] | `productViews` | [[!UICONTROL Measure]](./measure.md) | Décrit le moment où une ou plusieurs vues d’un produit individuel se sont produites. |
| [!UICONTROL Purchases] | `purchases` | [[!UICONTROL Measure]](./measure.md) | Permet de suivre l’acceptation d’une commande. L’événement d’achat est la seule action requise dans une conversion commerciale. L’événement d’achat doit avoir une liste de produits référencée. |
| [!UICONTROL Save For Laters] | `saveForLaters` | [[!UICONTROL Measure]](./measure.md) | Décrit à quel moment une liste de produits est enregistrée pour une utilisation ultérieure, telle qu’une liste de souhaits. |
| [!UICONTROL In Store Purchase] | `inStorePurchase` | [[!UICONTROL Measure]](./measure.md) | Indique un achat en magasin. Ces informations sont enregistrées à des fins d’analyse. |
| [!UICONTROL Cart] | `cart` | [[!UICONTROL cart]](./cart.md) | Propriétés du panier qui contient un ou plusieurs produits. |
| [!UICONTROL Shipping] | `shipping` | [[!UICONTROL shipping]](./shipping.md) | Détails d’expédition d’un ou de plusieurs produits. |
| [!UICONTROL Billing] | `billing` | [[!UICONTROL billing]](#billing) | Détails de facturation pour un ou plusieurs paiements. |
| [!UICONTROL Instant Purchase] | `instantPurchase` | [[!UICONTROL Measure]](./measure.md) | Décrit le moment où un produit a été acheté instantanément, pouvant ignorer le panier ou le passage en caisse. |
| [!UICONTROL Requisition List Opens] | `requisitionListOpens` | [[!UICONTROL Measure]](./measure.md) | Indique l&#39;initialisation d&#39;une nouvelle liste de demandes d&#39;approvisionnement. |
| [!UICONTROL Requisition List Deletes] | `requisitionListDeletes` | [[!UICONTROL Measure]](./measure.md) | Indique la suppression de la liste de demandes d&#39;approvisionnement. |
| [!UICONTROL Requisition List Adds] | `requisitionListAdds` | [[!UICONTROL Measure]](./measure.md) | Indique l&#39;ajout d&#39;un ou de plusieurs produits à une liste de demandes d&#39;approvisionnement. |
| [!UICONTROL Requisition List Removals] | `requisitionListRemovals` | [[!UICONTROL Measure]](./measure.md) | Indique le retrait d&#39;un ou de plusieurs produits d&#39;une liste de produits de demande d&#39;approvisionnement. |
| [!UICONTROL Requisition List] | `requisitionList` | [[!UICONTROL requisitionlist]](./requisition-list.md) | Propriétés de la liste de demandes d&#39;approvisionnement créée par le client. |
| [!UICONTROL Scope] | `commerceScope` | [[!UICONTROL commercescope]](./commerce-scope.md) | Identifiants d’étendue de commerce de l’emplacement où un événement s’est produit (vue de magasin, magasin, site web, etc.). |

{style="table-layout:auto"}

## Type de données [!UICONTROL billing] {#billing}

[!UICONTROL billing] est un type de données standard du modèle de données d’expérience (XDM) qui contient des informations sur les détails de facturation. Plus précisément, il se concentre sur l’adresse de facturation.

![Diagramme du type de données de facturation.](../images/data-types/billing.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL Billing Address] | `address` | [[!UICONTROL Postal Address]](./postal-address.md) | Adresse de facturation. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données [!UICONTROL Commerce], reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)

---
title: collecter des informations sur le commerce, les produits et les commandes à l’aide du SDK Web de Adobe Experience Platform ;
description: Découvrez comment ajouter des données relatives aux produits ou à un panier à l’aide du SDK Web de Adobe Experience Platform.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 37%

---

# Collecte d’informations sur le commerce, les produits et les commandes

Si votre entreprise vend des produits ou des services, vous pouvez utiliser cette page comme guide sur la manière de suivre ces produits et services.

Cette page utilise le groupe de champs XDM [Schéma Commerce](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md).

Ce groupe de champs se compose de deux parties principales :

* Objet `commerce`. Cet objet vous permet d’indiquer les actions qui se produisent dans le tableau `productListItems`.
* Le tableau `productListItems`.

>[!TIP]
>
>Si vous connaissez Adobe Analytics, l’objet `commerce` contient des données similaires aux événements commerciaux dans la variable `events`. Le tableau d’objets `productListItems` contient des données similaires à la variable `products`.

## Objet `commerce` {#commerce-object}

Cette section décrit les champs disponibles dans l’objet `commerce`.

>[!TIP]
>
>Une mesure comporte deux champs : `id` et `value`. La plupart du temps, vous utilisez uniquement le champ `value` (par exemple, `'value':1`). Le champ `id` vous permet de définir un identifiant unique pour le suivi lorsque la mesure a été envoyée. Pour plus d’informations, consultez la documentation XDM pour [Mesure](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) .

| Mesure | Recommandation | Description |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Facultative | Un panier n’est plus accessible ou ne peut plus être acheté par l’utilisateur. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Fortement recommandé | Un utilisateur ne recherche plus de produits mais est en train d’acheter un produit. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Fortement recommandé | Un produit est ajouté à une liste. Veillez à définir le produit dans `productListItems` en même temps. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Facultative | Une liste de produits est créée. Par exemple, un nouveau panier est créé. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Fortement recommandé | Un produit est supprimé d’une liste de produits. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Facultative | Une liste de produits est réactivée par l’utilisateur. Cette action se produit souvent dans les campagnes de remarketing. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Fortement recommandé | Une liste de produits est consultée. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Fortement recommandé | Une consultation d’un produit s’est produite. Veillez à définir le produit consulté dans `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Fortement recommandé | Une commande est acceptée. Doit avoir une liste de produits. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Facultative | Un produit est enregistré pour une utilisation ultérieure. |

{style="table-layout:auto"}

### Exemples d’objets `Commerce`

Développez la section ci-dessous pour voir un exemple de commande du SDK Web à l’aide d’un champ de l’objet `commerce`.

+++`productViews`

Un appel de base du SDK Web `sendEvent` définissant le champ `productViews` sur `1` :

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

+++

## Objet `order` {#order-object}

L’objet `commerce` contient un objet dédié pour la collecte des détails de commande. Il s’agit de l’objet `order` .

Cette section décrit tous les champs pris en charge par l’objet `order`.

| Champ | Option | Recommandation | Description |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) pour le total de la commande. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | Liste des paiements dans une commande. [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) comprend ce qui suit. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Facultatif | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) pour ce mode de paiement. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Fortement recommandé | Valeur du paiement dans le code de devise spécifié. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Fortement recommandé | Type de paiement (par exemple, `credit_card`, `gift_card`, `paypal`). Voir la liste des [valeurs connues](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) pour obtenir des détails. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Facultatif | ID unique pour cette transaction de paiement. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Fortement recommandé | Total de cette commande une fois toutes les remises et taxes appliquées. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Fortement recommandé | Identifiant unique attribué par le vendeur pour cet achat. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Facultatif | Identifiant unique attribué par l’acheteur pour cet achat. |

### Exemples d’objets de commande

Développez la section ci-dessous pour voir un exemple de commande de SDK Web à l’aide de l’objet `commerce`.

+++Exemple d’objet `Order`

Un appel du SDK Web `sendEvent` définissant l’objet `order` qui s’applique à plusieurs produits dans le tableau `productListItems` :

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

+++

## Objet de liste de produits {#product-list-object}

La liste de produits indique quels produits sont liés à l’action correspondante. Il s’agit d’une liste de [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). Chaque produit comporte plusieurs champs facultatifs.

| Champ | Recommandation | Description |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Facultatif | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) pour le produit. Ce champ s’applique généralement uniquement lorsque plusieurs produits de la liste de produits comportent des codes de devise différents. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Fortement recommandé | Définissez ce champ uniquement le cas échéant. Par exemple, il peut ne pas être possible de définir sur l’événement `productView` car différentes variantes du produit peuvent avoir des prix différents, mais sur un événement `productListAdds`. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Fortement recommandé | Identifiant XDM du produit. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Fortement recommandé | Méthode utilisée par le visiteur pour ajouter un produit à la liste. Défini avec des mesures `productListAdds` et utilisé uniquement lorsqu’un produit est ajouté à la liste. Par exemple, `add to cart button`, `quick add` et `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Fortement recommandé | Nom d’affichage ou nom lisible du produit. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Fortement recommandé | Nombre d’unités du produit que le client a indiqué. Doit être défini sur `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Fortement recommandé | Unité de gestion des stocks. Il s’agit de l’identifiant unique du produit. |

### Exemples de listes de produits

Développez les sections ci-dessous pour voir des exemples de commandes du SDK Web à l’aide de l’objet `productListItems`.

+++Exemple `productListItems`

Un appel du SDK Web `sendEvent` définissant le `productViews` pour plusieurs produits dans le tableau `productListItems` :

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

+++

+++`productListAdds` exemple

Un appel du SDK Web `sendEvent` définissant l’événement `productListAdds` pour plusieurs produits dans le tableau `productListItems` :

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

+++

+++Exemple `checkouts`

Un appel du SDK Web `sendEvent` définissant l’événement `checkouts` pour plusieurs produits dans le tableau `productListItems` :

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

+++

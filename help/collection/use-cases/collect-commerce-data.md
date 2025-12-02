---
title: Collectez des informations sur le commerce, les produits et les commandes à l’aide de Adobe Experience Platform Web SDK.
description: Découvrez comment ajouter des données relatives à des produits ou à un panier à l’aide de Adobe Experience Platform Web SDK.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 9b2ecedfafbafed042eba73a034cb9b9e95af579
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 37%

---

# Collecter des informations sur le commerce, les produits et les commandes

Si votre entreprise vend des produits ou des services, vous pouvez utiliser cette page comme guide sur la manière de suivre ces produits et services.

Cette page utilise le groupe de champs Schéma XDM [Commerce](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md).

Ce groupe de champs se compose de deux parties principales :

* Objet `commerce`. Cet objet vous permet d’indiquer les actions qui se produisent sur le tableau `productListItems`.
* Le tableau `productListItems`.

>[!TIP]
>
>Si vous connaissez Adobe Analytics, l’objet `commerce` contient des données similaires aux événements commerciaux dans la variable `events` . Le tableau d’objets `productListItems` contient des données similaires à la variable `products`.

## Objet `commerce` {#commerce-object}

Cette section décrit les champs disponibles dans l’objet `commerce`.

>[!TIP]
>
>Une mesure comporte deux champs : `id` et `value`. La plupart du temps, vous n’utilisez que le champ `value` (par exemple, `'value':1`). Le champ `id` vous permet de définir un identifiant unique pour le suivi lors de l’envoi de la mesure. Pour plus d’informations, consultez la documentation XDM relative à [Measure](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md).

| Mesure | Recommandation | Description |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Facultative | Un panier n’est plus accessible ou ne peut plus être acheté par l’utilisateur. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Hautement recommandé | Un utilisateur ne recherche plus de produits mais est en train d’acheter un produit. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Hautement recommandé | Un produit est ajouté à une liste. Veillez à définir le produit dans `productListItems` en même temps. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Facultative | Une liste de produits est créée. Par exemple, un nouveau panier est créé. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Hautement recommandé | Un produit est supprimé d’une liste de produits. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Facultative | Une liste de produits est réactivée par l’utilisateur. Cette action se produit souvent dans les campagnes de remarketing. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Hautement recommandé | Une liste de produits est consultée. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Hautement recommandé | Une vue d’un produit s’est produite. Veillez à définir le produit consulté dans `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Hautement recommandé | Une commande est acceptée. Doit avoir une liste de produits. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Facultative | Un produit est enregistré pour une utilisation ultérieure. |

{style="table-layout:auto"}

### Exemples d’objets `Commerce`

Développez la section ci-dessous pour afficher un exemple de commande Web SDK utilisant un champ de l’objet `commerce` .

+++`productViews`

Un appel de `sendEvent` Web SDK de base définissant le champ `productViews` sur `1` :

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

L’objet `commerce` contient un objet dédié à la collecte des détails de la commande. Il s’agit de l’objet `order`.

Cette section décrit tous les champs pris en charge par l’objet `order`.

| Champ | Option | Recommandation | Description |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) pour le total de la commande. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | Liste des paiements dans une commande. [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) comprend ce qui suit. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Facultatif | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) pour ce mode de paiement. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Hautement recommandé | Valeur du paiement dans le code de devise spécifié. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Hautement recommandé | Type de paiement (par exemple, `credit_card`, `gift_card`, `paypal`). Voir la liste des [valeurs connues](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) pour obtenir des détails. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Facultatif | ID unique pour cette transaction de paiement. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Hautement recommandé | Total de cette commande une fois toutes les remises et taxes appliquées. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Hautement recommandé | Identifiant unique attribué par le vendeur pour cet achat. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Facultatif | Identifiant unique attribué par l’acheteur pour cet achat. |

### Exemples d’objets de commande

Développez la section ci-dessous pour afficher un exemple de commande Web SDK utilisant l’objet `commerce`.

+++Exemple d’objet `Order`

Un appel de `sendEvent` Web SDK définissant l’objet `order` qui s’applique à plusieurs produits dans le tableau `productListItems` :

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
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Facultatif | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) du produit. Ce champ s’applique uniquement lorsque la liste de produits comporte plusieurs produits avec différents codes de devise. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Hautement recommandé | Définissez ce champ uniquement le cas échéant. Par exemple, il se peut qu’il ne soit pas possible de définir sur `productView` événement , car différentes variations du produit peuvent avoir des prix différents, mais sur un événement `productListAdds`. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Hautement recommandé | Identifiant XDM du produit. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Hautement recommandé | Méthode utilisée par le visiteur pour ajouter un produit à la liste. Défini avec des mesures `productListAdds` et utilisé uniquement lorsqu’un produit est ajouté à la liste. Par exemple, `add to cart button`, `quick add` et `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Hautement recommandé | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Hautement recommandé | Nombre d’unités du produit que le client a indiqué. Doit être défini sur `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Hautement recommandé | Unité de gestion des stocks. Il s’agit de l’identifiant unique du produit. |

### Exemples de listes de produits

Développez les sections ci-dessous pour afficher des exemples de commandes Web SDK utilisant l’objet `productListItems`.

+++`productListItems` exemple

Un appel de `sendEvent` Web SDK définissant la `productViews` de plusieurs produits dans le tableau `productListItems` :

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

Un appel de `sendEvent` Web SDK définissant l’événement `productListAdds` pour plusieurs produits dans le tableau de `productListItems` :

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

+++`checkouts` exemple

Un appel de `sendEvent` Web SDK définissant l’événement `checkouts` pour plusieurs produits dans le tableau de `productListItems` :

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

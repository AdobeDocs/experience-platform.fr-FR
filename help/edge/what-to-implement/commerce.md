---
title: 'Variable '
seo-title: Prise en charge des produits avec le SDK Web d’Adobe Experience Platform
description: Découvrez comment ajouter des données si vous disposez de produits ou d’un panier d’achat avec le SDK Web Experience Platform
seo-description: Découvrez comment ajouter des données si vous disposez de produits ou d’un panier d’achat avec le SDK Web Experience Platform
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Bêta) Produits

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Si votre site contient des produits, il s’agit d’un ensemble par défaut de choses que vous souhaitez peut-être envoyer pour activer le plus de fonctionnalités d’Adobe. Bien qu&#39;il s&#39;agisse d&#39;une suggestion, il fournit un ensemble très solide de données directement à partir du .

Ce utilise le mixin [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) . Le `commerce` mixin est divisé en deux parties : l’ `commerce` objet et le `productListItems` tableau. L’ `commerce` objet vous permet d’indiquer les actions qui se produisent dans le `productListItems` tableau.

>[!Tip]
>Si vous êtes familiarisé avec Adobe Analytics, La `commerce` est plus étroitement liée à la `events` variable. La variable `productListItems` est plus étroitement liée à la `products` variable.

## Actions liées aux produits

Vous trouverez ci-dessous un de `measures` disponibles dans l’ `commerce` objet.

>[!Tip]
>Une mesure comporte deux champs : `id` et `value`. La plupart du temps, vous utiliserez uniquement le `value` champ (par exemple, `'value':1`). Le `id` champ vous permet de définir un identifiant unique que vous pouvez utiliser pour suivre le moment où la mesure a été envoyée. Voir la documentation XDM pour [Measurement](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Mesurer** | **Recommandation** | **Description** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Facultatif | Un panier n’est plus accessible ou ne peut plus être acheté par l’utilisateur. |
| [passages en caisse](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Fortement recommandé | Un utilisateur ne recherche plus de produits mais est en train d’acheter un produit. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Fortement recommandé | Un produit est ajouté à un  de. Veillez à définir le produit en `productListItems` même temps. |
| [productListOpen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Facultatif | Un nouveau de produits est créé. (Par exemple, un nouveau panier est créé.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Fortement recommandé | Un produit est supprimé d’un  de produit. |
| [productListReouvertures](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Facultatif | Un de produit est réactivé par l’utilisateur. Cela arrive souvent en . |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Fortement recommandé | Un  de produits est affiché. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Fortement recommandé | Un  de produit s&#39;est produit. Veillez à définir le produit affiché dans le `productListItems`. |
| [achats](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Fortement recommandé | Une commande est acceptée. Doit avoir un de produit. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Facultatif | Un produit est enregistré pour une utilisation ultérieure. |

Voici un exemple de la manière dont vous les définiriez `Measures` dans le SDK.

```javascript
alloy("event", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

L’objet de commerce dispose également d’un champ spécial pour la collecte des détails de commande appelé `order`.

| **Commande** | **Option** | **Recommandation** | **Description** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | Devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) pour le total de la commande. |
| [paiements[payItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | de paiements sur commande. Un [objet](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) paiementItemcomprend les éléments suivants. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Facultatif | Devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) pour ce mode de paiement. |
|  | [payAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Fortement recommandé | Valeur du paiement dans le code de devise spécifié. |
|  | [payType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Fortement recommandé | Type de paiement (par exemple, `credit_card`, `gift_card`, `paypal`). Pour plus d’informations, reportez-vous au  des valeurs [](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) connues. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Facultatif | ID unique pour cette transaction de paiement. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Fortement recommandé | Le total de cette commande après toutes les remises et taxes appliquées. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Très recommandé | Identifiant unique attribué par le vendeur pour cet achat. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Facultatif | Identifiant unique attribué par l’acheteur pour cet achat. |

Voici un exemple d’achat type dans le SDK.

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
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
        "qauntity":1
      }
    ]
  }
});
```

##  de produits

Le de produits indique quels produits sont liés à l’action correspondante. Il s’agit d’un  de [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Chaque produit comporte un certain nombre de champs facultatifs.

| **Champ** | **Recommandation** | **Description** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Facultatif | Devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) pour le produit. Cela n’est utile que lorsque vous pouvez avoir des produits avec des codes de devise différents et qu’ils s’appliquent. Par exemple, en cas d’achat ou d’ajout au panier. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Fortement recommandé | Ne doit être définie que le cas échéant. Par exemple, il peut ne pas être possible de définir sur `productView` parce que différentes variations du produit peuvent avoir des prix différents mais sur un `productListAdds`. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Fortement recommandé | ID XDM du produit. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Fortement recommandé | Méthode utilisée pour ajouter un article de produit au  par le. Défini avec `productListAdds` des mesures et ne doit être utilisé que lorsqu’un produit est ajouté au . Par exemple, `add to cart button`, `quick add`et `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Fortement recommandé | Il s’agit du nom d’affichage ou du nom lisible du produit. |
| [quantité](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Fortement recommandé | Nombre d&#39;unités que le client a indiqué avoir besoin du produit. Doit être défini sur `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Fortement recommandé | Unité de conservation de la boutique. Il s’agit de l’identifiant unique du produit. |

## Exemples

`productView` event

```javascript
alloy("event",{
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

`productView` event

```javascript
alloy("event",{
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

`checkout` event

```javascript
alloy("event",{
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

`purchase` event

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
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
        "qauntity":1
      }
    ]
  }
});
```

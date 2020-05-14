---
title: Produits
seo-title: Prise en charge des produits avec le SDK Web d’Adobe Experience Platform
description: Découvrez comment ajouter des données si vous disposez de produits ou d’un panier d’achat avec le SDK Web Experience Platform
seo-description: Découvrez comment ajouter des données si vous disposez de produits ou d’un panier d’achat avec le SDK Web Experience Platform
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 100%

---


# Produits

Si votre site contient des produits, il s’agit d’un ensemble par défaut d’éléments que vous souhaiterez peut-être envoyer pour activer les fonctionnalités essentielles d’Adobe. Bien qu’il s’agisse d’une suggestion, un ensemble très solide de données est fourni dès le départ.

Ce document utilise le mixin [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md). Le mixin `commerce` est divisé en deux parties : l’objet `commerce`et le tableau `productListItems`. L’objet `commerce` vous permet d’indiquer les actions qui se produisent dans le tableau `productListItems`.

>[!Tip]
>Si vous maîtrisez Adobe Analytics, `commerce` est plus étroitement lié à la variable `events`. `productListItems` est plus étroitement lié à la variable `products`.

## Actions liées aux produits

Vous trouverez ci-dessous une liste de `measures` disponibles dans l’objet `commerce`.

>[!Tip]
>Une mesure comporte deux champs : `id` et `value`. La plupart du temps, vous utiliserez uniquement le champ `value` (par exemple, `'value':1`). Le champ `id` vous permet de définir un identifiant unique que vous pouvez utiliser pour suivre le moment où la mesure a été envoyée. Voir la documentation XDM pour [Mesure](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Mesure** | **Recommandation** | **Description** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Facultative | Un panier n’est plus accessible ou ne peut plus être acheté par l’utilisateur. |
| [checkouts](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Fortement recommandée | Un utilisateur ne recherche plus de produits mais est en train d’acheter un produit. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Fortement recommandée | Un produit est ajouté à une liste. Veillez à définir le produit dans `productListItems` en même temps. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Facultative | Une liste de produits est créée. (Par exemple, un nouveau panier est créé.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Fortement recommandée | Un produit est supprimé d’une liste de produits. |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Facultative | Une liste de produits est réactivée par l’utilisateur. Cela se produit souvent dans les campagnes de remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Fortement recommandée | Une liste de produits est consultée. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Fortement recommandée | Une consultation de produit s’est produite. Veillez à définir le produit consulté dans `productListItems`. |
| [purchases](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Fortement recommandée | Une commande est acceptée. Doit avoir une liste de produits. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Facultative | Un produit est enregistré pour une utilisation ultérieure. |

Voici un exemple de la manière dont vous définiriez ces `Measures` dans le SDK.

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

L’objet de commerce dispose également d’un champ spécial pour la collecte des détails de commande appelé `order`.

| **Commande** | **Option** | **Recommandation** | **Description** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) pour le total de la commande. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | Liste des paiements dans une commande. [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) comprend ce qui suit. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Facultatif | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) pour ce mode de paiement. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Fortement recommandé | Valeur du paiement dans le code de devise spécifié. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Fortement recommandé | Type de paiement (par exemple, `credit_card`, `gift_card`, `paypal`). Voir la liste des [valeurs connues](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) pour obtenir des détails. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Facultatif | Identifiant unique pour cette transaction de paiement. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Fortement recommandé | Total de cette commande une fois toutes les remises et taxes appliquées. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Fortement recommandé | Identifiant unique attribué par le vendeur pour cet achat. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Facultatif | Identifiant unique attribué par l’acheteur pour cet achat. |

Voici un exemple d’achat type dans le SDK.

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

## Listes de produits

La liste de produits indique quels produits sont liés à l’action correspondante. Il s’agit d’une liste de [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Chaque produit comporte un certain nombre de champs facultatifs.

| **Champ** | **Recommandation** | **Description** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Facultatif | Devise [ISO 4217](https://fr.wikipedia.org/wiki/ISO_4217) pour le produit. Cette valeur n’est utile que lorsque vous pouvez avoir des produits avec des codes de devise différents et lorsqu’elle est applicable. Par exemple, en cas d’achat ou d’ajout au panier. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Fortement recommandé | Ne doit être défini que le cas échéant. Par exemple, il peut ne pas être possible d’effectuer une définition sur `productView`, car différentes variantes du produit peuvent avoir des prix différents, mais sur `productListAdds`. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Fortement recommandé | Identifiant XDM du produit. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Fortement recommandé | Méthode utilisée par le visiteur pour ajouter un produit à la liste. Défini avec des mesures `productListAdds` et ne doit être utilisé que lorsqu’un produit est ajouté à la liste. Par exemple, `add to cart button`, `quick add` et `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Fortement recommandé | Il s’agit du nom d’affichage ou du nom lisible du produit. |
| [quantity](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Fortement recommandé | Nombre d’unités du produit que le client a indiqué. Doit être défini sur `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Fortement recommandé | Unité de gestion des stocks. Il s’agit de l’identifiant unique du produit. |

## Exemples

Événement `productView`

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

Événement `productView`

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

Événement `checkout`

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

Événement `purchase`

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
